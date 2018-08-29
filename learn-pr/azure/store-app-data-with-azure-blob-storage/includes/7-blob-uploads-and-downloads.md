<span data-ttu-id="a4ad1-101">Assim que tivermos uma referência para um blob, podemos carregar e transferir dados.</span><span class="sxs-lookup"><span data-stu-id="a4ad1-101">Once we have a reference to a blob, we can upload and download data.</span></span> <span data-ttu-id="a4ad1-102">Os objetos `ICloudBlob` têm métodos `Upload` e `Download` que oferecem suporte a matrizes de bytes, fluxos e arquivos como origens e destinos.</span><span class="sxs-lookup"><span data-stu-id="a4ad1-102">`ICloudBlob` objects have `Upload` and `Download` methods that support byte arrays, streams, and files as sources and targets.</span></span> <span data-ttu-id="a4ad1-103">Os tipos específicos têm métodos adicionais para a sua conveniência &mdash; por exemplo, `CloudBlockBlob` suporta o carregamento e a transferência de cadeias de caracteres com `UploadTextAsync` e `DownloadTextAsync`.</span><span class="sxs-lookup"><span data-stu-id="a4ad1-103">Specific types have additional methods for convenience &mdash; for example, `CloudBlockBlob` supports uploading and downloading strings with `UploadTextAsync` and `DownloadTextAsync`.</span></span>

## <a name="creating-new-blobs"></a><span data-ttu-id="a4ad1-104">Criar novos blobs</span><span class="sxs-lookup"><span data-stu-id="a4ad1-104">Creating new blobs</span></span>

<span data-ttu-id="a4ad1-105">Para criar um blob novo, chama um dos métodos `Upload` num blob que não existe.</span><span class="sxs-lookup"><span data-stu-id="a4ad1-105">To create a new blob, you call one of the `Upload` methods on a blob that doesn't exist.</span></span> <span data-ttu-id="a4ad1-106">Isso faz duas coisas: cria o blob e carrega os dados.</span><span class="sxs-lookup"><span data-stu-id="a4ad1-106">This does two things: creates the blob and uploads the data.</span></span> 

## <a name="moving-data-to-and-from-blobs"></a><span data-ttu-id="a4ad1-107">Mover dados de e para blobs</span><span class="sxs-lookup"><span data-stu-id="a4ad1-107">Moving data to and from blobs</span></span>

<span data-ttu-id="a4ad1-108">Mover dados de e para um blob é uma operação de rede que demora algum tempo.</span><span class="sxs-lookup"><span data-stu-id="a4ad1-108">Moving data to and from a blob is a network operation that takes time.</span></span> <span data-ttu-id="a4ad1-109">No SDK de Armazenamento do Azure para .NET Core, todos os métodos que requeiram a atividade de rede devolvem `Task`s, portanto, certifique-se de que os seus métodos do controlador estão `async` conforme adequado e que está a `await` chamadas de método e não a `Wait` nas mesmas.</span><span class="sxs-lookup"><span data-stu-id="a4ad1-109">In the Azure Storage SDK for .NET Core, all methods that require network activity return `Task`s, so make sure your controller methods are `async` as appropriate and that you are `await`ing method calls and not `Wait`ing on them.</span></span>

<span data-ttu-id="a4ad1-110">Uma recomendação comum ao trabalhar com objetos de dados de grandes dimensões é utilizar fluxos em vez de estruturas na memória, como matrizes de bytes ou cadeias de carateres.</span><span class="sxs-lookup"><span data-stu-id="a4ad1-110">A common recommendation when working with large data objects is to use streams instead of in-memory structures like byte arrays or strings.</span></span> <span data-ttu-id="a4ad1-111">Isso evita a colocação em memória intermédia do conteúdo completo na memória antes de o enviar para o destino.</span><span class="sxs-lookup"><span data-stu-id="a4ad1-111">This avoids buffering the full content in memory before sending it to the target.</span></span> <span data-ttu-id="a4ad1-112">O ASP.NET Core suporta a leitura e gravação de fluxos de solicitações e de respostas.</span><span class="sxs-lookup"><span data-stu-id="a4ad1-112">ASP.NET Core supports reading and writing streams from requests and responses.</span></span>

## <a name="concurrent-access"></a><span data-ttu-id="a4ad1-113">Acesso simultâneo</span><span class="sxs-lookup"><span data-stu-id="a4ad1-113">Concurrent access</span></span>

<span data-ttu-id="a4ad1-114">É possível que os outros processos podem adicionar, alterar ou eliminar blobs à medida que a nossa aplicação as utiliza.</span><span class="sxs-lookup"><span data-stu-id="a4ad1-114">It is possible that other processes may be adding, changing, or deleting blobs as your app is using them.</span></span> <span data-ttu-id="a4ad1-115">Programe de forma defensiva e pense nos problemas potencialmente causados pela simultaneidade, como blobs eliminados logo a seguir a tentar transferi-los ou blobs cujos conteúdos mudam quando não espera.</span><span class="sxs-lookup"><span data-stu-id="a4ad1-115">Always code defensively and think about problems caused by concurrency, such as blobs that are deleted right as you try to download from them, or blobs whose contents change when you don't expect them to.</span></span> <span data-ttu-id="a4ad1-116">Veja a secção de Recursos Adicionais no fim deste módulo para mais informações sobre as AccessConditions e concessões de blobs para gerir o acesso simultâneo de blobs.</span><span class="sxs-lookup"><span data-stu-id="a4ad1-116">See the Additional Resources section at the end of this module for information about using AccessConditions and blob leases to manage concurrent blob access.</span></span>

## <a name="exercise"></a><span data-ttu-id="a4ad1-117">Exercício</span><span class="sxs-lookup"><span data-stu-id="a4ad1-117">Exercise</span></span>

<span data-ttu-id="a4ad1-118">Vamos terminar a nossa aplicação ao adicionar código de carregamento e transferência e, então, implementar no Serviço de Aplicações do Azure para efeitos de teste.</span><span class="sxs-lookup"><span data-stu-id="a4ad1-118">Let's finish our app by adding upload and download code, then deploy it to Azure App Service for testing.</span></span>

### <a name="upload"></a><span data-ttu-id="a4ad1-119">Carregar</span><span class="sxs-lookup"><span data-stu-id="a4ad1-119">Upload</span></span>

<span data-ttu-id="a4ad1-120">Para carregar um blob, vamos implementar o método `BlobStorage.Save` ao utilizar `GetBlockBlobReference` para obter `CloudBlockBlob` do contentor.</span><span class="sxs-lookup"><span data-stu-id="a4ad1-120">To upload a blob, we'll implement the `BlobStorage.Save` method using `GetBlockBlobReference` to get a `CloudBlockBlob` from the container.</span></span> <span data-ttu-id="a4ad1-121">`FilesController.Upload` passa a transmissão de ficheiros para `Save`, para podermos utilizar `UploadFromStreamAsync` para realizar o carregamento e maximizar a eficiência.</span><span class="sxs-lookup"><span data-stu-id="a4ad1-121">`FilesController.Upload` passes the file stream to `Save`, so we can use `UploadFromStreamAsync` to perform the upload for maximum efficiency.</span></span>

<span data-ttu-id="a4ad1-122">Abra o `BlobStorage.cs` no editor e preencha `Save` na implementação com o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="a4ad1-122">Open `BlobStorage.cs` in the editor and fill in the `Save` implementation with the following code:</span></span>

```csharp
public Task Save(Stream fileStream, string name)
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    CloudBlockBlob blockBlob = container.GetBlockBlobReference(name);
    return blockBlob.UploadFromStreamAsync(fileStream);
}
```

> [!NOTE]
> <span data-ttu-id="a4ad1-123">O código de carregamento com base na transmissão que aparece aqui é mais eficiente que ler o ficheiro numa matriz de bytes antes de enviar para o armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="a4ad1-123">The stream-based upload code shown here is more efficient than reading the file into a byte array before sending it to Azure Blob storage.</span></span> <span data-ttu-id="a4ad1-124">No entanto, a técnica `IFormFile` que utilizamos para obter o ficheiro do cliente não é uma implementação de transmissão verdadeira de ponta a ponta, sendo apenas adequada para processar carregamentos de ficheiros pequenos.</span><span class="sxs-lookup"><span data-stu-id="a4ad1-124">However, the `IFormFile` technique we use to get the file from the client is not a true end-to-end streaming implementation and is only appropriate for handling uploads of small files.</span></span> <span data-ttu-id="a4ad1-125">Veja a secção Recursos Adicionais no final deste módulo para obter informações sobre regras o carregamento de ficheiros completamente transmitidos.</span><span class="sxs-lookup"><span data-stu-id="a4ad1-125">See the Additional Resources section at the end of this module for information about fully streamed file uploads.</span></span>

### <a name="download"></a><span data-ttu-id="a4ad1-126">Transferência</span><span class="sxs-lookup"><span data-stu-id="a4ad1-126">Download</span></span>

<span data-ttu-id="a4ad1-127">`BlobStorage.Load` devolve um `Stream`, que significa que o nosso código não precisa de mover fisicamente os bytes de armazenamento dos Blobs em todos os &mdash;, apenas precisamos de devolver uma referência ao fluxo de blobs.</span><span class="sxs-lookup"><span data-stu-id="a4ad1-127">`BlobStorage.Load` returns a `Stream`, meaning that our code doesn't need to physically move the bytes from Blob storage at all &mdash; we just need to return a reference to the blob stream.</span></span> <span data-ttu-id="a4ad1-128">Pode fazê-lo com `OpenReadAsync`.</span><span class="sxs-lookup"><span data-stu-id="a4ad1-128">We can do that with `OpenReadAsync`.</span></span> <span data-ttu-id="a4ad1-129">O ASP.NET Core vai processar a leitura e fechar o fluxo quando ele cria a resposta do cliente.</span><span class="sxs-lookup"><span data-stu-id="a4ad1-129">ASP.NET Core will handle reading and closing the stream when it builds the client response.</span></span>

<span data-ttu-id="a4ad1-130">Preencha `Load` com este código:</span><span class="sxs-lookup"><span data-stu-id="a4ad1-130">Fill in `Load` with this code:</span></span>

```csharp
public Task<Stream> Load(string name)
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    return container.GetBlobReference(name).OpenReadAsync();
}
```

### <a name="deploy-and-run-in-azure"></a><span data-ttu-id="a4ad1-131">Publicar e executar no Azure</span><span class="sxs-lookup"><span data-stu-id="a4ad1-131">Deploy and run in Azure</span></span>

<span data-ttu-id="a4ad1-132">A nossa aplicação está terminada &mdash; vamos implementá-la e ver como funciona.</span><span class="sxs-lookup"><span data-stu-id="a4ad1-132">Our app is finished &mdash; let's deploy it and see it work.</span></span> <span data-ttu-id="a4ad1-133">Execute o seguinte código no terminal do Azure Cloud Shell para criar o nosso código e implementá-lo numa nova instância do Serviço de Aplicações.</span><span class="sxs-lookup"><span data-stu-id="a4ad1-133">Run the following code in the Azure Cloud Shell terminal to build our code and deploy it to a new App Service instance.</span></span> <span data-ttu-id="a4ad1-134">Também podemos adicionar a nossa cadeia de ligação de conta de armazenamento para configuração.</span><span class="sxs-lookup"><span data-stu-id="a4ad1-134">We also add our storage account connection string to configuration.</span></span>

```console

```

<span data-ttu-id="a4ad1-135">...</span><span class="sxs-lookup"><span data-stu-id="a4ad1-135">...</span></span>

<span data-ttu-id="a4ad1-136">Carregue e transfira alguns dos ficheiros para testar a aplicação, então execute o seguinte no shell para ver os blobs que foram carregados:</span><span class="sxs-lookup"><span data-stu-id="a4ad1-136">Upload and download some files to test the app, then run the following in the shell to see the blobs that have been uploaded:</span></span>

```console

```

<span data-ttu-id="a4ad1-137">**Imagem LISTA DE TAREFAS do portal**</span><span class="sxs-lookup"><span data-stu-id="a4ad1-137">**TODO pic from portal**</span></span>