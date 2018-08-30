<span data-ttu-id="5f98b-101">Neste exercício, vai criar uma máquina virtual do Windows no Azure.</span><span class="sxs-lookup"><span data-stu-id="5f98b-101">In this exercise, you'll create a Windows virtual machine in Azure.</span></span>

## <a name="motivation"></a><span data-ttu-id="5f98b-102">Motivação</span><span class="sxs-lookup"><span data-stu-id="5f98b-102">Motivation</span></span>

<span data-ttu-id="5f98b-103">Vamos considerar um cenário alternativo para este exercício.</span><span class="sxs-lookup"><span data-stu-id="5f98b-103">Let's consider an alternate scenario for this exercise.</span></span> <span data-ttu-id="5f98b-104">Aqui, a sua organização é uma instituição de ensino que utiliza as máquinas virtuais do Windows para acelerar ambientes de teste em que os estudantes instalam aplicações Web, configurar domínios e explorar as funcionalidades e serviços do Windows sem afetar os computadores da instituição de ensino.</span><span class="sxs-lookup"><span data-stu-id="5f98b-104">Here, your organization is a school that uses Windows virtual machines to spin up test environments on which students install web apps, configure domains, and explore Windows services and features without affecting the school's computers.</span></span> <span data-ttu-id="5f98b-105">Os professores ligam-se a estas VMs através do RDP e verificam o progresso dos alunos.</span><span class="sxs-lookup"><span data-stu-id="5f98b-105">Teachers connect to these VMs by using RDP and check on student progress.</span></span>

## <a name="create-a-windows-vm"></a><span data-ttu-id="5f98b-106">Criar uma VM do Windows</span><span class="sxs-lookup"><span data-stu-id="5f98b-106">Create a Windows VM</span></span>

<span data-ttu-id="5f98b-107">Para criar uma VM do Windows, execute os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="5f98b-107">To create a Windows VM, complete the following steps:</span></span>

1. <span data-ttu-id="5f98b-108">Inicie sessão no Azure através do [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5f98b-108">Log onto Azure through the [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="5f98b-109">Clique em **Criar um recurso**, no canto superior esquerdo do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f98b-109">Click **Create a resource** in the upper left corner of the Azure portal.</span></span>

1. <span data-ttu-id="5f98b-110">Na **barra de pesquisa**, introduza **Windows Server 2016 Datacenter** e, em seguida, clique na ligação com o mesmo título.</span><span class="sxs-lookup"><span data-stu-id="5f98b-110">In the **search bar**, enter  **Windows Server 2016 Datacenter**  and then click on the link with the same title.</span></span>

### <a name="configure-the-vm-settings"></a><span data-ttu-id="5f98b-111">Configurar as definições da VM</span><span class="sxs-lookup"><span data-stu-id="5f98b-111">Configure the VM settings</span></span>

1. <span data-ttu-id="5f98b-112">Em **Noções básicas**, no campo **Nome**, introduza um nome para a VM, por exemplo, “VM_aluno”.</span><span class="sxs-lookup"><span data-stu-id="5f98b-112">Under **Basics**, in the **Name** field, enter a name for your VM, such as "StudentVM."</span></span>

1. <span data-ttu-id="5f98b-113">No campo **Tipo de Disco da VM**, clique no menu pendente para ver as opções.</span><span class="sxs-lookup"><span data-stu-id="5f98b-113">In the **VM Disk Type** field, click the drop-down menu to see the options.</span></span> <span data-ttu-id="5f98b-114">Verifique se **SSD** está selecionado.</span><span class="sxs-lookup"><span data-stu-id="5f98b-114">Ensure that **SSD** is selected.</span></span>

1. <span data-ttu-id="5f98b-115">No campo **Nome de utilizador**, introduza um nome de utilizador adequado para utilizar para iniciar sessão na VM.</span><span class="sxs-lookup"><span data-stu-id="5f98b-115">In the **Username** field, enter a suitable user name to use to sign in to the VM.</span></span>

1. <span data-ttu-id="5f98b-116">No campo **Palavra-passe**, introduza uma palavra-passe que tenha, pelo menos, 12 carateres.</span><span class="sxs-lookup"><span data-stu-id="5f98b-116">In the **Password** field, enter a password that's at least 12 characters long.</span></span> <span data-ttu-id="5f98b-117">Também tem de ter carateres em maiúsculas e minúsculas, números e carateres especiais.</span><span class="sxs-lookup"><span data-stu-id="5f98b-117">It must also have upper and lowercase characters, numbers, and special characters.</span></span>

1. <span data-ttu-id="5f98b-118">Em **Grupo de recursos**, clique em **Criar nova**.</span><span class="sxs-lookup"><span data-stu-id="5f98b-118">Under **Resource group**, click **Create new**.</span></span> <span data-ttu-id="5f98b-119">Dê um nome ao grupo de recursos, por exemplo, “meuGRteste”.</span><span class="sxs-lookup"><span data-stu-id="5f98b-119">Give the resource group a name, such as "myTestRG."</span></span>

1. <span data-ttu-id="5f98b-120">Selecione uma localização adequada para a VM a ser criada e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="5f98b-120">Select a suitable location for the VM to be created, and then click **OK**.</span></span>

### <a name="select-the-vm-image-size-and-options"></a><span data-ttu-id="5f98b-121">Selecionar as opções e o tamanho da imagem da VM</span><span class="sxs-lookup"><span data-stu-id="5f98b-121">Select the VM image size and options</span></span>

1. <span data-ttu-id="5f98b-122">Na página **Escolher um tamanho**, clique na imagem **B1s** e, em seguida, em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="5f98b-122">In the **Choose a size** page, click the **B1s** image, and then click **Select**.</span></span>

   > [!Note] 
   > <span data-ttu-id="5f98b-123">A imagem B1 tem apenas 1 GB de RAM e resultará em erros de memória quando iniciar sessão pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="5f98b-123">The B1 image has only 1 GB of RAM and will result in memory errors when you first sign in.</span></span> <span data-ttu-id="5f98b-124">No entanto, pode redimensionar a imagem mais tarde como parte de um laboratório posterior.</span><span class="sxs-lookup"><span data-stu-id="5f98b-124">However, you can resize the image later as part of a later lab.</span></span>

1. <span data-ttu-id="5f98b-125">Na página **Definições**, em **Selecionar Portas de Entrada Pública**, selecione **Nenhuma porta de entrada pública**.</span><span class="sxs-lookup"><span data-stu-id="5f98b-125">In the **Settings** page, under **Select Public Inbound Ports**, select **No public inbound ports**.</span></span> <span data-ttu-id="5f98b-126">Vamos configurar o acesso do RDP posteriormente.</span><span class="sxs-lookup"><span data-stu-id="5f98b-126">We'll configure RDP access later.</span></span>

### <a name="finish-configuring-the-vm-and-create-the-image"></a><span data-ttu-id="5f98b-127">Concluir a configuração da VM e criar a imagem</span><span class="sxs-lookup"><span data-stu-id="5f98b-127">Finish configuring the VM and create the image</span></span>

1. <span data-ttu-id="5f98b-128">Desloque-se para baixo e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="5f98b-128">Scroll to the bottom and click **OK**.</span></span>

1. <span data-ttu-id="5f98b-129">Em **Criar**, verifique as definições que configurou.</span><span class="sxs-lookup"><span data-stu-id="5f98b-129">Under **Create**, check the settings that you configured.</span></span> <span data-ttu-id="5f98b-130">Na parte inferior, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5f98b-130">At the bottom, click **Create**.</span></span> <span data-ttu-id="5f98b-131">O dashboard do Azure mostrará a VM que está a ser implementada.</span><span class="sxs-lookup"><span data-stu-id="5f98b-131">The Azure dashboard will show the VM that's being deployed.</span></span> <span data-ttu-id="5f98b-132">Este processo pode demorar vários minutos.</span><span class="sxs-lookup"><span data-stu-id="5f98b-132">This may take several minutes.</span></span>

## <a name="summary"></a><span data-ttu-id="5f98b-133">Resumo</span><span class="sxs-lookup"><span data-stu-id="5f98b-133">Summary</span></span>

<span data-ttu-id="5f98b-134">Acabou de criar uma máquina virtual do Windows Server adequada para os requisitos dos alunos e acessível a partir da rede da instituição de ensino.</span><span class="sxs-lookup"><span data-stu-id="5f98b-134">You've now created a Windows Server virtual machine that's suitable for student requirements and accessible from the school network.</span></span> <span data-ttu-id="5f98b-135">Na unidade seguinte, verá como se ligar e gerir essa VM através do RDP.</span><span class="sxs-lookup"><span data-stu-id="5f98b-135">In the next unit, you will look at how you connect to and manage that VM by using RDP.</span></span>
