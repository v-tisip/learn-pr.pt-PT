<span data-ttu-id="eec7c-101">Neste módulo, aprendeu como utilizar o Armazenamento de blobs do Azure para armazenar dados da aplicação Web.</span><span class="sxs-lookup"><span data-stu-id="eec7c-101">In this module, you learned how to use Azure Blob storage to store web application data.</span></span> <span data-ttu-id="eec7c-102">Apresentámos sugestões para criar uma estratégia para utilizar o Armazenamento de blobs numa aplicação Web e como utilizar o SDK do Armazenamento do Azure para .NET Core para gravar e ler a partir de blobs.</span><span class="sxs-lookup"><span data-stu-id="eec7c-102">We discussed tips for creating a strategy to use Blob storage in a web app and how to use the Azure Storage SDK for .NET Core to write to and read from blobs.</span></span> <span data-ttu-id="eec7c-103">A aplicação criada aceita os ficheiros carregados pelos utilizadores, armazena-os no Armazenamento de blobs e disponibiliza-os para transferência.</span><span class="sxs-lookup"><span data-stu-id="eec7c-103">The app we made accepts uploaded files from users, stores them in Blob storage, and makes them available for download.</span></span>

## <a name="cleanup"></a><span data-ttu-id="eec7c-104">Limpeza</span><span class="sxs-lookup"><span data-stu-id="eec7c-104">Cleanup</span></span>

<span data-ttu-id="eec7c-105">Para limpar a subscrição do Azure, execute o seguinte no Azure Cloud Shell para eliminar o grupo de recursos que contém todos os recursos criados neste módulo.</span><span class="sxs-lookup"><span data-stu-id="eec7c-105">To clean up your Azure subscription, run the following in Azure Cloud Shell to delete the resource group containing all the resources we created in this module.</span></span>

```console
az group delete --name blob-exercise-group
```

<span data-ttu-id="eec7c-106">Para limpar o armazenamento do Cloud Shell, elimine o diretório `TODO` com `rm -rf TODO`.</span><span class="sxs-lookup"><span data-stu-id="eec7c-106">To clean up your Cloud Shell storage, delete the `TODO` directory with `rm -rf TODO`.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="eec7c-107">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="eec7c-107">Additional resources</span></span>

<span data-ttu-id="eec7c-108">**Ligações cross-docset TODO?**</span><span class="sxs-lookup"><span data-stu-id="eec7c-108">**TODO cross-docset links?**</span></span>

* <span data-ttu-id="eec7c-109">**Armazenar as chaves da conta de armazenamento de forma segura**: o Azure Key Vault é a solução ponto a ponto mais robusta para armazenar os valores de configuração secretos.</span><span class="sxs-lookup"><span data-stu-id="eec7c-109">**Securely storing storage account keys**: The most robust end-to-end solution for storing secret configuration values is Azure Key Vault.</span></span> <span data-ttu-id="eec7c-110">Veja [aqui](https://docs.microsoft.com/aspnet/core/security/key-vault-configuration?view=aspnetcore-2.1&tabs=aspnetcore2x) para obter informações sobre como utilizar o Key Vault numa aplicação ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="eec7c-110">See [here](https://docs.microsoft.com/aspnet/core/security/key-vault-configuration?view=aspnetcore-2.1&tabs=aspnetcore2x) for information about using Key Vault in an ASP.NET Core application.</span></span> <span data-ttu-id="eec7c-111">Em alternativa, pode armazenar com segurança cadeias de ligação nas definições de aplicação do Serviço de Aplicações e utilizar a [ferramenta Secret Manager do ASP.NET Core](https://docs.microsoft.com/aspnet/core/security/app-secrets?view=aspnetcore-2.1&tabs=windows) para suportar ambientes de programação.</span><span class="sxs-lookup"><span data-stu-id="eec7c-111">Alternatively, you can safely store connection strings in App Service application settings and use the [ASP.NET Core Secret Manager tool](https://docs.microsoft.com/aspnet/core/security/app-secrets?view=aspnetcore-2.1&tabs=windows) to support developer environments.</span></span>
* [<span data-ttu-id="eec7c-112">Carregar ficheiros grandes com transmissão em fluxo no ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="eec7c-112">Uploading large files with streaming in ASP.NET Core</span></span>](https://docs.microsoft.com/aspnet/core/mvc/models/file-uploads?view=aspnetcore-2.1#uploading-large-files-with-streaming)
* [<span data-ttu-id="eec7c-113">Simultaneidade de blobs: AccessConditions e concessões de blobs</span><span class="sxs-lookup"><span data-stu-id="eec7c-113">Blob concurrency: AccessConditions and blob leases</span></span>](https://azure.microsoft.com/blog/managing-concurrency-in-microsoft-azure-storage-2/)
* [<span data-ttu-id="eec7c-114">Conceder acesso limitado ao objeto do Armazenamento do Azure com assinaturas de acesso partilhado</span><span class="sxs-lookup"><span data-stu-id="eec7c-114">Granting limited access to Azure Storage object with shared access signatures</span></span>](https://docs.microsoft.com/azure/storage/common/storage-dotnet-shared-access-signature-part-1)
* [<span data-ttu-id="eec7c-115">Indexar o Armazenamento de blobs com o Azure Search</span><span class="sxs-lookup"><span data-stu-id="eec7c-115">Indexing Blob storage with Azure Search</span></span>](https://docs.microsoft.com/azure/search/search-howto-indexing-azure-blob-storage)
* [<span data-ttu-id="eec7c-116">Restrições de nome de contentor e de blob</span><span class="sxs-lookup"><span data-stu-id="eec7c-116">Container and blob name restrictions</span></span>](https://docs.microsoft.com/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata#resource-names)