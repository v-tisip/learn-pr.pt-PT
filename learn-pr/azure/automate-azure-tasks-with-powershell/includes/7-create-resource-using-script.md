<span data-ttu-id="54521-101">As tarefas repetitivas ou complexas, muitas vezes, consomem muito tempo administrativo.</span><span class="sxs-lookup"><span data-stu-id="54521-101">Complex or repetitive tasks often take a great deal of administrative time.</span></span> <span data-ttu-id="54521-102">As organizações preferem automatizar estas tarefas para reduzir os custos e evitar erros.</span><span class="sxs-lookup"><span data-stu-id="54521-102">Organizations prefer to automate these tasks to reduce costs and avoid errors.</span></span>

<span data-ttu-id="54521-103">Isto é importante no exemplo da empresa de Gestão das Relações com os Clientes (CRM).</span><span class="sxs-lookup"><span data-stu-id="54521-103">This is important in the Customer Relationship Management (CRM) company example.</span></span> <span data-ttu-id="54521-104">Na CRM pode testar o seu software em várias Máquinas Virtuais do Linux (VMs) que tem de eliminar e recriar continuamente.</span><span class="sxs-lookup"><span data-stu-id="54521-104">There, you test your software on multiple Linux Virtual Machines (VMs) that you need to continuously delete and recreate.</span></span> <span data-ttu-id="54521-105">Deve utilizar um script do PowerShell para automatizar a criação das VMs.</span><span class="sxs-lookup"><span data-stu-id="54521-105">You want to use a PowerShell script to automate the creation of the VMs.</span></span>

<span data-ttu-id="54521-106">Para além do funcionamento essencial de criação de uma VM, tem alguns requisitos adicionais para o seu script.</span><span class="sxs-lookup"><span data-stu-id="54521-106">Beyond the core operation of creating a VM you have a few additional requirements for your script.</span></span> 
- <span data-ttu-id="54521-107">Irá criar várias VMs, pelo que deve colocar a criação dentro de um ciclo</span><span class="sxs-lookup"><span data-stu-id="54521-107">You will create multiple VMs, so you want to put the creation inside a loop</span></span>
- <span data-ttu-id="54521-108">Tem de criar VMs em três grupos de recursos diferentes, para que o nome do grupo de recursos seja passado para o script como um parâmetro</span><span class="sxs-lookup"><span data-stu-id="54521-108">You need to create VMs in three different resource groups, so the name of the resource group should be passed to the script as a parameter</span></span>

<span data-ttu-id="54521-109">Nesta secção, verá como escrever e executar um script do Azure PowerShell que cumpre estes requisitos.</span><span class="sxs-lookup"><span data-stu-id="54521-109">In this section, you will see how to write and execute an Azure PowerShell script that meets these requirements.</span></span>

## <a name="what-is-a-powershell-script"></a><span data-ttu-id="54521-110">O que é um script do PowerShell?</span><span class="sxs-lookup"><span data-stu-id="54521-110">What is a PowerShell script?</span></span>
<span data-ttu-id="54521-111">Um script do PowerShell é um ficheiro de texto que contém comandos e construções de controlo.</span><span class="sxs-lookup"><span data-stu-id="54521-111">A PowerShell script is a text file containing commands and control constructs.</span></span> <span data-ttu-id="54521-112">Os comandos são invocações de cmdlets.</span><span class="sxs-lookup"><span data-stu-id="54521-112">The commands are invocations of cmdlets.</span></span> <span data-ttu-id="54521-113">As construções de controlo são funcionalidades de programação como ciclos, variáveis, parâmetros, comentários, etc., disponibilizados pelo PowerShell.</span><span class="sxs-lookup"><span data-stu-id="54521-113">The control constructs are programming features like loops, variables, parameters, comments, etc. supplied by PowerShell.</span></span>

<span data-ttu-id="54521-114">Os ficheiros de script do PowerShell têm uma extensão de ficheiro **.ps1**.</span><span class="sxs-lookup"><span data-stu-id="54521-114">PowerShell script files have a **.ps1** file extension.</span></span> <span data-ttu-id="54521-115">Pode criar e guardar estes ficheiros com qualquer editor de texto.</span><span class="sxs-lookup"><span data-stu-id="54521-115">You can create and save these files with any text editor.</span></span> 

> [!TIP]
> <span data-ttu-id="54521-116">Se estiver a escrever scripts do PowerShell no Windows, pode utilizar o Windows PowerShell Integrated Scripting Environment (ISE).</span><span class="sxs-lookup"><span data-stu-id="54521-116">If you’re writing PowerShell scripts under Windows, you can use the Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="54521-117">Este editor oferece funcionalidades como a sintaxe colorida e uma lista dos cmdlets disponíveis.</span><span class="sxs-lookup"><span data-stu-id="54521-117">This editor provides features such as syntax coloring and a list of available cmdlets.</span></span>
>
>![A ISE do Windows PowerShell](../media-drafts/7-windows-powershell-ise-screenshot.png)

<span data-ttu-id="54521-119">Assim que gravar o script, execute-o a partir da linha de comandos do PowerShell ao passar o nome do ficheiro precedido por um ponto e uma barra invertida:</span><span class="sxs-lookup"><span data-stu-id="54521-119">Once you have written the script, execute it from the PowerShell command line by passing the name of the file preceded by a dot and a backslash:</span></span>

```powershell
.\myScript.ps1
```

## <a name="powershell-techniques"></a><span data-ttu-id="54521-120">Técnicas do PowerShell</span><span class="sxs-lookup"><span data-stu-id="54521-120">PowerShell techniques</span></span>
<span data-ttu-id="54521-121">O PowerShell tem muitas funcionalidades encontradas em linguagens de programação típicas.</span><span class="sxs-lookup"><span data-stu-id="54521-121">PowerShell has many features found in typical programming languages.</span></span> <span data-ttu-id="54521-122">Pode definir variáveis, utilizar ramos e ciclos, capturar parâmetros da linha de comandos, escrever funções, adicionar comentários e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="54521-122">You can define variables, use branches and loops, capture command-line parameters, write functions, add comments, and so on.</span></span> <span data-ttu-id="54521-123">Iremos precisar de três funcionalidades para o nosso script: variáveis, ciclos e parâmetros.</span><span class="sxs-lookup"><span data-stu-id="54521-123">We will need three features for our script: variables, loops, and parameters.</span></span>

### <a name="variables"></a><span data-ttu-id="54521-124">Variáveis</span><span class="sxs-lookup"><span data-stu-id="54521-124">Variables</span></span>
<span data-ttu-id="54521-125">O PowerShell suporta variáveis.</span><span class="sxs-lookup"><span data-stu-id="54521-125">PowerShell supports variables.</span></span> <span data-ttu-id="54521-126">Utilize **$** para declarar uma variável e **=** para atribuir um valor.</span><span class="sxs-lookup"><span data-stu-id="54521-126">Use **$** to declare a variable and **=** to assign a value.</span></span> <span data-ttu-id="54521-127">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="54521-127">For example:</span></span>

```powershell
$loc = "East US"
$iterations = 3
```

<span data-ttu-id="54521-128">As variáveis podem conter objetos.</span><span class="sxs-lookup"><span data-stu-id="54521-128">Variables can hold objects.</span></span> <span data-ttu-id="54521-129">Por exemplo, a seguinte definição define a variável **adminCredential** para o objeto devolvido pelo cmdlet **Get-Credential**.</span><span class="sxs-lookup"><span data-stu-id="54521-129">For example, the following definition sets the **adminCredential** variable to the object returned by the **Get-Credential** cmdlet.</span></span>

```powershell
$adminCredential = Get-Credential
```

<span data-ttu-id="54521-130">Para obter o valor armazenado numa variável, utilize o prefixo **$** e o respetivo nome, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="54521-130">To obtain the value stored in a variable, use the **$** prefix and its name as shown below:</span></span> 

```powershell
$loc = "East US"
New-AzureRmResourceGroup -Name "MyResourceGroup" -Location $loc
```

### <a name="loops"></a><span data-ttu-id="54521-131">Ciclos</span><span class="sxs-lookup"><span data-stu-id="54521-131">Loops</span></span>
<span data-ttu-id="54521-132">O PowerShell tem vários ciclos: **For**, **Do...While**, **For...Each** e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="54521-132">PowerShell has several loops: **For**, **Do...While**, **For...Each**, and so on.</span></span> <span data-ttu-id="54521-133">O ciclo **For** é a melhor correspondência para as nossas necessidades porque iremos executar um cmdlet um número fixo de vezes.</span><span class="sxs-lookup"><span data-stu-id="54521-133">The **For** loop is the best match for our needs because we will execute a cmdlet a fixed number of times.</span></span>

<span data-ttu-id="54521-134">A sintaxe de núcleo é mostrada abaixo; o exemplo é executado durante duas iterações e imprime sempre o valor de **i**.</span><span class="sxs-lookup"><span data-stu-id="54521-134">The core syntax is shown below; the example runs for two iterations and prints the value of **i** each time.</span></span> <span data-ttu-id="54521-135">Os operadores de comparação são escritos **-lt** para "menos de", **-le** para "menos de ou igual a", **eq** para "igual", **ne** para "não igual a", etc.</span><span class="sxs-lookup"><span data-stu-id="54521-135">The comparison operators are written **-lt** for "less than", **-le** for "less than or equal", **eq** for "equal", **ne** for "not equal", etc.</span></span>

```powershell
For ($i = 1; $i -lt 3; $i++)
{
    $i
}
```

### <a name="parameters"></a><span data-ttu-id="54521-136">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="54521-136">Parameters</span></span>
<span data-ttu-id="54521-137">Quando executa um script, pode passar argumentos na linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="54521-137">When you execute a script, you can pass arguments on the command line.</span></span> <span data-ttu-id="54521-138">Pode indicar nomes para cada parâmetro para ajudar o script a extrair os valores.</span><span class="sxs-lookup"><span data-stu-id="54521-138">You can provide names for each parameter to help the script extract the values.</span></span> <span data-ttu-id="54521-139">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="54521-139">For example:</span></span>

```powershell
.\setupEnvironment.ps1 -size 5 -location "East US"
```

<span data-ttu-id="54521-140">No script, capture os valores em variáveis.</span><span class="sxs-lookup"><span data-stu-id="54521-140">Inside the script, you capture the values into variables.</span></span> <span data-ttu-id="54521-141">Neste exemplo, os parâmetros são correspondidos por nome:</span><span class="sxs-lookup"><span data-stu-id="54521-141">In this example, the parameters are matched by name:</span></span>

```powershell
param([string]$location, [int]$size)
```

<span data-ttu-id="54521-142">Pode omitir os nomes da linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="54521-142">You can omit the names from the command line.</span></span> <span data-ttu-id="54521-143">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="54521-143">For example:</span></span>

```powershell
.\setupEnvironment.ps1 5 "East US"
```

<span data-ttu-id="54521-144">No script, o utilizador depende da posição para a correspondência quando os parâmetros não têm nome:</span><span class="sxs-lookup"><span data-stu-id="54521-144">Inside the script, you rely on position for matching when the parameters are unnamed:</span></span>

```powershell
param([int]$size, [string]$location)
```

## <a name="how-to-create-a-linux-virtual-machine"></a><span data-ttu-id="54521-145">Como criar uma Máquina Virtual do Linux</span><span class="sxs-lookup"><span data-stu-id="54521-145">How to create a Linux Virtual Machine</span></span>
<span data-ttu-id="54521-146">O Azure PowerShell disponibiliza o cmdlet **New-AzureRmVm** para criar uma Máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="54521-146">Azure PowerShell provides the **New-AzureRmVm** cmdlet to create a Virtual Machine.</span></span> <span data-ttu-id="54521-147">O cmdlet tem vários parâmetros para permitir lidar com o grande número de definições de configuração de VM.</span><span class="sxs-lookup"><span data-stu-id="54521-147">The cmdlet has many parameters to let it handle the large number of VM configuration settings.</span></span> <span data-ttu-id="54521-148">A maioria dos parâmetros tem valores predefinidos razoáveis, portanto, precisamos apenas de especificar cinco coisas:</span><span class="sxs-lookup"><span data-stu-id="54521-148">Most of the parameters have reasonable default values so we only need to specify five things:</span></span>
- <span data-ttu-id="54521-149">**ResourceGroupName**: O grupo de recursos no qual a nova VM será colocada.</span><span class="sxs-lookup"><span data-stu-id="54521-149">**ResourceGroupName**: The resource group into which the new VM will be placed.</span></span>
- <span data-ttu-id="54521-150">**VM Name (Nome da VM)**: O nome da VM no Azure.</span><span class="sxs-lookup"><span data-stu-id="54521-150">**Name**: The name of the VM in Azure.</span></span>
- <span data-ttu-id="54521-151">**Localização**: A localização geográfica onde a VM será aprovisionada.</span><span class="sxs-lookup"><span data-stu-id="54521-151">**Location**: Geographic location where the VM will be provisioned.</span></span>
- <span data-ttu-id="54521-152">**Credencial**: Um objeto que contém o nome de utilizador e a palavra-passe para a conta de administrador da VM.</span><span class="sxs-lookup"><span data-stu-id="54521-152">**Credential**: An object containing the username and password for the VM admin account.</span></span> <span data-ttu-id="54521-153">Iremos utilizar o cmdlet **Get-Credential** para pedir um nome de utilizador e palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="54521-153">We will use the **Get-Credential** The cmdlet to prompt for a username and password.</span></span> <span data-ttu-id="54521-154">O **Get-Credential** inclui o nome de utilizador e a palavra-passe num objeto de credencial, que devolve como resultado.</span><span class="sxs-lookup"><span data-stu-id="54521-154">**Get-Credential** packages the username and password into a credential object, which it returns as its result.</span></span>
- <span data-ttu-id="54521-155">**Imagem**: identidade do sistema operativo a utilizar para a VM.</span><span class="sxs-lookup"><span data-stu-id="54521-155">**Image**: Identity of the operating system to use for the VM.</span></span> <span data-ttu-id="54521-156">Nós iremos utilizar "UbuntuLTS".</span><span class="sxs-lookup"><span data-stu-id="54521-156">We will use "UbuntuLTS".</span></span>

<span data-ttu-id="54521-157">A sintaxe do cmdlet é mostrada abaixo:</span><span class="sxs-lookup"><span data-stu-id="54521-157">The syntax for the cmdlet is shown below:</span></span>

```powershell
   New-AzureRmVm 
       -ResourceGroupName <resource group name> 
       -Name <machine name> 
       -Credential <credentials object> 
       -Location <location> 
       -Image <image name>
```

## <a name="summary"></a><span data-ttu-id="54521-158">Resumo</span><span class="sxs-lookup"><span data-stu-id="54521-158">Summary</span></span>
<span data-ttu-id="54521-159">A combinação do PowerShell e do Azure PowerShell oferece-lhe todas as ferramentas que precisa para automatizar o Azure.</span><span class="sxs-lookup"><span data-stu-id="54521-159">The combination of PowerShell and Azure PowerShell gives you all the tools you need to automate Azure.</span></span> <span data-ttu-id="54521-160">No nosso exemplo do CRM, poderemos criar várias VMs do Linux com um parâmetro para manter o script genérico e um ciclo para evitar o código repetido.</span><span class="sxs-lookup"><span data-stu-id="54521-160">In our CRM example, we will be able to create multiple Linux VMs using a parameter to keep the script generic and a loop to avoid repeated code.</span></span> <span data-ttu-id="54521-161">O que significa que uma operação anteriormente complexa agora pode ser executada num único passo.</span><span class="sxs-lookup"><span data-stu-id="54521-161">This means that a formerly complex operation can now be executed in a single step.</span></span>