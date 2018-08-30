<span data-ttu-id="bb270-101">Suponha que trabalha numa empresa que produz um conjunto de ferramentas de administração do Linux.</span><span class="sxs-lookup"><span data-stu-id="bb270-101">Suppose you work at a company that makes a suite of Linux admin tools.</span></span> <span data-ttu-id="bb270-102">A sua função é ajudar os potenciais clientes a experimentar o software antes de o comprarem.</span><span class="sxs-lookup"><span data-stu-id="bb270-102">Your job is to help potential customers try your software before they buy it.</span></span> <span data-ttu-id="bb270-103">Uma vez que o software faz alterações a nível de raiz no sistema operativo, você decidiu criar uma VM do Linux para cada cliente de avaliação.</span><span class="sxs-lookup"><span data-stu-id="bb270-103">Because the software makes root-level changes to the OS, you have decided to create a Linux VM for each trial customer.</span></span> <span data-ttu-id="bb270-104">Cria as VMs, conforme necessário, e elimina-as no final da subscrição de avaliação.</span><span class="sxs-lookup"><span data-stu-id="bb270-104">You create the VMs as needed and delete them at the end of the trial subscription.</span></span> <span data-ttu-id="bb270-105">Dessa forma, cada cliente começa com uma versão limpa do sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="bb270-105">This way, each customer starts with a clean version of the OS.</span></span> 

<span data-ttu-id="bb270-106">Para manter estas VMs separadas das VMs que a sua empresa utiliza para testes internos, vai criar um grupo de recursos dedicado para as alojar.</span><span class="sxs-lookup"><span data-stu-id="bb270-106">To keep these VMs separate from the VMs your company uses for internal testing, you will create a dedicated resource group to house them.</span></span> <span data-ttu-id="bb270-107">Só precisa de um grupo de recursos, por isso, utilizar o Azure PowerShell no modo interativo é uma opção razoável para esta tarefa.</span><span class="sxs-lookup"><span data-stu-id="bb270-107">You only need one resource group so using Azure PowerShell in interactive mode is a reasonable choice for this task.</span></span>

## <a name="steps-to-create-a-resource-group"></a><span data-ttu-id="bb270-108">Passos para criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="bb270-108">Steps to create a resource group</span></span>

1. <span data-ttu-id="bb270-109">Inicie o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bb270-109">Launch PowerShell.</span></span>

1. <span data-ttu-id="bb270-110">Importe o módulo para a sessão atual para que tenha acesso aos cmdlets do Azure.</span><span class="sxs-lookup"><span data-stu-id="bb270-110">Import the module into the current session so you have access to the Azure cmdlets.</span></span>

   ```powershell
   Import-Module AzureRM
   ```

1. <span data-ttu-id="bb270-111">Ligue-se ao Azure com o comando mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="bb270-111">Connect to Azure using the command shown below.</span></span> <span data-ttu-id="bb270-112">Depois de introduzir o comando, autentique-se ao fornecer as credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="bb270-112">After entering the command, authenticate by providing your Azure credentials.</span></span>

   ```powershell
   Connect-AzureRmAccount
   ```

1. <span data-ttu-id="bb270-113">Crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="bb270-113">Create a resource group.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name "TrialsResourceGroup" -Location "East US"
    ```

1. <span data-ttu-id="bb270-114">Verifique se o grupo de recursos foi criado com êxito.</span><span class="sxs-lookup"><span data-stu-id="bb270-114">Verify the resource group was created successfully.</span></span>

    ```powershell
    Get-AzureRmResource | Format-Table
    ```
<span data-ttu-id="bb270-115">Outra forma de verificar se o grupo de recursos foi criado com êxito é utilizar o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bb270-115">Another way to check whether the resource group was created successfully is to use the Azure Portal.</span></span> <span data-ttu-id="bb270-116">Para tal, inicie sessão no Portal e navegue para a secção **Grupos de Recursos** (ver abaixo).</span><span class="sxs-lookup"><span data-stu-id="bb270-116">To do this, login to the Portal and navigate to the **Resource Groups** section (see below).</span></span> <span data-ttu-id="bb270-117">O novo grupo de recursos deverá ser apresentado na lista.</span><span class="sxs-lookup"><span data-stu-id="bb270-117">The new resource group should be displayed in the list.</span></span>

![Utilizar o Portal para Listar os Grupos de Recursos](../media-drafts/6-listing-resource-groups.png)

## <a name="summary"></a><span data-ttu-id="bb270-119">Resumo</span><span class="sxs-lookup"><span data-stu-id="bb270-119">Summary</span></span>
<span data-ttu-id="bb270-120">Este exercício mostra um padrão comum para uma sessão interativa do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bb270-120">This exercise shows a common pattern for an interactive PowerShell session.</span></span> <span data-ttu-id="bb270-121">Utilizou um cmdlet padrão para importar o módulo AzureRM e, em seguida, os cmdlets do Azure PowerShell para executar uma tarefa específica.</span><span class="sxs-lookup"><span data-stu-id="bb270-121">You used a standard cmdlet to import the AzureRM module and then the Azure PowerShell cmdlets to perform a specific task.</span></span> <span data-ttu-id="bb270-122">Agora tem um grupo de recursos na sua subscrição e está pronto para criar VMs.</span><span class="sxs-lookup"><span data-stu-id="bb270-122">You now have a resource group in your subscription and are ready to create VMs.</span></span>