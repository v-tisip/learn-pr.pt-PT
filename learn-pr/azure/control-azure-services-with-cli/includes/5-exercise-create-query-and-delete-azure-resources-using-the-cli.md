
<span data-ttu-id="8ad65-101">Neste exercício, vai utilizar a CLI do Azure no computador local para criar um grupo de recursos e, em seguida, implementar uma aplicação Web neste grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8ad65-101">In this exercise, you will use the Azure CLI on your local machine to create a resource group, and then to deploy a web app into this resource group.</span></span> 

### <a name="steps-to-create-a-resource-group"></a><span data-ttu-id="8ad65-102">Passos para criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="8ad65-102">Steps to create a resource group</span></span>
1. <span data-ttu-id="8ad65-103">Abra uma shell do Bash no Linux ou macOS ou, em alternativa, abra a janela Linha de Comandos ou o PowerShell se estiver a trabalhar no Windows.</span><span class="sxs-lookup"><span data-stu-id="8ad65-103">Open a bash shell on Linux or macOS, or open the Command Prompt window or PowerShell if working from Windows.</span></span>

1. <span data-ttu-id="8ad65-104">Inicie a CLI do Azure e execute o comando de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="8ad65-104">Start the Azure CLI and run the login command.</span></span>

    ```bash
    az login
    ```
    <span data-ttu-id="8ad65-105">Se não surgir uma página de início de sessão do Azure no browser, siga as instruções da linha de comandos e introduza um código de autorização em [https://aka.ms/devicelogin](https://aka.ms/devicelogin).</span><span class="sxs-lookup"><span data-stu-id="8ad65-105">If you do not get an Azure sign-in page in your web browser, follow the command-line instructions and enter an authorization code at [https://aka.ms/devicelogin](https://aka.ms/devicelogin).</span></span>

1. <span data-ttu-id="8ad65-106">Crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8ad65-106">Create a resource group.</span></span>

    ```bash
    az group create --location westeurope --name popupResGroup
    ```

1. <span data-ttu-id="8ad65-107">Verifique se o grupo de recursos foi criado com êxito ao listar todos os grupos de recursos numa tabela.</span><span class="sxs-lookup"><span data-stu-id="8ad65-107">Verify that the resource group was created successfully by listing all your resource groups in a table.</span></span>

    ```bash
    az group list --output table
    ```
1. <span data-ttu-id="8ad65-108">Opcionalmente, verifique se o recurso foi criado no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ad65-108">Optionally, confirm the resource was created in the Azure portal.</span></span> <span data-ttu-id="8ad65-109">Abra um browser, inicie sessão no portal e navegue para a secção **Grupos de Recursos** (ver abaixo).</span><span class="sxs-lookup"><span data-stu-id="8ad65-109">Open a web browser, sign in to the portal and navigate to the **Resource Groups** section (see below).</span></span> <span data-ttu-id="8ad65-110">O novo grupo de recursos deverá ser apresentado na lista.</span><span class="sxs-lookup"><span data-stu-id="8ad65-110">The new resource group should be displayed in the list.</span></span>

![Utilizar o Portal para Listar os Grupos de Recursos](../media-drafts/5-listing-resource-groups.png)

### <a name="steps-to-create-a-service-plan"></a><span data-ttu-id="8ad65-112">Passos para criar um plano do serviço</span><span class="sxs-lookup"><span data-stu-id="8ad65-112">Steps to create a service plan</span></span>
<span data-ttu-id="8ad65-113">Ao executar Aplicações Web, com o Serviço de Aplicações do Azure, paga os recursos de computação do Azure utilizados pela aplicação, o que depende do plano do Serviço de Aplicações associado às suas Aplicações Web.</span><span class="sxs-lookup"><span data-stu-id="8ad65-113">When you run Web Apps, using the Azure App Service, you pay for the Azure compute resources used by the app, and this depends on the App Service plan associated with your Web Apps.</span></span> <span data-ttu-id="8ad65-114">Os planos de serviço determinam a região utilizada para o datacenter da aplicação, o número de VMs utilizadas e o escalão de preços.</span><span class="sxs-lookup"><span data-stu-id="8ad65-114">Service plans determine the region used for the app datacenter, number of VMs used, and pricing tier.</span></span>

1. <span data-ttu-id="8ad65-115">Crie um plano do Serviço da Aplicações para executar a aplicação.</span><span class="sxs-lookup"><span data-stu-id="8ad65-115">Create an App Service plan to run your app.</span></span> <span data-ttu-id="8ad65-116">O nome da aplicação e do plano tem de ser exclusivo, assim, altere a cadeia de caracteres “12345” para um número aleatório.</span><span class="sxs-lookup"><span data-stu-id="8ad65-116">The name of the app and plan must be unique, so change the string "12345" to a random number.</span></span> <span data-ttu-id="8ad65-117">O comando seguinte não especifica um escalão de preço nem os detalhes de instância de VM; assim, por norma, obterá um plano **Básico** com 1 instância de VM **Pequena**.</span><span class="sxs-lookup"><span data-stu-id="8ad65-117">The following command does not specify a pricing tier or VM instance details, so by default, you'll get a **Basic** plan with 1 **Small** VM instance.</span></span>

    ```bash
    az appservice plan create --name popupapp12345 --resource-group popupResGroup --location westeurope
    ```

1. <span data-ttu-id="8ad65-118">Verifique se o plano de serviço foi criado com êxito ao listar todos os planos numa tabela.</span><span class="sxs-lookup"><span data-stu-id="8ad65-118">Verify that the service plan was created successfully by listing all your plans in a table.</span></span>

    ```bash
    az appservice plan list --output table
    ```

### <a name="steps-to-create-a-web-app"></a><span data-ttu-id="8ad65-119">Passos para criar uma aplicação Web</span><span class="sxs-lookup"><span data-stu-id="8ad65-119">Steps to create a web app</span></span>
<span data-ttu-id="8ad65-120">Em seguida, vai criar a aplicação Web no plano de serviço.</span><span class="sxs-lookup"><span data-stu-id="8ad65-120">Next, you'll create the web app in your service plan.</span></span> <span data-ttu-id="8ad65-121">Pode implementar o código ao mesmo tempo, mas, no nosso exemplo, vamos fazê-lo em passos distintos.</span><span class="sxs-lookup"><span data-stu-id="8ad65-121">You can deploy the code at the same time, but for our example, we'll do this as separate steps.</span></span>

1. <span data-ttu-id="8ad65-122">Crie a aplicação Web, lembrando-se de alterar a cadeia de caracteres “12345” para o mesmo número aleatório que utilizou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8ad65-122">Create the web app, remembering to change the string "12345" to the same random number you used earlier.</span></span>
    ```bash
    az webapp create --name popupapp12345 --resource-group popupResGroup --plan popupapp12345
    ```

1. <span data-ttu-id="8ad65-123">Verifique se a aplicação foi criada com êxito ao listar todas as aplicações numa tabela.</span><span class="sxs-lookup"><span data-stu-id="8ad65-123">Verify that the app was created successfully by listing all your apps in a table.</span></span>

    ```bash
    az webapp list --output table
    ```

1. <span data-ttu-id="8ad65-124">Anote o **DefaultHostName**; vai precisar dele posteriormente.</span><span class="sxs-lookup"><span data-stu-id="8ad65-124">Make a note of the **DefaultHostName**; you will need this later.</span></span>

### <a name="steps-to-deploy-code-from-github"></a><span data-ttu-id="8ad65-125">Passos para implementar o código a partir do GitHub</span><span class="sxs-lookup"><span data-stu-id="8ad65-125">Steps to deploy code from GitHub</span></span>
1. <span data-ttu-id="8ad65-126">A etapa final é implementar código a partir de um repositório do GitHub na aplicação Web, lembrando-se igualmente de alterar a cadeia de caracteres “12345” para o mesmo número aleatório que utilizou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8ad65-126">The final step is to deploy code from a GitHub repository to the web app, again remembering to change the string "12345" to the same random number you used earlier.</span></span>
    ```bash
    az webapp deployment source config --name popupapp12345 --resource-group popupResGroup --repo-url "https://github.com/Azure-Samples/php-docs-hello-world" --branch master --manual-integration
    ```

1. <span data-ttu-id="8ad65-127">Copie o URL seguinte para um browser para ver a aplicação Web.</span><span class="sxs-lookup"><span data-stu-id="8ad65-127">Copy the following url into a browser to see the web app.</span></span>
<span data-ttu-id="8ad65-128">http://popupapp12345.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="8ad65-128">http://popupapp12345.azurewebsites.net</span></span>

1. <span data-ttu-id="8ad65-129">A página apresenta “OláMundo!”</span><span class="sxs-lookup"><span data-stu-id="8ad65-129">The page displays "HelloWorld!"</span></span>

1. <span data-ttu-id="8ad65-130">Feche a janela do browser.</span><span class="sxs-lookup"><span data-stu-id="8ad65-130">Close the browser window.</span></span>

## <a name="summary"></a><span data-ttu-id="8ad65-131">Resumo</span><span class="sxs-lookup"><span data-stu-id="8ad65-131">Summary</span></span>
<span data-ttu-id="8ad65-132">Este exercício demonstrou um padrão típico de uma sessão interativa da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ad65-132">This exercise demonstrated a typical pattern for an interactive Azure CLI session.</span></span> <span data-ttu-id="8ad65-133">Primeiro, utilizou um comando padrão para criar um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8ad65-133">You first used a standard command to create a new resource group.</span></span> <span data-ttu-id="8ad65-134">Em seguida, utilizou um conjunto de comandos para implementar um recurso (neste exemplo, uma aplicação Web) para este grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8ad65-134">You then used a set of commands to deploy a resource (in this example, a web app) into this resource group.</span></span> <span data-ttu-id="8ad65-135">Este conjunto de comandos poderá ser facilmente combinado num script de shell e executado sempre que precisar de criar o mesmo recurso.</span><span class="sxs-lookup"><span data-stu-id="8ad65-135">This set of commands could easily be combined into a shell script, and executed every time you need to create the same resource.</span></span>
