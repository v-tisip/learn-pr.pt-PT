Segue-se o fluxo de trabalho típico para as aplicações que utilizam o armazenamento de Blobs do Azure:

1. **Obter configuração**: No arranque, carregue a configuração, como a cadeia de ligação com a chave de conta. Isto é preciso para autenticar as chamadas à API.
1. **Inicializar o cliente**: Utilize a cadeia de ligação para inicializar a biblioteca de cliente de Armazenamento do Azure. Esta ação cria os objetos que a aplicação irá utilizar para trabalhar com a API de Armazenamento de blobs.
1. **Utilizar**: Faça chamadas à API com a biblioteca de cliente para operar em contentores e blobs.

## <a name="configure-your-connection-string"></a>Configurar a cadeia de ligação

Antes de escrever qualquer código, irá precisar da cadeia de ligação para a conta de armazenamento que irá utilizar. 

A cadeia de ligação inclui a sua chave de conta. A chave da conta é considerada um segredo e deve ser armazenada em segurança. Iremos armazenar a cadeia de ligação numa definição de aplicação do Serviço de Aplicações. Uma definição da aplicação é um local seguro para segredos da aplicação, mas não suporta o desenvolvimento local e não é uma solução robusta de ponto a ponto por conta própria.

> [!WARNING]
> **Não coloque as chaves da conta de armazenamento no código ou nos ficheiros de configuração não protegidos.** As chaves de conta de armazenamento permitem acesso total à sua conta de armazenamento. A fuga de uma chave pode resultar em danos irrecuperáveis e faturas altas. Veja a secção Recursos Adicionais no final deste módulo para obter documentação de orientação de armazenamento e conselhos sobre como recuperar de uma chave perdida.

## <a name="initialize-the-blob-storage-object-model"></a>Inicializar o modelo de objeto de Armazenamento de blobs

No SDK de Armazenamento do Azure para .NET Core, o padrão habitual para utilizar o Armazenamento de blobs inclui os seguintes passos:

1. Chame `CloudStorageAccount.Parse` (ou `TryParse`) com a sua cadeia de ligação para obter um `CloudStorageAccount`.
1. Chame `CreateCloudBlobClient` no `CloudStorageAccount` para obter um `CloudBlobClient`.
1. Chame `GetContainerReference` no `CloudBlobClient` para obter um `CloudBlobContainer`.
1. Utilize métodos no contentor para obter uma lista de blobs e/ou obter referências para blobs individuais para carregar e transferir dados.

No código, os passos 1&ndash;3 são semelhantes ao seguinte:

```csharp
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString); // or TryParse()
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference(containerName);
```

Nenhum deste código de inicialização faz chamadas através da rede. O que significa que as exceções que ocorrem de informações incorretas não serão geradas mais tarde; por exemplo, a chamada para `GetContainerReference` terá êxito se o contentor existir, ou não, na conta.

## <a name="create-containers-at-startup"></a>Criar contentores no arranque

É prática comum para aplicações criar contentores que são precisos no código, mesmo quando sabemos quais serão esses contentores antecipadamente. Chamar `CreateIfNotExistsAsync` num `CloudBlobContainer` é a melhor forma de o fazer, e devemos utilizá-lo para criar cada contentor que sabemos que iremos precisar antes o utilizar.

`CreateIfNotExistsAsync` *faz* uma chamada de rede para o Armazenamento do Azure. É melhor prática fazer uma chamada para o mesmo no arranque, e não sempre que acedemos a um contentor.

## <a name="exercise"></a>Exercício

### <a name="clone-and-explore-the-unfinished-app"></a>Clonar e explorar a aplicação não terminada

Primeiro, vamos clonar a aplicação de arranque a partir do GitHub. No terminal do Cloud Shell, execute o seguinte comando para obter uma cópia do código fonte e abra-o no editor:

```console
git clone TODO
cd TODO
code .
```

Abra o ficheiro `Controllers/FilesController.cs`.

Este controlador implementa uma API com três ações:

* **Indexar** (POST /api/Files) devolve uma lista de URLs, um para cada ficheiro que foi carregado. O front-end de aplicação chama este método para criar uma lista de hiperlinks para os ficheiros carregados.
* **Carregar** (POST /api/Files) recebe um ficheiro carregado e guarda-o.
* **Transferir** (GET /api/Files/{file-name}) transfere um ficheiro individual pelo seu nome.

Cada método utiliza uma instância `IStorage` chamada `storage` para realizar o seu trabalho. Existe uma implementação incompleta de `IStorage` em `Models/BlobStorage.cs`.

### <a name="add-the-nuget-package"></a>Adicionar o pacote NuGet

Primeiro, adicione uma referência ao SDK de Armazenamento do Azure. No terminal, execute o seguinte:

```console
dotnet add package WindowsAzure.Storage
dotnet restore
```

Isto irá garantir que estamos a utilizar a versão mais recente da biblioteca de clientes de Armazenamento de blobs.

### <a name="configure"></a>Configurar

A nossa aplicação de arranque já inclui a ligação de configuração que precisamos. O parâmetro de construtor `IOptions<AzureStorageConfig>` no `BlobStorage` tem duas propriedades: a cadeia de ligação da conta de armazenamento e o nome do contentor em que a nossa aplicação irá armazenar os blobs. Existe código no método `ConfigureServices` de `Startup.cs` que carrega os valores da configuração quando a aplicação é iniciada.

Neste exercício, iremos executar a aplicação no Serviço de Aplicações do Azure, pelo que iremos adicionar mais tarde os valores de configuração nas definições de aplicação do Serviço de Aplicações. Por enquanto, não precisamos de realizar qualquer ação relacionada com a configuração.

### <a name="initialize"></a>Inicializar

Abra `BlobStorage.cs`.

Localização do método `Initialize`. A nossa aplicação irá chamar este método quando for utilizado pela primeira vez. Se estiver curioso, pode dar uma vista de olhos em `ConfigureServices` em `Startup.cs` para ver como isto é feito. 

`Initialize` é onde queremos criar o nosso contentor se ainda não existir. Preencha `Initialize` com o código seguinte e guarde o seu trabalho:

```csharp
public Task Initialize()
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    return container.CreateIfNotExistsAsync();
}
```