<span data-ttu-id="f0c9c-101">Suponha que escolheu o Azure PowerShell como solução de automatização.</span><span class="sxs-lookup"><span data-stu-id="f0c9c-101">Suppose you have chosen Azure PowerShell as your automation solution.</span></span> <span data-ttu-id="f0c9c-102">Os administradores preferem executar os scripts localmente em vez de no Azure Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="f0c9c-102">Your administrators prefer to run their scripts locally rather than in the Azure Cloud Shell.</span></span> <span data-ttu-id="f0c9c-103">A equipa utiliza máquinas com Linux, macOS e Windows.</span><span class="sxs-lookup"><span data-stu-id="f0c9c-103">The team uses machines that run Linux, macOS, and Windows.</span></span> <span data-ttu-id="f0c9c-104">Tem de colocar o Azure PowerShell a funcionar em todos os dispositivos.</span><span class="sxs-lookup"><span data-stu-id="f0c9c-104">You need to get Azure PowerShell working on all their devices.</span></span> 

## <a name="what-must-be-installed"></a><span data-ttu-id="f0c9c-105">O que deve ser instalado?</span><span class="sxs-lookup"><span data-stu-id="f0c9c-105">What must be installed?</span></span>
<span data-ttu-id="f0c9c-106">Vamos percorrer as instruções de instalação reais na unidade seguinte, mas vamos examinar os dois componentes que constituem o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f0c9c-106">We'll go through the actual installation instructions in the next unit, but let's look at the two components which make up Azure PowerShell.</span></span>

- <span data-ttu-id="f0c9c-107">**Produto PowerShell base** Tem duas variantes: o PowerShell no Windows e o PowerShell Core no macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="f0c9c-107">**The base PowerShell product** This comes in two variants: PowerShell on Windows, and PowerShell Core on macOS and Linux.</span></span>
- <span data-ttu-id="f0c9c-108">**Módulo do Azure PowerShell** Este modulo adicional tem de estar instalado para adicionar os comandos específicos do Azure ao PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f0c9c-108">**The Azure PowerShell module** This extra module must be installed to add the Azure-specific commands to PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="f0c9c-109">O PowerShell está incluído no Windows (mas pode ter uma atualização disponível).</span><span class="sxs-lookup"><span data-stu-id="f0c9c-109">PowerShell is included with Windows (but might have an update available).</span></span> <span data-ttu-id="f0c9c-110">Terá de instalar o PowerShell Core no Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="f0c9c-110">You will need to install PowerShell Core on Linux and macOS.</span></span>

<span data-ttu-id="f0c9c-111">Depois de instalar o produto base, adicione o módulo do Azure PowerShell à sua instalação.</span><span class="sxs-lookup"><span data-stu-id="f0c9c-111">Once the base product is installed, you then add the Azure PowerShell module to your installation.</span></span>

## <a name="how-to-install-powershell-core"></a><span data-ttu-id="f0c9c-112">Como instalar o PowerShell Core</span><span class="sxs-lookup"><span data-stu-id="f0c9c-112">How to install PowerShell Core</span></span>
<span data-ttu-id="f0c9c-113">No Linux e no macOS, utilize um gestor de pacotes para instalar o PowerShell Core.</span><span class="sxs-lookup"><span data-stu-id="f0c9c-113">On both Linux and macOS, you use a package manager to install PowerShell Core.</span></span> <span data-ttu-id="f0c9c-114">O gestor de pacotes recomendado é diferente consoante o SO e a distribuição.</span><span class="sxs-lookup"><span data-stu-id="f0c9c-114">The recommended package manager differs by OS and distribution.</span></span>

> [!NOTE]
> <span data-ttu-id="f0c9c-115">O PowerShell Core está disponível no repositório da Microsoft, pelo que primeiro tem de adicionar esse repositório ao gestor de pacotes.</span><span class="sxs-lookup"><span data-stu-id="f0c9c-115">PowerShell Core is available in the Microsoft repository, so you'll first need to add that repository to your package manager.</span></span>

### <a name="linux"></a><span data-ttu-id="f0c9c-116">Linux</span><span class="sxs-lookup"><span data-stu-id="f0c9c-116">Linux</span></span>
<span data-ttu-id="f0c9c-117">No Linux, o gestor de pacotes será alterado consoante a distribuição Linux que escolher.</span><span class="sxs-lookup"><span data-stu-id="f0c9c-117">On Linux, the package manager will change based on the Linux distribution you choose.</span></span>

| <span data-ttu-id="f0c9c-118">Distribuição(ões)</span><span class="sxs-lookup"><span data-stu-id="f0c9c-118">Distribution(s)</span></span>  | <span data-ttu-id="f0c9c-119">Gestor de pacotes</span><span class="sxs-lookup"><span data-stu-id="f0c9c-119">Package manager</span></span> |
|------------------|-----------------|
| <span data-ttu-id="f0c9c-120">Ubuntu, Debian</span><span class="sxs-lookup"><span data-stu-id="f0c9c-120">Ubuntu, Debian</span></span>   | `apt-get`       |
| <span data-ttu-id="f0c9c-121">Red Hat, CentOS</span><span class="sxs-lookup"><span data-stu-id="f0c9c-121">Red Hat, CentOS</span></span>  | `yum`           |
| <span data-ttu-id="f0c9c-122">OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="f0c9c-122">OpenSUSE</span></span>         | `zypper`        |
| <span data-ttu-id="f0c9c-123">Fedora</span><span class="sxs-lookup"><span data-stu-id="f0c9c-123">Fedora</span></span>           | `dnf`           |

### <a name="mac"></a><span data-ttu-id="f0c9c-124">Mac</span><span class="sxs-lookup"><span data-stu-id="f0c9c-124">Mac</span></span>
<span data-ttu-id="f0c9c-125">No macOS, utilizará `Homebrew` para instalar o PowerShell Core.</span><span class="sxs-lookup"><span data-stu-id="f0c9c-125">On macOS, you will use `Homebrew` to install PowerShell Core.</span></span>

## <a name="how-to-install-azure-powershell"></a><span data-ttu-id="f0c9c-126">Como instalar o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f0c9c-126">How to install Azure PowerShell</span></span>
<span data-ttu-id="f0c9c-127">Assim que tiver o PowerShell instalado, o método de instalação preferencial para o módulo do Azure PowerShell é utilizar o comando `Install-Module` a partir do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f0c9c-127">Once you have PowerShell installed, the preferred installation method for the Azure PowerShell module is to use the `Install-Module` command from within PowerShell.</span></span> <span data-ttu-id="f0c9c-128">Precisará de privilégios elevados para instalar os módulos.</span><span class="sxs-lookup"><span data-stu-id="f0c9c-128">You'll need elevated privileges to install modules.</span></span>

- <span data-ttu-id="f0c9c-129">No Windows, tem de executar o PowerShell como administrador</span><span class="sxs-lookup"><span data-stu-id="f0c9c-129">On Windows you must run PowerShell as an administrator</span></span>
- <span data-ttu-id="f0c9c-130">No Linux e macOS, utilizará o comando `sudo` para obter privilégios elevados</span><span class="sxs-lookup"><span data-stu-id="f0c9c-130">On Linux and macOS, you will use the `sudo` command to obtain elevated privileges</span></span>

## <a name="summary"></a><span data-ttu-id="f0c9c-131">Resumo</span><span class="sxs-lookup"><span data-stu-id="f0c9c-131">Summary</span></span>
<span data-ttu-id="f0c9c-132">O PowerShell está incorporado no Windows, mas tem de instalar o módulo do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f0c9c-132">On Windows, PowerShell is built-in, but you must install the Azure PowerShell module.</span></span> <span data-ttu-id="f0c9c-133">No Linux e macOS, tem de instalar o PowerShell Core e o módulo do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f0c9c-133">On Linux and macOS, you must install both PowerShell Core and the Azure PowerShell module.</span></span> <span data-ttu-id="f0c9c-134">Na secção seguinte, vai percorrer os passos de instalação detalhados para algumas plataformas comuns.</span><span class="sxs-lookup"><span data-stu-id="f0c9c-134">In the next section, you will go through the detailed installation steps for some common platforms.</span></span>