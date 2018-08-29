<span data-ttu-id="f9ab8-101">Trabalhar com um blob individual no SDK de Armazenamento do Azure para .NET Core exige uma *referência de blob*, uma instância de um objeto `ICloudBlob`.</span><span class="sxs-lookup"><span data-stu-id="f9ab8-101">Working with an individual blob in the Azure Storage SDK for .NET Core requires a *blob reference* &mdash; an instance of an `ICloudBlob` object.</span></span>

<span data-ttu-id="f9ab8-102">Pode obter um `ICloudBlob` ao pedi-lo com o nome do blob ou selecioná-lo a partir de uma lista de blobs no contentor.</span><span class="sxs-lookup"><span data-stu-id="f9ab8-102">You can get an `ICloudBlob` by requesting it with the blob's name or selecting it from a list of blobs in the container.</span></span> <span data-ttu-id="f9ab8-103">Ambos necessitam de um `CloudBlobContainer`, que vimos como obter na última unidade.</span><span class="sxs-lookup"><span data-stu-id="f9ab8-103">Both require a `CloudBlobContainer`, which we saw how to get in the last unit.</span></span>

## <a name="getting-blobs-by-name"></a><span data-ttu-id="f9ab8-104">Obter blobs por nome</span><span class="sxs-lookup"><span data-stu-id="f9ab8-104">Getting blobs by name</span></span>

<span data-ttu-id="f9ab8-105">Chame um dos métodos `GetXXXReference` num `CloudBlobContainer` para obter um `ICloudBlob` por nome.</span><span class="sxs-lookup"><span data-stu-id="f9ab8-105">Call one of the `GetXXXReference` methods on a `CloudBlobContainer` to get an `ICloudBlob` by name.</span></span> <span data-ttu-id="f9ab8-106">Se conhecer o tipo de blob que está a obter, é preferível utilizar um dos métodos mais específicos (`GetBlockBlobReference`, `GetAppendBlobReference` ou `GetPageBlobReference`).</span><span class="sxs-lookup"><span data-stu-id="f9ab8-106">If you know the type of the blob you are retrieving, prefer using one of the more specific methods (`GetBlockBlobReference`, `GetAppendBlobReference`, or `GetPageBlobReference`).</span></span>

<span data-ttu-id="f9ab8-107">Nenhum destes métodos faz uma chamada de rede nem confirma se o blob existe ou não.</span><span class="sxs-lookup"><span data-stu-id="f9ab8-107">None of these methods make a network call, nor do they confirm whether or not the blob actually exists.</span></span> <span data-ttu-id="f9ab8-108">Um método separado, `GetBlobReferenceFromServerAsync`, chama a API de armazenamento do Blob e lança uma exceção se o blob ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="f9ab8-108">A separate method, `GetBlobReferenceFromServerAsync`, does call the Blob storage API and will throw an exception if the blob doesn't already exist.</span></span>

## <a name="listing-blobs-in-a-container"></a><span data-ttu-id="f9ab8-109">Listar blobs num contentor</span><span class="sxs-lookup"><span data-stu-id="f9ab8-109">Listing blobs in a container</span></span>

<span data-ttu-id="f9ab8-110">Pode obter uma lista dos blobs num contentor com o método `ListBlobsSegmentedAsync` do `CloudBlobContainer`.</span><span class="sxs-lookup"><span data-stu-id="f9ab8-110">You can get a list of the blobs in a container using `CloudBlobContainer`'s `ListBlobsSegmentedAsync` method.</span></span> <span data-ttu-id="f9ab8-111">*Segmented* refere-se às páginas separadas de resultados devolvidos, uma chamada única para `ListBlobsSegmentedAsync` nunca garante a devolução de todos os resultados numa única página.</span><span class="sxs-lookup"><span data-stu-id="f9ab8-111">*Segmented* refers to the separate pages of results returned &mdash; a single call to `ListBlobsSegmentedAsync` is never guaranteed to return all the results in a single page.</span></span> <span data-ttu-id="f9ab8-112">Poderemos ter de chamá-la repetidamente através do `ContinuationToken` que devolver para percorrer as páginas.</span><span class="sxs-lookup"><span data-stu-id="f9ab8-112">We may need to call it repeatedly using the `ContinuationToken` it returns to work our way through the pages.</span></span> <span data-ttu-id="f9ab8-113">Isto torna o código para listagem de blobs um pouco mais complexo do que o código para carregar ou transferir, mas existe um padrão-tipo que pode utilizar para obter todos os blobs num contentor:</span><span class="sxs-lookup"><span data-stu-id="f9ab8-113">This makes the code for listing blobs a little more complex than the code for uploading or downloading, but there's a standard pattern you can use to get every blob in a container:</span></span>

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

<span data-ttu-id="f9ab8-114">Isto irá chamar `ListBlobsSegmentedAsync` repetidamente até o `continuationToken` ser `null`, o que assinala o fim dos resultados.</span><span class="sxs-lookup"><span data-stu-id="f9ab8-114">This will call `ListBlobsSegmentedAsync` repeatedly until `continuationToken` is `null`, which signals the end of the results.</span></span>

### <a name="processing-list-results"></a><span data-ttu-id="f9ab8-115">Processamento de resultados de lista</span><span class="sxs-lookup"><span data-stu-id="f9ab8-115">Processing list results</span></span>

<span data-ttu-id="f9ab8-116">O objeto que irá receber de `ListBlobsSegmentedAsync` contém uma propriedade `Results` do tipo `IEnumerable<IListBlobItem>`.</span><span class="sxs-lookup"><span data-stu-id="f9ab8-116">The object you'll get back from `ListBlobsSegmentedAsync` contains a `Results` property of type `IEnumerable<IListBlobItem>`.</span></span> <span data-ttu-id="f9ab8-117">Os `IListBlobItem`s contêm uma série de propriedades sobre o contentor e URL do blob, mas não contêm métodos de carregamento ou transferência.</span><span class="sxs-lookup"><span data-stu-id="f9ab8-117">`IListBlobItem`s contain a handful of properties about the blob's container and URL, but no upload or download methods.</span></span> <span data-ttu-id="f9ab8-118">Isto deve-se ao facto de alguns objetos de resultados poderem ser objetos `CloudBlobDirectory` que representam diretórios e não blobs individuais.</span><span class="sxs-lookup"><span data-stu-id="f9ab8-118">This is because some of the result objects may be `CloudBlobDirectory` objects that represent virtual directories rather than individual blobs.</span></span>

<span data-ttu-id="f9ab8-119">Caso só esteja interessado em blobs individuais, pode utilizar o método `OfType<>` para filtrar os resultados.</span><span class="sxs-lookup"><span data-stu-id="f9ab8-119">If you are only interested in individual blobs, you can use the `OfType<>` method to filter the results.</span></span> <span data-ttu-id="f9ab8-120">Eis alguns exemplos:</span><span class="sxs-lookup"><span data-stu-id="f9ab8-120">Here are a few examples:</span></span>

```csharp
// Get all blobs
var allBlobs = resultSegment.Results.OfType<ICloudBlob>();

// Get only block blobs
var blockBlobs = resultSegment.Results.OfType<CloudBlockBlob();
```

<span data-ttu-id="f9ab8-121">A utilização de `OfType<>` exige uma referência ao espaço de nomes `System.Linq` (`using System.Linq;`).</span><span class="sxs-lookup"><span data-stu-id="f9ab8-121">Using `OfType<>` will require a reference to the `System.Linq` namespace (`using System.Linq;`).</span></span>

## <a name="exercise"></a><span data-ttu-id="f9ab8-122">Exercício</span><span class="sxs-lookup"><span data-stu-id="f9ab8-122">Exercise</span></span>

<span data-ttu-id="f9ab8-123">Uma das funcionalidades na nossa aplicação exige a obtenção de uma lista de blobs da API.</span><span class="sxs-lookup"><span data-stu-id="f9ab8-123">One of the features in our app requires getting a list of blobs from the API.</span></span> <span data-ttu-id="f9ab8-124">Iremos utilizar o padrão acima para listar todos os blobs no nosso contentor.</span><span class="sxs-lookup"><span data-stu-id="f9ab8-124">We'll use the pattern shown above to list all the blobs in our container.</span></span> <span data-ttu-id="f9ab8-125">Ao processarmos a lista, obteremos o nome de cada blob.</span><span class="sxs-lookup"><span data-stu-id="f9ab8-125">As we process the list, we get the name of each blob.</span></span>

<span data-ttu-id="f9ab8-126">Abra o `BlobStorage.cs` no editor e preencha `GetNames` com o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="f9ab8-126">Open `BlobStorage.cs` in the editor and fill in `GetNames` with the following code:</span></span>

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

<span data-ttu-id="f9ab8-127">Os nomes devolvidos por este método são processados por `FilesController` para os converter em URLs.</span><span class="sxs-lookup"><span data-stu-id="f9ab8-127">The names returned by this method are processed by `FilesController` to turn them into URLs.</span></span> <span data-ttu-id="f9ab8-128">Quando são devolvidos ao cliente, são compostos como hiperligações na página.</span><span class="sxs-lookup"><span data-stu-id="f9ab8-128">When they are returned to the client, they are rendered as hyperlinks on the page.</span></span>