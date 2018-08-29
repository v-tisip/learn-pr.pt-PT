Trabalhar com um blob individual no SDK de Armazenamento do Azure para .NET Core exige uma *referência de blob*, uma instância de um objeto `ICloudBlob`.

Pode obter um `ICloudBlob` ao pedi-lo com o nome do blob ou selecioná-lo a partir de uma lista de blobs no contentor. Ambos necessitam de um `CloudBlobContainer`, que vimos como obter na última unidade.

## <a name="getting-blobs-by-name"></a>Obter blobs por nome

Chame um dos métodos `GetXXXReference` num `CloudBlobContainer` para obter um `ICloudBlob` por nome. Se conhecer o tipo de blob que está a obter, é preferível utilizar um dos métodos mais específicos (`GetBlockBlobReference`, `GetAppendBlobReference` ou `GetPageBlobReference`).

Nenhum destes métodos faz uma chamada de rede nem confirma se o blob existe ou não. Um método separado, `GetBlobReferenceFromServerAsync`, chama a API de armazenamento do Blob e lança uma exceção se o blob ainda não existir.

## <a name="listing-blobs-in-a-container"></a>Listar blobs num contentor

Pode obter uma lista dos blobs num contentor com o método `ListBlobsSegmentedAsync` do `CloudBlobContainer`. *Segmented* refere-se às páginas separadas de resultados devolvidos, uma chamada única para `ListBlobsSegmentedAsync` nunca garante a devolução de todos os resultados numa única página. Poderemos ter de chamá-la repetidamente através do `ContinuationToken` que devolver para percorrer as páginas. Isto torna o código para listagem de blobs um pouco mais complexo do que o código para carregar ou transferir, mas existe um padrão-tipo que pode utilizar para obter todos os blobs num contentor:

```csharp
BlobContinuationToken continuationToken = null;
BlobResultSegment resultSegment = null; 

do
{
    resultSegment = await container.ListBlobsSegmentedAsync(continuationToken);

    // Do work here on resultSegment.Results

    continuationToken = resultSegment.ContinuationToken;
} while (continuationToken != null);
```

Isto irá chamar `ListBlobsSegmentedAsync` repetidamente até o `continuationToken` ser `null`, o que assinala o fim dos resultados.

### <a name="processing-list-results"></a>Processamento de resultados de lista

O objeto que irá receber de `ListBlobsSegmentedAsync` contém uma propriedade `Results` do tipo `IEnumerable<IListBlobItem>`. Os `IListBlobItem`s contêm uma série de propriedades sobre o contentor e URL do blob, mas não contêm métodos de carregamento ou transferência. Isto deve-se ao facto de alguns objetos de resultados poderem ser objetos `CloudBlobDirectory` que representam diretórios e não blobs individuais.

Caso só esteja interessado em blobs individuais, pode utilizar o método `OfType<>` para filtrar os resultados. Eis alguns exemplos:

```csharp
// Get all blobs
var allBlobs = resultSegment.Results.OfType<ICloudBlob>();

// Get only block blobs
var blockBlobs = resultSegment.Results.OfType<CloudBlockBlob();
```

A utilização de `OfType<>` exige uma referência ao espaço de nomes `System.Linq` (`using System.Linq;`).

## <a name="exercise"></a>Exercício

Uma das funcionalidades na nossa aplicação exige a obtenção de uma lista de blobs da API. Iremos utilizar o padrão acima para listar todos os blobs no nosso contentor. Ao processarmos a lista, obteremos o nome de cada blob.

Abra o `BlobStorage.cs` no editor e preencha `GetNames` com o seguinte código:

```csharp
public async Task<IEnumerable<string>> GetNames()
{
    List<string> names = new List<string>();

    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);

    BlobContinuationToken continuationToken = null;
    BlobResultSegment resultSegment = null;

    do
    {
        resultSegment = await container.ListBlobsSegmentedAsync(continuationToken);

        // Get the name of each blob.
        names.AddRange(resultSegment.Results.OfType<ICloudBlob>().Select(b => b.Name));

        continuationToken = resultSegment.ContinuationToken;
    } while (continuationToken != null);

    return names;
}
```

Os nomes devolvidos por este método são processados por `FilesController` para os converter em URLs. Quando são devolvidos ao cliente, são compostos como hiperligações na página.