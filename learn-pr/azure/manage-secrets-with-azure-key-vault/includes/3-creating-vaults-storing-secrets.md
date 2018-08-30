## <a name="creating-key-vaults-for-your-applications"></a><span data-ttu-id="28fa9-101">Criar Cofres de Chaves para as suas aplicações</span><span class="sxs-lookup"><span data-stu-id="28fa9-101">Creating Key Vaults for your applications</span></span>

<span data-ttu-id="28fa9-102">Uma prática recomendada é atribuir a cada aplicação um cofre separado para cada ambiente de implementação que utilizar, como, por exemplo, desenvolvimento, teste e produção.</span><span class="sxs-lookup"><span data-stu-id="28fa9-102">Good practice is to give each application a separate vault for each deployment environment you use, such as development, test, and production.</span></span> <span data-ttu-id="28fa9-103">Ainda que lhe seja conveniente partilhar segredos entre as várias aplicações, lembre-se que o risco de um atacante obter acesso de leitura a um cofre aumenta com o número de segredos no cofre.</span><span class="sxs-lookup"><span data-stu-id="28fa9-103">It may be convenient to share secrets across apps, but the impact of an attacker gaining read access to a vault increases with the number of secrets in the vault.</span></span>

> [!TIP]
> <span data-ttu-id="28fa9-104">Se utilizar os mesmos nomes para segredos entre os diferentes ambientes, a única configuração específica do ambiente que tem de ser alterada na aplicação é o URL do cofre.</span><span class="sxs-lookup"><span data-stu-id="28fa9-104">If you use the same names for secrets across different environments, the only environment-specific configuration that has to change in your app is the vault URL.</span></span>

<span data-ttu-id="28fa9-105">Criar um cofre não requer qualquer configuração inicial.</span><span class="sxs-lookup"><span data-stu-id="28fa9-105">Creating a vault requires no initial configuration.</span></span> <span data-ttu-id="28fa9-106">À sua identidade de utilizador é automaticamente concedido o conjunto completo de permissões de gestão de segredos e pode começar a adicionar segredos imediatamente.</span><span class="sxs-lookup"><span data-stu-id="28fa9-106">Your user identity is automatically granted the full set of secret management permissions and you can start adding secrets immediately.</span></span> <span data-ttu-id="28fa9-107">Assim que tiver um cofre, pode adicionar e gerir segredos a partir de qualquer interface administrativa do Azure, incluindo o portal do Azure, a CLI do Azure e o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="28fa9-107">Once you have a vault, adding and managing secrets can be done from any Azure administrative interface, including the Azure portal, the Azure CLI, and Azure PowerShell.</span></span> <span data-ttu-id="28fa9-108">Quando configurar a sua aplicação para utilizar o cofre, terá de atribuir as permissões corretas para-lo. Vamos ver isto na unidade seguinte.</span><span class="sxs-lookup"><span data-stu-id="28fa9-108">When you set up your application to use the vault, you'll need to assign the correct permissions to it; we'll see that in the next unit.</span></span>

## <a name="vault-authentication-and-permissions"></a><span data-ttu-id="28fa9-109">Permissões e autenticação do cofre</span><span class="sxs-lookup"><span data-stu-id="28fa9-109">Vault authentication and permissions</span></span>

<span data-ttu-id="28fa9-110">A API do Azure Key Vault utiliza o Azure Active Directory para autenticar utilizadores e aplicações.</span><span class="sxs-lookup"><span data-stu-id="28fa9-110">Azure Key Vault's API uses Azure Active Directory to authenticate users and applications.</span></span> <span data-ttu-id="28fa9-111">As políticas de acesso ao cofre baseiam-se em *ações* e são aplicadas à totalidade do cofre.</span><span class="sxs-lookup"><span data-stu-id="28fa9-111">Vault access policies are based on *actions*, and are applied across an entire vault.</span></span> <span data-ttu-id="28fa9-112">Por exemplo, numa aplicação com as permissões **Obter** (ler valores secretos), **Listar** (listar nomes de todos os segredos), e **Definir** (criar ou atualizar valores secretos) para um cofre, é possível criar segredos, listar todos os nomes de segredos e obter e definir todos os valores dos segredos nesse cofre.</span><span class="sxs-lookup"><span data-stu-id="28fa9-112">For example, an application with **Get** (read secret values), **List** (list names of all secrets), and **Set** (create or update secret values) permissions to a vault is able to create secrets, list all secret names, and get and set all secret values in that vault.</span></span>

<span data-ttu-id="28fa9-113">*Todas* as ações realizadas num cofre requerem autenticação e autorização &mdash; não é possível conceder qualquer tipo de acesso anónimo.</span><span class="sxs-lookup"><span data-stu-id="28fa9-113">*All* actions performed on a vault require authentication and authorization &mdash; there is no way to grant any kind of anonymous access.</span></span>

> [!TIP]
> <span data-ttu-id="28fa9-114">Ao conceder acesso ao cofre a programadores e aplicações, conceda apenas o conjunto mínimo de permissões necessárias.</span><span class="sxs-lookup"><span data-stu-id="28fa9-114">When granting vault access to developers and apps, grant only the minimum set of permissions needed.</span></span> <span data-ttu-id="28fa9-115">As restrições de permissões ajudam a evitar acidentes provocados por erros de código e a reduzir o risco de credenciais roubadas ou código malicioso injetado na sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="28fa9-115">Permissions restrictions help avoid accidents caused by code bugs and reduce the impact of stolen credentials or malicious code injected into your app.</span></span>

<span data-ttu-id="28fa9-116">Regra geral, os programadores necessitam apenas das permissões **Obter** e **Listar** para um cofre de ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="28fa9-116">Developers will usually only need **Get** and **List** permissions to a development-environment vault.</span></span> <span data-ttu-id="28fa9-117">Um programador chefe ou sénior necessitará de todas as permissões do cofre, para poder alterar e adicionar segredos sempre que necessário.</span><span class="sxs-lookup"><span data-stu-id="28fa9-117">A lead or senior developer will need full permissions to the vault to change and add secrets when necessary.</span></span> <span data-ttu-id="28fa9-118">Por norma, todas as permissões para os cofres de ambiente de produção estão reservadas para técnicos operacionais séniores.</span><span class="sxs-lookup"><span data-stu-id="28fa9-118">Full permissions to production-environment vaults are typically reserved for senior operations staff.</span></span>

<span data-ttu-id="28fa9-119">No caso das aplicações, apenas as permissões **Obter** são, normalmente, necessárias.</span><span class="sxs-lookup"><span data-stu-id="28fa9-119">For apps, typically only **Get** permissions are required.</span></span> <span data-ttu-id="28fa9-120">Algumas aplicações podem exigir permissões **Listar**, dependendo da forma como a aplicação for implementada.</span><span class="sxs-lookup"><span data-stu-id="28fa9-120">Some apps may require **List** depending on the way the app is implemented.</span></span> <span data-ttu-id="28fa9-121">A aplicação que vamos implementar no exercício deste módulo precisa da permissão **Listar**, devido à técnica utilizada para ler os segredos do cofre.</span><span class="sxs-lookup"><span data-stu-id="28fa9-121">The app we'll implement in this module's exercise requires the **List** permission because of the technique it uses to read secrets from the vault.</span></span>

## <a name="exercise"></a><span data-ttu-id="28fa9-122">Exercício</span><span class="sxs-lookup"><span data-stu-id="28fa9-122">Exercise</span></span>

<span data-ttu-id="28fa9-123">Tendo em conta todos os problemas que a empresa tem tido com os segredos da aplicação, a direção pediu-lhe para criar uma pequena aplicação de arranque para que os outros programadores possam seguir no caminho certo.</span><span class="sxs-lookup"><span data-stu-id="28fa9-123">Given all the trouble the company's been having with application secrets, management has asked you to create a small starter app to set the other developers on the right path.</span></span> <span data-ttu-id="28fa9-124">A aplicação precisa de mostrar as melhores práticas para a gestão de segredos, da forma mais simples e mais segura possível.</span><span class="sxs-lookup"><span data-stu-id="28fa9-124">The app needs to demonstrate best practices for managing secrets as simply and securely as possible.</span></span>

<span data-ttu-id="28fa9-125">Para começar, vai criar um cofre e armazenar um segredo.</span><span class="sxs-lookup"><span data-stu-id="28fa9-125">To start, you'll create a vault and store one secret.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="28fa9-126">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="28fa9-126">Create a resource group</span></span>

<span data-ttu-id="28fa9-127">Crie um grupo de recursos com o nome `keyvault-exercise-group` para todos os recursos neste exercício.</span><span class="sxs-lookup"><span data-stu-id="28fa9-127">Create a resource group called `keyvault-exercise-group` for all of the resources in this exercise.</span></span> <span data-ttu-id="28fa9-128">No final deste módulo, este grupo de recursos será eliminado para limpar tudo ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="28fa9-128">At the end of this module, we'll be deleting this resource group to clean up everything at once.</span></span> <span data-ttu-id="28fa9-129">Vamos utilizar `eastus` como a localização para tudo neste exercício.</span><span class="sxs-lookup"><span data-stu-id="28fa9-129">We'll use `eastus` as the location for everything in this exercise.</span></span>

<span data-ttu-id="28fa9-130">Utilize o terminal do Azure Cloud Shell no lado direito para executar o seguinte comando da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="28fa9-130">Use the Azure Cloud Shell terminal on the right to run the following Azure CLI command.</span></span> <span data-ttu-id="28fa9-131">Isso cria o grupo de recursos na sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="28fa9-131">This will create the resource group in your subscription.</span></span>

```azurecli
az group create --name keyvault-exercise-group --location eastus
```

### <a name="create-the-vault-and-store-the-secret-in-it"></a><span data-ttu-id="28fa9-132">Criar o cofre e armazenar o segredo no mesmo</span><span class="sxs-lookup"><span data-stu-id="28fa9-132">Create the vault and store the secret in it</span></span>

<span data-ttu-id="28fa9-133">Criar o cofre e armazenar o segredo no mesmo.</span><span class="sxs-lookup"><span data-stu-id="28fa9-133">Next, we'll create the vault and store our secret in it.</span></span>

<span data-ttu-id="28fa9-134">**Os nomes do cofre de chaves têm de ser globalmente exclusivos e, portanto, precisará de escolher um nome exclusivo**.</span><span class="sxs-lookup"><span data-stu-id="28fa9-134">**Key Vault names must be globally unique, so you'll need to pick a unique name**.</span></span> <span data-ttu-id="28fa9-135">Os nomes do cofre têm de ter entre 3 e 24 carateres de comprimento e conter apenas carateres alfanuméricos e travessões.</span><span class="sxs-lookup"><span data-stu-id="28fa9-135">Vault names must be 3-24 characters long and contain only alphanumeric characters and dashes.</span></span>

```azurecli
az keyvault create --name <your-unique-vault-name> --resource-group keyvault-exercise-group --location eastus
```

<span data-ttu-id="28fa9-136">Quando terminar, verá a saída JSON que descreve o novo cofre.</span><span class="sxs-lookup"><span data-stu-id="28fa9-136">When it finishes, you'll see JSON output describing the new vault.</span></span>

<span data-ttu-id="28fa9-137">Agora, adicione o segredo: o nosso segredo terá o nome **SecretPassword** com um valor de **reindeer_flotilla**.</span><span class="sxs-lookup"><span data-stu-id="28fa9-137">Now add the secret: our secret will be named **SecretPassword** with a value of **reindeer_flotilla**.</span></span>

```azurecli
az keyvault secret set --name SecretPassword --value open_sesame --vault-name <your-unique-vault-name>
```

<span data-ttu-id="28fa9-138">Tome nota do nome do cofre &mdash; vai precisar dele novamente em breve.</span><span class="sxs-lookup"><span data-stu-id="28fa9-138">Make a note of the vault name &mdash; you'll be needing it again soon.</span></span>

<span data-ttu-id="28fa9-139">Vamos escrever o código para a nossa aplicação daqui a pouco, mas, primeiro, é necessário saber como a nossa aplicação se vai autenticar num cofre.</span><span class="sxs-lookup"><span data-stu-id="28fa9-139">We'll write the code for our application shortly, but first we need to learn a little bit about how our app is going to authenticate to a vault.</span></span>