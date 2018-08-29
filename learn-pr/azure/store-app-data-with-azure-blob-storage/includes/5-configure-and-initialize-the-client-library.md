<span data-ttu-id="f9126-101">Segue-se o fluxo de trabalho típico para as aplicações que utilizam o armazenamento de Blobs do Azure:</span><span class="sxs-lookup"><span data-stu-id="f9126-101">The following is the typical workflow for apps that use Azure Blob storage:</span></span>

1. <span data-ttu-id="f9126-102">**Obter configuração**: No arranque, carregue a configuração, como a cadeia de ligação com a chave de conta.</span><span class="sxs-lookup"><span data-stu-id="f9126-102">**Retrieve configuration**: At startup, load the configuration, such as the connection string with the account key.</span></span> <span data-ttu-id="f9126-103">Isto é preciso para autenticar as chamadas à API.</span><span class="sxs-lookup"><span data-stu-id="f9126-103">This is needed to authenticate API calls.</span></span>
1. <span data-ttu-id="f9126-104">**Inicializar o cliente**: Utilize a cadeia de ligação para inicializar a biblioteca de cliente de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f9126-104">**Initialize client**: Use the connection string to initialize the Azure Storage client library.</span></span> <span data-ttu-id="f9126-105">Esta ação cria os objetos que a aplicação irá utilizar para trabalhar com a API de Armazenamento de blobs.</span><span class="sxs-lookup"><span data-stu-id="f9126-105">This creates the objects the app will use to work with the Blob storage API.</span></span>
1. <span data-ttu-id="f9126-106">**Utilizar**: Faça chamadas à API com a biblioteca de cliente para operar em contentores e blobs.</span><span class="sxs-lookup"><span data-stu-id="f9126-106">**Use**: Make API calls with the client library to operate on containers and blobs.</span></span>

## <a name="configure-your-connection-string"></a><span data-ttu-id="f9126-107">Configurar a cadeia de ligação</span><span class="sxs-lookup"><span data-stu-id="f9126-107">Configure your connection string</span></span>

<span data-ttu-id="f9126-108">Antes de escrever qualquer código, irá precisar da cadeia de ligação para a conta de armazenamento que irá utilizar.</span><span class="sxs-lookup"><span data-stu-id="f9126-108">Before writing any code, you'll need the connection string for the storage account you will use.</span></span> 

<span data-ttu-id="f9126-109">A cadeia de ligação inclui a sua chave de conta.</span><span class="sxs-lookup"><span data-stu-id="f9126-109">The connection string includes your account key.</span></span> <span data-ttu-id="f9126-110">A chave da conta é considerada um segredo e deve ser armazenada em segurança.</span><span class="sxs-lookup"><span data-stu-id="f9126-110">The account key is considered a secret and should be stored securely.</span></span> <span data-ttu-id="f9126-111">Iremos armazenar a cadeia de ligação numa definição de aplicação do Serviço de Aplicações.</span><span class="sxs-lookup"><span data-stu-id="f9126-111">We will store the connection string in an App Service application setting.</span></span> <span data-ttu-id="f9126-112">Uma definição da aplicação é um local seguro para segredos da aplicação, mas não suporta o desenvolvimento local e não é uma solução robusta de ponto a ponto por conta própria.</span><span class="sxs-lookup"><span data-stu-id="f9126-112">An application setting is a secure place for application secrets, but it does not support local development and is not a robust, end-to-end solution on its own.</span></span>

> [!WARNING]
> <span data-ttu-id="f9126-113">**Não coloque as chaves da conta de armazenamento no código ou nos ficheiros de configuração não protegidos.**</span><span class="sxs-lookup"><span data-stu-id="f9126-113">**Do not place storage account keys in code or in unprotected configuration files.**</span></span> <span data-ttu-id="f9126-114">As chaves de conta de armazenamento permitem acesso total à sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f9126-114">Storage account keys enable full access to your storage account.</span></span> <span data-ttu-id="f9126-115">A fuga de uma chave pode resultar em danos irrecuperáveis e faturas altas.</span><span class="sxs-lookup"><span data-stu-id="f9126-115">Leaking a key can result in unrecoverable damage and large bills.</span></span> <span data-ttu-id="f9126-116">Veja a secção Recursos Adicionais no final deste módulo para obter documentação de orientação de armazenamento e conselhos sobre como recuperar de uma chave perdida.</span><span class="sxs-lookup"><span data-stu-id="f9126-116">See the Additional Resources section at the end of this module for storage guidance and advice about how to recover from a leaked key.</span></span>

## <a name="initialize-the-blob-storage-object-model"></a><span data-ttu-id="f9126-117">Inicializar o modelo de objeto de Armazenamento de blobs</span><span class="sxs-lookup"><span data-stu-id="f9126-117">Initialize the Blob storage object model</span></span>

<span data-ttu-id="f9126-118">No SDK de Armazenamento do Azure para .NET Core, o padrão habitual para utilizar o Armazenamento de blobs inclui os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="f9126-118">In the Azure Storage SDK for .NET Core, the standard pattern for using Blob storage consists of the following steps:</span></span>

1. <span data-ttu-id="f9126-119">Chame `CloudStorageAccount.Parse` (ou `TryParse`) com a sua cadeia de ligação para obter um `CloudStorageAccount`.</span><span class="sxs-lookup"><span data-stu-id="f9126-119">Call `CloudStorageAccount.Parse` (or `TryParse`) with your connection string to get a `CloudStorageAccount`.</span></span>
1. <span data-ttu-id="f9126-120">Chame `CreateCloudBlobClient` no `CloudStorageAccount` para obter um `CloudBlobClient`.</span><span class="sxs-lookup"><span data-stu-id="f9126-120">Call `CreateCloudBlobClient` on the `CloudStorageAccount` to get a `CloudBlobClient`.</span></span>
1. <span data-ttu-id="f9126-121">Chame `GetContainerReference` no `CloudBlobClient` para obter um `CloudBlobContainer`.</span><span class="sxs-lookup"><span data-stu-id="f9126-121">Call `GetContainerReference` on the `CloudBlobClient` to get a `CloudBlobContainer`.</span></span>
1. <span data-ttu-id="f9126-122">Utilize métodos no contentor para obter uma lista de blobs e/ou obter referências para blobs individuais para carregar e transferir dados.</span><span class="sxs-lookup"><span data-stu-id="f9126-122">Use methods on the container to get a list of blobs and/or get references to individual blobs to upload and download data.</span></span>

<span data-ttu-id="f9126-123">No código, os passos 1&ndash;3 são semelhantes ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="f9126-123">In code, steps 1&ndash;3 look like this:</span></span>

```csharp
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString); // or TryParse()
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference(containerName);
```

<span data-ttu-id="f9126-124">Nenhum deste código de inicialização faz chamadas através da rede.</span><span class="sxs-lookup"><span data-stu-id="f9126-124">None of this initialization code makes calls over the network.</span></span> <span data-ttu-id="f9126-125">O que significa que as exceções que ocorrem de informações incorretas não serão geradas mais tarde; por exemplo, a chamada para `GetContainerReference` terá êxito se o contentor existir, ou não, na conta.</span><span class="sxs-lookup"><span data-stu-id="f9126-125">This means exceptions that occur from incorrect information won't be thrown until later; for example, the call to `GetContainerReference` will succeed whether or not the container actually exists in the account.</span></span>

## <a name="create-containers-at-startup"></a><span data-ttu-id="f9126-126">Criar contentores no arranque</span><span class="sxs-lookup"><span data-stu-id="f9126-126">Create containers at startup</span></span>

<span data-ttu-id="f9126-127">É prática comum para aplicações criar contentores que são precisos no código, mesmo quando sabemos quais serão esses contentores antecipadamente.</span><span class="sxs-lookup"><span data-stu-id="f9126-127">Common practice is for applications to create needed containers in code, even when we know what those containers will be up-front.</span></span> <span data-ttu-id="f9126-128">Chamar `CreateIfNotExistsAsync` num `CloudBlobContainer` é a melhor forma de o fazer, e devemos utilizá-lo para criar cada contentor que sabemos que iremos precisar antes o utilizar.</span><span class="sxs-lookup"><span data-stu-id="f9126-128">Calling `CreateIfNotExistsAsync` on a `CloudBlobContainer` is the best way to do this, and we should use it to create each container we know we'll need before we use them.</span></span>

<span data-ttu-id="f9126-129">`CreateIfNotExistsAsync` *faz* uma chamada de rede para o Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f9126-129">`CreateIfNotExistsAsync` *does* make a network call to Azure Storage.</span></span> <span data-ttu-id="f9126-130">É melhor prática fazer uma chamada para o mesmo no arranque, e não sempre que acedemos a um contentor.</span><span class="sxs-lookup"><span data-stu-id="f9126-130">Best practice is to call it once at startup and not every time we access a container.</span></span>

## <a name="exercise"></a><span data-ttu-id="f9126-131">Exercício</span><span class="sxs-lookup"><span data-stu-id="f9126-131">Exercise</span></span>

### <a name="clone-and-explore-the-unfinished-app"></a><span data-ttu-id="f9126-132">Clonar e explorar a aplicação não terminada</span><span class="sxs-lookup"><span data-stu-id="f9126-132">Clone and explore the unfinished app</span></span>

<span data-ttu-id="f9126-133">Primeiro, vamos clonar a aplicação de arranque a partir do GitHub.</span><span class="sxs-lookup"><span data-stu-id="f9126-133">First, let's clone the starter app from GitHub.</span></span> <span data-ttu-id="f9126-134">No terminal do Cloud Shell, execute o seguinte comando para obter uma cópia do código fonte e abra-o no editor:</span><span class="sxs-lookup"><span data-stu-id="f9126-134">In the Cloud Shell terminal, run the following command to get a copy of the source code and open it in the editor:</span></span>

```console
git clone TODO
cd TODO
code .
```

<span data-ttu-id="f9126-135">Abra o ficheiro `Controllers/FilesController.cs`.</span><span class="sxs-lookup"><span data-stu-id="f9126-135">Open the file `Controllers/FilesController.cs`.</span></span>

<span data-ttu-id="f9126-136">Este controlador implementa uma API com três ações:</span><span class="sxs-lookup"><span data-stu-id="f9126-136">This controller implements an API with three actions:</span></span>

* <span data-ttu-id="f9126-137">**Indexar** (POST /api/Files) devolve uma lista de URLs, um para cada ficheiro que foi carregado.</span><span class="sxs-lookup"><span data-stu-id="f9126-137">**Index** (GET /api/Files) returns a list of URLs, one for each file that's been uploaded.</span></span> <span data-ttu-id="f9126-138">O front-end de aplicação chama este método para criar uma lista de hiperlinks para os ficheiros carregados.</span><span class="sxs-lookup"><span data-stu-id="f9126-138">The app front end calls this method to build a list of hyperlinks to the uploaded files.</span></span>
* <span data-ttu-id="f9126-139">**Carregar** (POST /api/Files) recebe um ficheiro carregado e guarda-o.</span><span class="sxs-lookup"><span data-stu-id="f9126-139">**Upload** (POST /api/Files) receives an uploaded file and saves it.</span></span>
* <span data-ttu-id="f9126-140">**Transferir** (GET /api/Files/{file-name}) transfere um ficheiro individual pelo seu nome.</span><span class="sxs-lookup"><span data-stu-id="f9126-140">**Download** (GET /api/Files/{file-name}) downloads an individual file by its name.</span></span>

<span data-ttu-id="f9126-141">Cada método utiliza uma instância `IStorage` chamada `storage` para realizar o seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="f9126-141">Each method uses an `IStorage` instance called `storage` to do its work.</span></span> <span data-ttu-id="f9126-142">Existe uma implementação incompleta de `IStorage` em `Models/BlobStorage.cs`.</span><span class="sxs-lookup"><span data-stu-id="f9126-142">There is an incomplete implementation of `IStorage` in  `Models/BlobStorage.cs`.</span></span>

### <a name="add-the-nuget-package"></a><span data-ttu-id="f9126-143">Adicionar o pacote NuGet</span><span class="sxs-lookup"><span data-stu-id="f9126-143">Add the NuGet package</span></span>

<span data-ttu-id="f9126-144">Primeiro, adicione uma referência ao SDK de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f9126-144">First, add a reference to the Azure Storage SDK.</span></span> <span data-ttu-id="f9126-145">No terminal, execute o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f9126-145">In the terminal, run the following:</span></span>

```console
dotnet add package WindowsAzure.Storage
dotnet restore
```

<span data-ttu-id="f9126-146">Isto irá garantir que estamos a utilizar a versão mais recente da biblioteca de clientes de Armazenamento de blobs.</span><span class="sxs-lookup"><span data-stu-id="f9126-146">This will make sure we're using the newest version of the Blob storage client library.</span></span>

### <a name="configure"></a><span data-ttu-id="f9126-147">Configurar</span><span class="sxs-lookup"><span data-stu-id="f9126-147">Configure</span></span>

<span data-ttu-id="f9126-148">A nossa aplicação de arranque já inclui a ligação de configuração que precisamos.</span><span class="sxs-lookup"><span data-stu-id="f9126-148">Our starter app already includes the configuration plumbing we need.</span></span> <span data-ttu-id="f9126-149">O parâmetro de construtor `IOptions<AzureStorageConfig>` no `BlobStorage` tem duas propriedades: a cadeia de ligação da conta de armazenamento e o nome do contentor em que a nossa aplicação irá armazenar os blobs.</span><span class="sxs-lookup"><span data-stu-id="f9126-149">The `IOptions<AzureStorageConfig>` constructor parameter in `BlobStorage` has two properties: the storage account connection string and the name of the container our app will store blobs in.</span></span> <span data-ttu-id="f9126-150">Existe código no método `ConfigureServices` de `Startup.cs` que carrega os valores da configuração quando a aplicação é iniciada.</span><span class="sxs-lookup"><span data-stu-id="f9126-150">There is code in the `ConfigureServices` method of `Startup.cs` that loads the values from configuration when the app starts.</span></span>

<span data-ttu-id="f9126-151">Neste exercício, iremos executar a aplicação no Serviço de Aplicações do Azure, pelo que iremos adicionar mais tarde os valores de configuração nas definições de aplicação do Serviço de Aplicações.</span><span class="sxs-lookup"><span data-stu-id="f9126-151">In this exercise, we will run the app in Azure App Service, so we will add the configuration values to the App Service application settings later.</span></span> <span data-ttu-id="f9126-152">Por enquanto, não precisamos de realizar qualquer ação relacionada com a configuração.</span><span class="sxs-lookup"><span data-stu-id="f9126-152">For now, we don't need to do any work related to configuration.</span></span>

### <a name="initialize"></a><span data-ttu-id="f9126-153">Inicializar</span><span class="sxs-lookup"><span data-stu-id="f9126-153">Initialize</span></span>

<span data-ttu-id="f9126-154">Abra `BlobStorage.cs`.</span><span class="sxs-lookup"><span data-stu-id="f9126-154">Open `BlobStorage.cs`.</span></span>

<span data-ttu-id="f9126-155">Localização do método `Initialize`.</span><span class="sxs-lookup"><span data-stu-id="f9126-155">Location the `Initialize` method.</span></span> <span data-ttu-id="f9126-156">A nossa aplicação irá chamar este método quando for utilizado pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="f9126-156">Our app will call this method when it's first used.</span></span> <span data-ttu-id="f9126-157">Se estiver curioso, pode dar uma vista de olhos em `ConfigureServices` em `Startup.cs` para ver como isto é feito.</span><span class="sxs-lookup"><span data-stu-id="f9126-157">If you're curious, you can look at `ConfigureServices` in `Startup.cs` to see how this is done.</span></span> 

<span data-ttu-id="f9126-158">`Initialize` é onde queremos criar o nosso contentor se ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="f9126-158">`Initialize` is where we want to create our container if it doesn't already exist.</span></span> <span data-ttu-id="f9126-159">Preencha `Initialize` com o código seguinte e guarde o seu trabalho:</span><span class="sxs-lookup"><span data-stu-id="f9126-159">Fill in `Initialize` with the following code and save your work:</span></span>

```csharp
public Task Initialize()
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    return container.CreateIfNotExistsAsync();
}
```