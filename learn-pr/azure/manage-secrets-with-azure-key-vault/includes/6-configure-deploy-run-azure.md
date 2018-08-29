<span data-ttu-id="8ad3c-101">Agora está na altura de executar a nossa aplicação no Azure.</span><span class="sxs-lookup"><span data-stu-id="8ad3c-101">Now it's time to run our app in Azure.</span></span> <span data-ttu-id="8ad3c-102">Precisamos de criar uma aplicação do Serviço de Aplicações do Azure, configurá-la com um MSI e com a nossa configuração do cofre, e implementar o nosso código.</span><span class="sxs-lookup"><span data-stu-id="8ad3c-102">We need to create an Azure App Service app, set it up with MSI and our vault configuration, and deploy our code.</span></span>

## <a name="exercise"></a><span data-ttu-id="8ad3c-103">Exercício</span><span class="sxs-lookup"><span data-stu-id="8ad3c-103">Exercise</span></span>

### <a name="create-the-app-service-plan-and-app"></a><span data-ttu-id="8ad3c-104">Criar a aplicação e o plano do Serviço de Aplicações</span><span class="sxs-lookup"><span data-stu-id="8ad3c-104">Create the App Service plan and app</span></span>

<span data-ttu-id="8ad3c-105">Criar uma aplicação do Serviço de Aplicações é um processo de dois passos: primeiro, crie o *plano*, depois a *aplicação*.</span><span class="sxs-lookup"><span data-stu-id="8ad3c-105">Creating an App Service app is a two-step process: First create the *plan*, then the *app*.</span></span>

<span data-ttu-id="8ad3c-106">O nome do *plano* só precisa de ser exclusivo na sua subscrição, por isso pode utilizar o mesmo nome que utilizámos: **keyvault-exercise-plan**.</span><span class="sxs-lookup"><span data-stu-id="8ad3c-106">The *plan* name only needs to be unique within your subscription, so you can use the same name we've used: **keyvault-exercise-plan**.</span></span> <span data-ttu-id="8ad3c-107">No entanto, o nome da aplicação terá de ser globalmente exclusivo, por isso terá de escolher o seu.</span><span class="sxs-lookup"><span data-stu-id="8ad3c-107">The app name needs to be globally unique, though, so you'll need to pick your own.</span></span>

<span data-ttu-id="8ad3c-108">No Azure Cloud Shell, execute o seguinte:</span><span class="sxs-lookup"><span data-stu-id="8ad3c-108">In Azure Cloud Shell, run the following:</span></span>

```azurecli
az appservice plan create --name keyvault-exercise-plan --resource-group keyvault-exercise-group
az webapp create --name <your-unique-app-name> --plan keyvault-exercise-plan --resource-group keyvault-exercise-group
```

### <a name="add-configuration-to-the-app"></a><span data-ttu-id="8ad3c-109">Adicionar configuração à aplicação</span><span class="sxs-lookup"><span data-stu-id="8ad3c-109">Add configuration to the app</span></span>

<span data-ttu-id="8ad3c-110">Para implementar no Azure, vamos seguir a prática recomendada do Serviço de Aplicações de colocar a configuração nas Definições de Aplicações em vez de num ficheiro de configuração.</span><span class="sxs-lookup"><span data-stu-id="8ad3c-110">For deploying to Azure, we'll follow the App Service best practice of putting configuration in Application Settings instead of a configuration file.</span></span>

```azurecli
az webapp config appsettings set --name <your-unique-app-name> --resource-group keyvault-exercise-group --settings VaultName=<your-unique-vault-name>
```

### <a name="enable-msi"></a><span data-ttu-id="8ad3c-111">Ativar MSI</span><span class="sxs-lookup"><span data-stu-id="8ad3c-111">Enable MSI</span></span>

<span data-ttu-id="8ad3c-112">Ativar o MSI numa aplicação é um processo simples:</span><span class="sxs-lookup"><span data-stu-id="8ad3c-112">Enabling MSI on an app is a one-liner:</span></span>

```azurecli
az webapp identity assign --name <your-unique-app-name> --resource-group keyvault-exercise-group
```

<span data-ttu-id="8ad3c-113">No resultado JSON, copie o valor **principalId**.</span><span class="sxs-lookup"><span data-stu-id="8ad3c-113">From the JSON output that results, copy the **principalId** value.</span></span> <span data-ttu-id="8ad3c-114">O PrincipalId é o ID exclusivo da nova identidade da aplicação no Azure Active Directory e vamos utilizá-lo no próximo passo.</span><span class="sxs-lookup"><span data-stu-id="8ad3c-114">PrincipalId is the unique ID of the app's new identity in Azure Active Directory, and we're going to use it in the next step.</span></span>

### <a name="grant-access-to-the-vault"></a><span data-ttu-id="8ad3c-115">Conceder acesso ao cofre</span><span class="sxs-lookup"><span data-stu-id="8ad3c-115">Grant access to the vault</span></span>

<span data-ttu-id="8ad3c-116">Agora, precisa de dar à sua aplicação permissões de identidade para obter e listar segredos do seu cofre de ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="8ad3c-116">Now you need to give your app identity permissions to get and list secrets from your production-environment vault.</span></span> <span data-ttu-id="8ad3c-117">Utilize o valor **principalId** que copiou no passo anterior como o valor para **object-id** no comando abaixo.</span><span class="sxs-lookup"><span data-stu-id="8ad3c-117">Use the **principalId** value you copied from the previous step as the value for **object-id** in the command below.</span></span>

```azurecli
az keyvault set-policy --name <your-unique-vault-name> --object-id <your-msi-principleid> --secret-permissions get list
```

### <a name="deploy-the-app-and-try-it-out"></a><span data-ttu-id="8ad3c-118">Implementar e experimentar a aplicação</span><span class="sxs-lookup"><span data-stu-id="8ad3c-118">Deploy the app and try it out</span></span>

<span data-ttu-id="8ad3c-119">A sua configuração foi definida e está tudo pronto para implementar!</span><span class="sxs-lookup"><span data-stu-id="8ad3c-119">All your configuration is set and you're ready to deploy!</span></span> <span data-ttu-id="8ad3c-120">Os comandos abaixo irão publicar o site na pasta `pub`, zipá-la para o ficheiro `site.zip` e implementar o zip no Serviço de Aplicações.</span><span class="sxs-lookup"><span data-stu-id="8ad3c-120">The below commands will publish the site to the `pub` folder, zip it up into `site.zip`, and deploy the zip to App Service.</span></span>

> [!NOTE]
> <span data-ttu-id="8ad3c-121">Terá de utilizar o comando `cd` para regressar ao diretório KeyVaultDemoApp, caso ainda não o tenha feito.</span><span class="sxs-lookup"><span data-stu-id="8ad3c-121">You'll need to `cd` back to the KeyVaultDemoApp directory if you haven't already.</span></span>

```console
dotnet publish -o pub
zip -j site.zip pub/*
az webapp deployment source config-zip --src site.zip --name <your-unique-app-name> --resource-group keyvault-exercise-group
```

<span data-ttu-id="8ad3c-122">Depois de obter um resultado que indique que o site foi implementado, abra `https://<your-unique-app-name>.azurewebsites.net/api/SecretTest` num browser.</span><span class="sxs-lookup"><span data-stu-id="8ad3c-122">Once you get a result that indicates the site has deployed, open `https://<your-unique-app-name>.azurewebsites.net/api/SecretTest` in a browser.</span></span> <span data-ttu-id="8ad3c-123">Deverá ver o valor de segredo, **reindeer_flotilla**.</span><span class="sxs-lookup"><span data-stu-id="8ad3c-123">You should see the secret value, **reindeer_flotilla**.</span></span>

<span data-ttu-id="8ad3c-124">A sua aplicação está concluída e implementada!</span><span class="sxs-lookup"><span data-stu-id="8ad3c-124">Your app is finished and deployed!</span></span>