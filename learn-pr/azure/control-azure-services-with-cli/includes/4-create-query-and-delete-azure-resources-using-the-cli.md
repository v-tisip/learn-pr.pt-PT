## <a name="motivation"></a><span data-ttu-id="9ea0b-101">Motivação</span><span class="sxs-lookup"><span data-stu-id="9ea0b-101">Motivation</span></span>
<span data-ttu-id="9ea0b-102">A CLI do Azure permite-lhe escrever comandos e executá-los imediatamente.</span><span class="sxs-lookup"><span data-stu-id="9ea0b-102">The Azure CLI lets you write commands and execute them immediately.</span></span> <span data-ttu-id="9ea0b-103">Lembre-se de que o objetivo geral no exemplo de desenvolvimento de software é implementar novas compilações de uma aplicação Web para fins de teste.</span><span class="sxs-lookup"><span data-stu-id="9ea0b-103">Recall that the overall goal in the software development example is to deploy new builds of a web app for testing.</span></span> <span data-ttu-id="9ea0b-104">O primeiro passo é criar um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="9ea0b-104">The first step is to create a resource group.</span></span> <span data-ttu-id="9ea0b-105">Lembre-se de que o objetivo aqui é criar estes recursos com uma instalação local da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ea0b-105">Remember that the goal here is to create these resources using a local installation of the Azure CLI.</span></span> 

<span data-ttu-id="9ea0b-106">Esta unidade mostra-lhe como utilizar a CLI do Azure para iniciar sessão na sua subscrição do Azure e criar um novo recurso.</span><span class="sxs-lookup"><span data-stu-id="9ea0b-106">This unit shows you how to use the Azure CLI to sign in to your Azure subscription and create a new resource.</span></span>

## <a name="what-azure-resources-can-be-managed-using-the-azure-cli"></a><span data-ttu-id="9ea0b-107">Que recursos do Azure podem ser geridos com a CLI do Azure?</span><span class="sxs-lookup"><span data-stu-id="9ea0b-107">What Azure resources can be managed using the Azure CLI?</span></span>
<span data-ttu-id="9ea0b-108">A CLI do Azure permite-lhe controlar praticamente todos os aspectos de cada recurso do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ea0b-108">The Azure CLI lets you control nearly every aspect of every Azure resource.</span></span> <span data-ttu-id="9ea0b-109">Pode trabalhar com grupos de recursos, armazenamento, máquinas virtuais, Azure Active Directory (Azure AD), contentores, aprendizagem automática e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="9ea0b-109">You can work with resource groups, storage, virtual machines, Azure Active Directory (Azure AD), containers, machine learning, and so on.</span></span>

<span data-ttu-id="9ea0b-110">Os comandos da CLI são estruturados em grupos e subgrupos.</span><span class="sxs-lookup"><span data-stu-id="9ea0b-110">Commands in the CLI are structured in groups and subgroups.</span></span> <span data-ttu-id="9ea0b-111">Cada grupo representa um serviço fornecido pelo Azure, sendo que os subgrupos dividem os comandos desses serviços em agrupamentos lógicos.</span><span class="sxs-lookup"><span data-stu-id="9ea0b-111">Each group represents a service provided by Azure, and the subgroups divide commands for these services into logical groupings.</span></span> <span data-ttu-id="9ea0b-112">Por exemplo, o grupo **armazenamento** contém subgrupos que incluem **conta**, **blob**, **armazenamento** e **fila**.</span><span class="sxs-lookup"><span data-stu-id="9ea0b-112">For example, the **storage** group contains subgroups including **account**, **blob**, **storage**, and **queue**.</span></span>

<span data-ttu-id="9ea0b-113">Assim, como encontrar os comandos específicos de que precisa?</span><span class="sxs-lookup"><span data-stu-id="9ea0b-113">So, how do you find the particular commands you need?</span></span> <span data-ttu-id="9ea0b-114">Uma das formas é usar **az find**.</span><span class="sxs-lookup"><span data-stu-id="9ea0b-114">One way is to use **az find**.</span></span> <span data-ttu-id="9ea0b-115">Por exemplo, se quiser localizar comandos que podem ajudá-lo a gerir um **blob** de armazenamento, usará o seguinte comando de pesquisa:</span><span class="sxs-lookup"><span data-stu-id="9ea0b-115">For example, if you want to find commands that might help you manage a storage **blob**, you'd use the following find command:</span></span>

```bash
az find -q blob
```

<span data-ttu-id="9ea0b-116">Se já sabe o nome do comando que pretende, o argumento **--help** desse comando poderá ser mais útil.</span><span class="sxs-lookup"><span data-stu-id="9ea0b-116">If you already know the name of the command you want, the **--help** argument for that command may be more useful.</span></span> <span data-ttu-id="9ea0b-117">Obtém informações detalhadas sobre o comando e, para um grupo de comandos, uma lista de subcomandos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="9ea0b-117">You get detailed information on the command, and for a command group, a list of the available subcommands.</span></span> <span data-ttu-id="9ea0b-118">Assim, com o nosso exemplo de armazenamento, apresentamos a seguir como pode obter uma lista dos comandos e dos subgrupos para gerir o armazenamento de blobs:</span><span class="sxs-lookup"><span data-stu-id="9ea0b-118">So, with our storage example, here's how you can get a list of the subgroups and commands for managing blob storage:</span></span>

```bash
az storage blob --help
```

## <a name="how-to-create-an-azure-resource"></a><span data-ttu-id="9ea0b-119">Como criar um recurso do Azure</span><span class="sxs-lookup"><span data-stu-id="9ea0b-119">How to create an Azure resource</span></span>
<span data-ttu-id="9ea0b-120">Ao criar um novo recurso do Azure, normalmente, existem três passos: ligar-se à sua subscrição do Azure, criar o recurso e verificar se a criação foi concluída com êxito (ver abaixo).</span><span class="sxs-lookup"><span data-stu-id="9ea0b-120">When creating a new Azure resource, there are typically three steps: connect to your Azure subscription, create the resource, and verify that creation was successful (see below).</span></span>

![Passos para criar um recurso com a CLI do Azure](../media-drafts/4-create-resources-overview.png)

<span data-ttu-id="9ea0b-122">Cada passo corresponde a um comando da CLI do Azure diferente.</span><span class="sxs-lookup"><span data-stu-id="9ea0b-122">Each step corresponds to a different Azure CLI command.</span></span>

### <a name="connect"></a><span data-ttu-id="9ea0b-123">Ligar</span><span class="sxs-lookup"><span data-stu-id="9ea0b-123">Connect</span></span>
<span data-ttu-id="9ea0b-124">Dado que está a trabalhar com uma instalação local da CLI do Azure, terá de se autenticar para poder executar os comandos do Azure, através do comando **login** da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ea0b-124">Since you're working with a local install of the Azure CLI, you'll need to authenticate before you can execute Azure commands, by using the Azure CLI **login** command.</span></span> 

```bash
az login
```

<span data-ttu-id="9ea0b-125">A CLI do Azure, normalmente, iniciará o seu browser predefinido para abrir a página de início de sessão do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ea0b-125">The Azure CLI will typically launch your default browser to open the Azure sign-in page.</span></span> <span data-ttu-id="9ea0b-126">Se não funcionar, siga as instruções da linha de comandos e introduza um código de autorização em [https://aka.ms/devicelogin](https://aka.ms/devicelogin).</span><span class="sxs-lookup"><span data-stu-id="9ea0b-126">If this doesn't work, follow the command-line instructions and enter an authorization code at [https://aka.ms/devicelogin](https://aka.ms/devicelogin).</span></span>

<span data-ttu-id="9ea0b-127">Após iniciar sessão, estará conectado à sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ea0b-127">After a successful sign in, you'll be connected to your Azure subscription.</span></span> 

### <a name="create"></a><span data-ttu-id="9ea0b-128">Criar</span><span class="sxs-lookup"><span data-stu-id="9ea0b-128">Create</span></span>
<span data-ttu-id="9ea0b-129">Muitas vezes, terá de criar um novo grupo de recursos antes de criar um novo serviço do Azure, pelo que vamos utilizar grupos de recursos como exemplo para mostrar como criar recursos do Azure a partir da CLI.</span><span class="sxs-lookup"><span data-stu-id="9ea0b-129">You'll often need to create a new resource group before you create a new Azure service, so we'll use resource groups as an example to show how to create Azure resources from the CLI.</span></span>

<span data-ttu-id="9ea0b-130">O comando **group create** da CLI do Azure cria um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="9ea0b-130">The Azure CLI **group create** command creates a resource group.</span></span> <span data-ttu-id="9ea0b-131">Tem de especificar um nome e a localização.</span><span class="sxs-lookup"><span data-stu-id="9ea0b-131">You must specify a name and location.</span></span> <span data-ttu-id="9ea0b-132">O nome tem de ser exclusivo na sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="9ea0b-132">The name must be unique within your subscription.</span></span> <span data-ttu-id="9ea0b-133">A localização determina onde os metadados do grupo de recursos serão armazenados.</span><span class="sxs-lookup"><span data-stu-id="9ea0b-133">The location determines where the metadata for your resource group will be stored.</span></span> <span data-ttu-id="9ea0b-134">Utilize cadeias de caracteres como “EUA Oeste”, “Europa do Norte” ou “Oeste da Índia” para especificar a localização; em alternativa, pode usar equivalentes de palavra única, por exemplo, euaoeste, europanorte ou oesteíndia.</span><span class="sxs-lookup"><span data-stu-id="9ea0b-134">You use strings like "West US", "North Europe", or "West India" to specify the location; alternatively, you can use single word equivalents, such as westus, northeurope, or westindia.</span></span> <span data-ttu-id="9ea0b-135">A sintaxe principal é:</span><span class="sxs-lookup"><span data-stu-id="9ea0b-135">The core syntax is:</span></span>

```bash
az group create --name <name> --location <location>
```

### <a name="verify"></a><span data-ttu-id="9ea0b-136">Verificar</span><span class="sxs-lookup"><span data-stu-id="9ea0b-136">Verify</span></span>
<span data-ttu-id="9ea0b-137">Para muitos recursos do Azure, a CLI do Azure fornece um subcomando de **lista** para ver os detalhes dos recursos.</span><span class="sxs-lookup"><span data-stu-id="9ea0b-137">For many Azure resources, the Azure CLI provides a **list** subcommand to view resource details.</span></span> <span data-ttu-id="9ea0b-138">Por exemplo, a **lista de grupos** da CLI do Azure lista os seus grupos de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ea0b-138">For example, the Azure CLI **group list** command lists your Azure resource groups.</span></span> <span data-ttu-id="9ea0b-139">Este subcomando é útil para verificar se a criação do grupo de recursos foi concluída com êxito:</span><span class="sxs-lookup"><span data-stu-id="9ea0b-139">This is useful here to verify whether creation of the resource group was successful:</span></span>

```bash
az group list
```

<span data-ttu-id="9ea0b-140">Para obter uma vista mais concisa, pode formatar a saída para ser uma tabela simples:</span><span class="sxs-lookup"><span data-stu-id="9ea0b-140">To get a more concise view, you can format the output as a simple table:</span></span>

```bash
az group list --output table
```
