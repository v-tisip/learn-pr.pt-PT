<span data-ttu-id="842dd-101">Neste exercício, vai continuar com o exemplo de uma empresa que cria ferramentas de administração do Linux.</span><span class="sxs-lookup"><span data-stu-id="842dd-101">In this exercise, you will continue with the example of a company that makes Linux admin tools.</span></span> <span data-ttu-id="842dd-102">Lembre-se de que planeia utilizar VMs do Linux para permitir aos potenciais clientes testar o seu software.</span><span class="sxs-lookup"><span data-stu-id="842dd-102">Recall that you plan to use Linux VMs to let potential customers test your software.</span></span> <span data-ttu-id="842dd-103">Tem um grupo de recursos pronto e agora chegou a altura de criar as VMs.</span><span class="sxs-lookup"><span data-stu-id="842dd-103">You have a resource group ready and now it is time to create the VMs.</span></span>

<span data-ttu-id="842dd-104">A sua empresa tem um stand numa grande feira sobre Linux.</span><span class="sxs-lookup"><span data-stu-id="842dd-104">Your company has paid for a booth at a big Linux trade show.</span></span> <span data-ttu-id="842dd-105">Planeia uma área de demonstração com três terminais cada ligados a uma VM do Linux separada.</span><span class="sxs-lookup"><span data-stu-id="842dd-105">You plan a demo area containing three terminals each connected to a separate Linux VM.</span></span> <span data-ttu-id="842dd-106">No final de cada dia, quer eliminar as VMs e recriá-las, para que recomecem do zero todas as manhãs.</span><span class="sxs-lookup"><span data-stu-id="842dd-106">At the end of each day, you want to delete the VMs and recreate them, so they start fresh every morning.</span></span> <span data-ttu-id="842dd-107">Criar as VMs manualmente depois do trabalho quando está cansado seria propenso a erros.</span><span class="sxs-lookup"><span data-stu-id="842dd-107">Creating the VMs manually after work when you are tired would be error prone.</span></span> <span data-ttu-id="842dd-108">Quer escrever um script do PowerShell para automatizar o processo de criação das VMs.</span><span class="sxs-lookup"><span data-stu-id="842dd-108">You want to write a PowerShell script to automate the VM creation process.</span></span>

## <a name="write-a-script-that-creates-virtual-machines"></a><span data-ttu-id="842dd-109">Escrever um script que cria Máquinas Virtuais</span><span class="sxs-lookup"><span data-stu-id="842dd-109">Write a script that creates Virtual Machines</span></span>

<span data-ttu-id="842dd-110">Siga estes passos para escrever o script:</span><span class="sxs-lookup"><span data-stu-id="842dd-110">Follow these steps to write the script:</span></span>

1. <span data-ttu-id="842dd-111">Crie um novo ficheiro de texto chamado **ConferenceDailyReset.ps1**.</span><span class="sxs-lookup"><span data-stu-id="842dd-111">Create a new text file named **ConferenceDailyReset.ps1**.</span></span>

2. <span data-ttu-id="842dd-112">Capture o parâmetro numa variável:</span><span class="sxs-lookup"><span data-stu-id="842dd-112">Capture the parameter in a variable:</span></span>

    ```powershell
    param([string]$resourceGroup)
    ```

3. <span data-ttu-id="842dd-113">Autentique no Azure com as suas credenciais:</span><span class="sxs-lookup"><span data-stu-id="842dd-113">Authenticate with Azure using your credentials:</span></span>

    ```powershell
    Connect-AzureRmAccount
    ```

4. <span data-ttu-id="842dd-114">Solicite um nome de utilizador e uma palavra-passe para a conta de administrador da VM e capture o resultado numa variável:</span><span class="sxs-lookup"><span data-stu-id="842dd-114">Prompt for a username and password for the VM's admin account and capture the result in a variable:</span></span>

    ```powershell
    $adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."
    ```

5. <span data-ttu-id="842dd-115">Crie um ciclo que seja executado três vezes:</span><span class="sxs-lookup"><span data-stu-id="842dd-115">Create a loop that executes three times:</span></span>

    ```powershell
    For ($i = 1; $i -le 3; $i++) 
    {

    }
    ```

6. <span data-ttu-id="842dd-116">No corpo do ciclo, crie um nome para cada VM e armazene-o numa variável:</span><span class="sxs-lookup"><span data-stu-id="842dd-116">In the loop body, create a name for each VM and store it in a variable:</span></span>

    ```powershell
    $vmName = "ConferenceDemo" + $i
    ```

7. <span data-ttu-id="842dd-117">Em seguida, crie uma VM com a variável `$vmName`:</span><span class="sxs-lookup"><span data-stu-id="842dd-117">Next, create a VM using the `$vmName` variable:</span></span>

   ```powershell
   New-AzureRmVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Location "East US" 
   ```

8. <span data-ttu-id="842dd-118">Guarde o ficheiro.</span><span class="sxs-lookup"><span data-stu-id="842dd-118">Save the file.</span></span>

<span data-ttu-id="842dd-119">O script completo deve ter o seguinte aspeto:</span><span class="sxs-lookup"><span data-stu-id="842dd-119">The completed script should look like this:</span></span>

```powershell
param([string]$resourceGroup)

$adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."

Connect-AzureRmAccount

For ($i = 1; $i -le 3; $i++)
{
    $vmName = "ConferenceDemo" + $i

    New-AzureRmVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Location "East US" -Image UbuntuLTS
}
```

## <a name="execute-the-script"></a><span data-ttu-id="842dd-120">Executar o script</span><span class="sxs-lookup"><span data-stu-id="842dd-120">Execute the script</span></span>

<span data-ttu-id="842dd-121">Inicie o PowerShell e altere o diretório onde guardou o ficheiro de script.</span><span class="sxs-lookup"><span data-stu-id="842dd-121">Launch PowerShell and change to the directory where you saved the script file.</span></span> <span data-ttu-id="842dd-122">Para executar o script, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="842dd-122">To run the script, execute the following command:</span></span>

```powershell
.\ConferenceDailyReset.ps1 TrialsResourceGroup
```

<span data-ttu-id="842dd-123">O script pode demorar alguns minutos a ser concluído.</span><span class="sxs-lookup"><span data-stu-id="842dd-123">The script may take a few minutes to complete.</span></span> <span data-ttu-id="842dd-124">Quando estiver concluído, certifique-se de que foi executado com êxito:</span><span class="sxs-lookup"><span data-stu-id="842dd-124">When it is finished, verify that it ran successfully:</span></span>

1. <span data-ttu-id="842dd-125">Num browser, inicie sessão no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="842dd-125">In a browser, sign into the Azure portal.</span></span>
2. <span data-ttu-id="842dd-126">Na navegação à esquerda, clique em **Grupos de Recursos**.</span><span class="sxs-lookup"><span data-stu-id="842dd-126">In the navigation on the left, click **Resource Groups**.</span></span>
3. <span data-ttu-id="842dd-127">Na lista de grupos de recursos, clique em **TrialsResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="842dd-127">In the list of resource groups, click **TrialsResourceGroup**.</span></span> <span data-ttu-id="842dd-128">Na lista de recursos, deverá ver as VMs recentemente criadas e os recursos associados.</span><span class="sxs-lookup"><span data-stu-id="842dd-128">In the list of resources, you should see the newly created VMs and their associated resources.</span></span>

## <a name="summary"></a><span data-ttu-id="842dd-129">Resumo</span><span class="sxs-lookup"><span data-stu-id="842dd-129">Summary</span></span>
<span data-ttu-id="842dd-130">Escreveu um script que automatizou a criação de três VMs no grupo de recursos indicado por um parâmetro de script.</span><span class="sxs-lookup"><span data-stu-id="842dd-130">You wrote a script that automated the creation of three VMs in the resource group indicated by a script parameter.</span></span> <span data-ttu-id="842dd-131">O script é curto e simples, mas automatiza um processo que levaria muito tempo a ser concluído manualmente com o portal.</span><span class="sxs-lookup"><span data-stu-id="842dd-131">The script is short and simple but automates a process that would take a long time to complete manually with the portal.</span></span>