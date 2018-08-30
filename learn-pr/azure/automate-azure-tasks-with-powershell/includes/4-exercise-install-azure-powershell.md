<span data-ttu-id="afc88-101">Neste exercício, vai instalar o **Azure PowerShell** no computador local.</span><span class="sxs-lookup"><span data-stu-id="afc88-101">In this exercise, you will install **Azure PowerShell** on your local machine.</span></span> <span data-ttu-id="afc88-102">Escolha a seção apropriada para o sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="afc88-102">Choose the appropriate section for your operating system.</span></span>

## <a name="linux-and-mac"></a><span data-ttu-id="afc88-103">Linux e Mac</span><span class="sxs-lookup"><span data-stu-id="afc88-103">Linux and Mac</span></span>
<span data-ttu-id="afc88-104">No Linux e no macOS, o primeiro passo é instalar o **PowerShell Core**.</span><span class="sxs-lookup"><span data-stu-id="afc88-104">On Linux and macOS, the first step is to install **PowerShell Core**.</span></span>

### <a name="linux"></a><span data-ttu-id="afc88-105">Linux</span><span class="sxs-lookup"><span data-stu-id="afc88-105">Linux</span></span>
<span data-ttu-id="afc88-106">Conforme mencionado na última unidade, instalar o PowerShell para Linux implicará utilizar um gestor de pacotes.</span><span class="sxs-lookup"><span data-stu-id="afc88-106">As mentioned in the last unit, installing PowerShell for Linux will involve using a package manager.</span></span> <span data-ttu-id="afc88-107">Vamos utilizar o **Ubuntu 18.04** neste exemplo, mas temos [instruções detalhadas para outras versões e distribuições na nossa documentação](https://docs.microsoft.com/powershell/scripting/setup/installing-powershell-core-on-linux).</span><span class="sxs-lookup"><span data-stu-id="afc88-107">We will use **Ubuntu 18.04** for our example here, but we have [detailed instructions for other versions and distributions in our documentation](https://docs.microsoft.com/powershell/scripting/setup/installing-powershell-core-on-linux).</span></span>

<span data-ttu-id="afc88-108">Aqui, vai instalar o PowerShell Core no Ubuntu Linux com o Advanced Packaging Tool (**apt**) e a linha de comandos do Bash.</span><span class="sxs-lookup"><span data-stu-id="afc88-108">You will install PowerShell Core on Ubuntu Linux using the Advanced Packaging Tool (**apt**) and the Bash command line.</span></span> 

1. <span data-ttu-id="afc88-109">Importe a chave de encriptação do repositório Ubuntu da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="afc88-109">Import the encryption key for the Microsoft Ubuntu repository.</span></span> <span data-ttu-id="afc88-110">Este procedimento permitirá que o gestor de pacotes verifique se o pacote do PowerShell Core que instala é da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="afc88-110">This will allow the package manager to verify that the PowerShell Core package you install comes from Microsoft.</span></span>

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```
1. <span data-ttu-id="afc88-111">Registe o **repositório Microsoft Ubuntu** para que o Gestor de pacotes possa localizar o pacote do PowerShell Core.</span><span class="sxs-lookup"><span data-stu-id="afc88-111">Register the **Microsoft Ubuntu repository** so the package manager can locate the PowerShell Core package.</span></span>

    ```bash
    sudo curl -o /etc/apt/sources.list.d/microsoft.list https://packages.microsoft.com/config/ubuntu/18.04/prod.list
    ```

1. <span data-ttu-id="afc88-112">Atualize a lista de pacotes.</span><span class="sxs-lookup"><span data-stu-id="afc88-112">Update the list of packages.</span></span>

    ```bash
    sudo apt-get update
    ```

1. <span data-ttu-id="afc88-113">Instale o PowerShell Core.</span><span class="sxs-lookup"><span data-stu-id="afc88-113">Install PowerShell Core.</span></span>

    ```bash
    sudo apt-get install -y powershell
    ```

1. <span data-ttu-id="afc88-114">Inicie o PowerShell para verificar se foi instalado com êxito.</span><span class="sxs-lookup"><span data-stu-id="afc88-114">Start PowerShell to verify that it installed successfully.</span></span>

    ```bash
    pwsh
    ```

### <a name="macos"></a><span data-ttu-id="afc88-115">macOS</span><span class="sxs-lookup"><span data-stu-id="afc88-115">macOS</span></span>
<span data-ttu-id="afc88-116">Em seguida, instale o **PowerShell Core** no macOS, com o gestor de pacotes Homebrew.</span><span class="sxs-lookup"><span data-stu-id="afc88-116">Next, install **PowerShell Core** on macOS using the Homebrew package manager.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="afc88-117">Se o comando **brew** não estiver disponível, poderá ter de instalar o gestor de pacotes Homebrew.</span><span class="sxs-lookup"><span data-stu-id="afc88-117">If the **brew** command is unavailable, you may need to install the Homebrew package manager.</span></span> <span data-ttu-id="afc88-118">Para obter os detalhes, veja o [site do Homebrew](https://brew.sh/).</span><span class="sxs-lookup"><span data-stu-id="afc88-118">For details see the [Homebrew website](https://brew.sh/).</span></span>

1. <span data-ttu-id="afc88-119">Instale o Homebrew-Cask, para obter mais pacotes, incluindo o pacote do PowerShell Core:</span><span class="sxs-lookup"><span data-stu-id="afc88-119">Install Homebrew-Cask to obtain more packages, including the PowerShell Core package:</span></span>

    ```bash
    brew tap caskroom/cask
    ```
1. <span data-ttu-id="afc88-120">Instale o PowerShell Core:</span><span class="sxs-lookup"><span data-stu-id="afc88-120">Install PowerShell Core:</span></span>

    ```bash
    brew cask install powershell
    ```

1. <span data-ttu-id="afc88-121">Inicie o PowerShell para verificar se foi instalado com êxito:</span><span class="sxs-lookup"><span data-stu-id="afc88-121">Start PowerShell Core to verify that it installed successfully:</span></span>

    ```bash
    pwsh
    ```

## <a name="install-azure-powershell"></a><span data-ttu-id="afc88-122">Instalar o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="afc88-122">Install Azure PowerShell</span></span>
<span data-ttu-id="afc88-123">Depois de instalar a produto **PowerShell** base, instale o **Azure PowerShell** para adicionar os comandos específicos do Azure.</span><span class="sxs-lookup"><span data-stu-id="afc88-123">After installing the base **PowerShell** product, install **Azure PowerShell** to add the Azure-specific commands.</span></span>

### <a name="windows"></a><span data-ttu-id="afc88-124">Windows</span><span class="sxs-lookup"><span data-stu-id="afc88-124">Windows</span></span>
<span data-ttu-id="afc88-125">Instale o Azure PowerShell no Windows com o comando `Install-Module` do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="afc88-125">Install Azure PowerShell on Windows using the `Install-Module` PowerShell command.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="afc88-126">Precisa do PowerShell versão 5.0 ou superior para instalar o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="afc88-126">You must have PowerShell version 5.0 or higher to install Azure PowerShell.</span></span> <span data-ttu-id="afc88-127">Para verificar a versão do PowerShell, utilize o comando seguinte:</span><span class="sxs-lookup"><span data-stu-id="afc88-127">To check your version of PowerShell, use the following command:</span></span> 
>
> `$PSVersionTable.PSVersion` 
>
><span data-ttu-id="afc88-128">Se o número da versão for inferior a 5.0, siga as instruções para [atualizar o PowerShell existente no Windows](https://docs.microsoft.com/powershell/scripting/setup/installing-windows-powershell?view=powershell-6#upgrading-existing-windows-powershell).</span><span class="sxs-lookup"><span data-stu-id="afc88-128">If the version number is lower than 5.0, follow the instructions for [upgrading existing Windows PowerShell](https://docs.microsoft.com/powershell/scripting/setup/installing-windows-powershell?view=powershell-6#upgrading-existing-windows-powershell).</span></span>

1. <span data-ttu-id="afc88-129">Abra o menu **Iniciar** e escreva **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="afc88-129">Open the **Start** menu and type **Windows PowerShell**.</span></span>
2. <span data-ttu-id="afc88-130">Clique com o botão direito do rato no ícone **Windows PowerShell** e selecione **Executar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="afc88-130">Right-click the **Windows PowerShell** icon and select **Run as administrator**.</span></span>
3. <span data-ttu-id="afc88-131">Na caixa de diálogo **Controlo de Conta de Utilizador**, selecione **Sim**.</span><span class="sxs-lookup"><span data-stu-id="afc88-131">In the **User Account Control** dialog, select **Yes**.</span></span>
4. <span data-ttu-id="afc88-132">Digite o comando seguinte e, em seguida, prima Enter:</span><span class="sxs-lookup"><span data-stu-id="afc88-132">Type the following command, and then press Enter:</span></span>

    ```powershell
    Install-Module -Name AzureRM
    ```
5. <span data-ttu-id="afc88-133">Quando lhe for perguntado se confia nos módulos do PSGallery, responda **Sim** ou **Sim para Todos**.</span><span class="sxs-lookup"><span data-stu-id="afc88-133">If you are asked whether you trust modules from PSGallery, answer **Yes** or **Yes to All**.</span></span>

> [!NOTE]
> <span data-ttu-id="afc88-134">Se obtiver uma mensagem de erro a indicar que já está instalada uma versão do módulo do Powershell do Azure, poderá atualizar para a versão _mais recente_ ao emitir o comando:</span><span class="sxs-lookup"><span data-stu-id="afc88-134">If you get an error message indicating that a version of the Azure Powershell module is already installed, you can update to the _latest_ version by issuing the command:</span></span>
> 
> `Update-Module -Name AzureRM`
> 
> <span data-ttu-id="afc88-135">Tal como no comando `Install-Module`, responda **Sim** ou **Sim para Todos** quando lhe for perguntado se confia no módulo.</span><span class="sxs-lookup"><span data-stu-id="afc88-135">As with the `Install-Module` command, answer **Yes** or **Yes to All** when prompted to trust the module.</span></span>

### <a name="linux-or-macos"></a><span data-ttu-id="afc88-136">Linux ou macOS</span><span class="sxs-lookup"><span data-stu-id="afc88-136">Linux or macOS</span></span>
<span data-ttu-id="afc88-137">Utilizamos o mesmo processo básico para instalar o Azure PowerShell no Linux ou no macOS.</span><span class="sxs-lookup"><span data-stu-id="afc88-137">We use the same basic process to install the Azure PowerShell on either Linux or macOS.</span></span> <span data-ttu-id="afc88-138">O procedimento é o mesmo para ambos os sistemas operativos.</span><span class="sxs-lookup"><span data-stu-id="afc88-138">The procedure is the same for both operating systems.</span></span> <span data-ttu-id="afc88-139">A diferença está na obtenção de uma sessão elevada do PowerShell Core.</span><span class="sxs-lookup"><span data-stu-id="afc88-139">The difference is in getting an elevated PowerShell Core session.</span></span>

1. <span data-ttu-id="afc88-140">Num terminal, escreva o comando seguinte para iniciar o PowerShell Core com privilégios elevados.</span><span class="sxs-lookup"><span data-stu-id="afc88-140">In a terminal, type the following command to launch PowerShell Core with elevated privileges.</span></span>

    ```bash
    sudo pwsh
    ```

1. <span data-ttu-id="afc88-141">Execute o seguinte comando na linha de comandos do Azure PowerShell para instalar o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="afc88-141">Run the following command at the PowerShell Core prompt to install Azure PowerShell.</span></span>

    ```powershell
    Install-Module AzureRM.NetCore
    ```

1. <span data-ttu-id="afc88-142">Quando lhe for perguntado se confia nos módulos do **PSGallery**, responda **Sim** ou **Sim para Todos**.</span><span class="sxs-lookup"><span data-stu-id="afc88-142">If you are asked whether you trust modules from **PSGallery**, answer **Yes** or **Yes to All**.</span></span>

## <a name="summary"></a><span data-ttu-id="afc88-143">Resumo</span><span class="sxs-lookup"><span data-stu-id="afc88-143">Summary</span></span>
<span data-ttu-id="afc88-144">Acabou de configurar os computadores locais para administrar os recursos do Azure com o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="afc88-144">You setup your local machine(s) to administer Azure resources with Azure PowerShell.</span></span> <span data-ttu-id="afc88-145">Agora, pode utilizar o Azure PowerShell localmente para introduzir comandos ou executar scripts.</span><span class="sxs-lookup"><span data-stu-id="afc88-145">You can now use Azure PowerShell locally to enter commands or execute scripts.</span></span> <span data-ttu-id="afc88-146">O Azure PowerShell vai encaminhar os comandos para os datacenters do Azure, onde serão executados no contexto da sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="afc88-146">Azure PowerShell will forward your commands to the Azure datacenters where they will run inside your Azure subscription.</span></span>