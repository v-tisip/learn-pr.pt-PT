
<span data-ttu-id="91e48-101">Neste exercício, vai instalar a CLI do Azure no computador local e, em seguida, executar um comando simples para verificar a instalação.</span><span class="sxs-lookup"><span data-stu-id="91e48-101">In this exercise, you will install the Azure CLI on your local machine, and then run a simple command to verify your installation.</span></span> 

## <a name="installing-the-azure-cli"></a><span data-ttu-id="91e48-102">Instalar a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="91e48-102">Installing the Azure CLI</span></span>
<span data-ttu-id="91e48-103">O método utilizado para instalar a CLI do Azure depende do sistema operativo do computador.</span><span class="sxs-lookup"><span data-stu-id="91e48-103">The method you use for installing the Azure CLI depends on the operating system of your computer.</span></span> <span data-ttu-id="91e48-104">Escolha os passos para o seu sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="91e48-104">Please choose the steps for your operating system.</span></span>

### <a name="linux"></a><span data-ttu-id="91e48-105">Linux</span><span class="sxs-lookup"><span data-stu-id="91e48-105">Linux</span></span>
<span data-ttu-id="91e48-106">Aqui, vai instalar a CLI do Azure no Ubuntu Linux com o Advanced Packaging Tool (**apt**) e a linha de comandos do Bash.</span><span class="sxs-lookup"><span data-stu-id="91e48-106">Here you will install the Azure CLI on Ubuntu Linux using the Advanced Packaging Tool (**apt**) and the Bash command line.</span></span>

> [!NOTE]
> <span data-ttu-id="91e48-107">Os comandos listados abaixo referem-se à versão 18.04 do Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="91e48-107">The commands listed below are for Ubuntu version 18.04.</span></span> <span data-ttu-id="91e48-108">Se estiver a utilizar uma versão diferente do Ubuntu, terá de adicionar um repositório diferente.</span><span class="sxs-lookup"><span data-stu-id="91e48-108">If you are using a different version of Ubuntu, you must add a different repository.</span></span> <span data-ttu-id="91e48-109">Para obter os detalhes, veja [Instalar a CLI 2.0 do Azure com apt](https://docs.microsoft.com/cli/azure/install-azure-cli-apt).</span><span class="sxs-lookup"><span data-stu-id="91e48-109">For details see [Install the Azure CLI 2.0 with apt](https://docs.microsoft.com/cli/azure/install-azure-cli-apt).</span></span>

1. <span data-ttu-id="91e48-110">Modifique a lista de origens para que o repositório da Microsoft seja registado e o gestor de pacotes possa localizar o pacote da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="91e48-110">Modify your sources list so that the Microsoft repository is registered, and the package manager can locate the Azure CLI package.</span></span>

    ```bash
    AZ_REPO=$(lsb_release -cs)
    echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | \
    sudo tee /etc/apt/sources.list.d/azure-cli.list
    ```
1. <span data-ttu-id="91e48-111">Importe a chave de encriptação do repositório Ubuntu da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="91e48-111">Import the encryption key for the Microsoft Ubuntu repository.</span></span> <span data-ttu-id="91e48-112">Este procedimento permitirá que o gestor de pacotes verifique se o pacote da CLI do Azure que instala é da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="91e48-112">This will allow the package manager to verify that the Azure CLI package you install comes from Microsoft.</span></span>

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```
1. <span data-ttu-id="91e48-113">Instale a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="91e48-113">Install the Azure CLI.</span></span>

    ```bash
    sudo apt-get install apt-transport-https
    sudo apt-get update && sudo apt-get install azure-cli
    ```

### <a name="macos"></a><span data-ttu-id="91e48-114">macOS</span><span class="sxs-lookup"><span data-stu-id="91e48-114">macOS</span></span>
<span data-ttu-id="91e48-115">Aqui, vai instalar a CLI do Azure no macOS, com o gestor de pacotes Homebrew.</span><span class="sxs-lookup"><span data-stu-id="91e48-115">Here you will install the Azure CLI on macOS using the Homebrew package manager.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="91e48-116">Se o comando **brew** não estiver disponível, poderá ter de instalar o gestor de pacotes Homebrew.</span><span class="sxs-lookup"><span data-stu-id="91e48-116">If the **brew** command is unavailable, you may need to install the Homebrew package manager.</span></span> <span data-ttu-id="91e48-117">Para obter os detalhes, veja o [site do Homebrew](https://brew.sh/).</span><span class="sxs-lookup"><span data-stu-id="91e48-117">For details see the [Homebrew website](https://brew.sh/).</span></span>

1. <span data-ttu-id="91e48-118">Atualize o repositório brew para se certificar de que obtém o pacote mais recente da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="91e48-118">Update your brew repository to make sure you get the latest Azure CLI package.</span></span>

    ```bash
    brew update
    ```
1. <span data-ttu-id="91e48-119">Instale a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="91e48-119">Install the Azure CLI.</span></span>

    ```bash
    brew install azure-cli
    ```

### <a name="windows"></a><span data-ttu-id="91e48-120">Windows</span><span class="sxs-lookup"><span data-stu-id="91e48-120">Windows</span></span>
<span data-ttu-id="91e48-121">Aqui, vai instalar a CLI do Azure no Windows com o instalador MSI.</span><span class="sxs-lookup"><span data-stu-id="91e48-121">Here you will install the Azure CLI on Windows using the MSI installer.</span></span>

1. <span data-ttu-id="91e48-122">Aceda a [https://aka.ms/installazurecliwindows](https://aka.ms/installazurecliwindows) e, na caixa de diálogo de segurança do browser, clique em **Executar**.</span><span class="sxs-lookup"><span data-stu-id="91e48-122">Go to [https://aka.ms/installazurecliwindows](https://aka.ms/installazurecliwindows), and in the browser security dialog box, click **Run**.</span></span>
1. <span data-ttu-id="91e48-123">No instalador, aceite os termos de licenciamento e clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="91e48-123">In the installer, accept the license terms, and then click **Install**.</span></span>
1. <span data-ttu-id="91e48-124">Na caixa de diálogo **Controlo de Conta de Utilizador**, selecione **Sim**.</span><span class="sxs-lookup"><span data-stu-id="91e48-124">In the **User Account Control** dialog, select **Yes**.</span></span>

## <a name="running-the-azure-cli"></a><span data-ttu-id="91e48-125">Executar a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="91e48-125">Running the Azure CLI</span></span>
<span data-ttu-id="91e48-126">Execute a CLI do Azure ao abrir uma shell do Bash (Linux e macOS) ou a partir da linha de comandos ou do PowerShell (Windows).</span><span class="sxs-lookup"><span data-stu-id="91e48-126">You run the Azure CLI by opening a bash shell (Linux and macOS), or from the command prompt or PowerShell (Windows).</span></span>

1. <span data-ttu-id="91e48-127">Inicie a CLI do Azure e verifique a instalação ao executar a verificação da versão.</span><span class="sxs-lookup"><span data-stu-id="91e48-127">Start the Azure CLI and verify your installation by running the version check.</span></span>

    ```bash
    az --version
    ```

> [!NOTE]
> <span data-ttu-id="91e48-128">No Windows, executar a CLI do Azure a partir do PowerShell tem algumas vantagens em relação a executar a CLI do Azure a partir da linha de comandos; por exemplo, o PowerShell fornece funcionalidades de conclusão de separadores adicionais em comparação com aquelas disponíveis na linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="91e48-128">In Windows, running the Azure CLI from PowerShell has some advantages over running the Azure CLI from the command prompt; for example, PowerShell provides additional tab completion features over those available from the command prompt.</span></span> 

## <a name="summary"></a><span data-ttu-id="91e48-129">Resumo</span><span class="sxs-lookup"><span data-stu-id="91e48-129">Summary</span></span>
<span data-ttu-id="91e48-130">Acabou de configurar os computadores locais para administrar os recursos do Azure com a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="91e48-130">You set up your local machines to administer Azure resources with the Azure CLI.</span></span> <span data-ttu-id="91e48-131">Agora, pode utilizar a CLI do Azure localmente para introduzir comandos ou executar scripts.</span><span class="sxs-lookup"><span data-stu-id="91e48-131">You can now use the Azure CLI locally to enter commands or execute scripts.</span></span> <span data-ttu-id="91e48-132">O Azure PowerShell encaminhará os comandos para os datacenters do Azure, onde serão executados no contexto da sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="91e48-132">The Azure CLI will forward your commands to the Azure datacenters where they will run inside your Azure subscription.</span></span>
