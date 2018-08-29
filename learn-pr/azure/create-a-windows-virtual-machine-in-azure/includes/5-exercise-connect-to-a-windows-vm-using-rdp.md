<span data-ttu-id="e6527-101">Neste exercício, vai utilizar o cliente RDP para ligar à VM do Windows que criou na unidade anterior.</span><span class="sxs-lookup"><span data-stu-id="e6527-101">In this exercise, you'll use the RDP client to connect to the Windows VM that you created in the previous unit.</span></span> <span data-ttu-id="e6527-102">Pode ligar ao transferir e executar um ficheiro RDP a partir do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e6527-102">You can connect by downloading and running an RDP file from the Azure portal.</span></span> <span data-ttu-id="e6527-103">Este ficheiro RDP vai ter:</span><span class="sxs-lookup"><span data-stu-id="e6527-103">This RDP file will have:</span></span>

* <span data-ttu-id="e6527-104">O endereço IP público da VM.</span><span class="sxs-lookup"><span data-stu-id="e6527-104">The public IP address of the VM.</span></span>
* <span data-ttu-id="e6527-105">O número da porta.</span><span class="sxs-lookup"><span data-stu-id="e6527-105">The port number.</span></span>

## <a name="motivation"></a><span data-ttu-id="e6527-106">Motivação</span><span class="sxs-lookup"><span data-stu-id="e6527-106">Motivation</span></span>

<span data-ttu-id="e6527-107">A partir do cenário do nosso exercício, é agora um estudante e quer aprender sobre adicionar funções e funcionalidades a um computador do Windows Server.</span><span class="sxs-lookup"><span data-stu-id="e6527-107">From our exercise scenario, you're now a student and you want to learn about adding roles and features to a Windows Server computer.</span></span> <span data-ttu-id="e6527-108">No entanto, o seu administrador de rede não quer que faça isto num computador físico na rede, além de os computadores da escola terem más especificações para executar o Windows Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="e6527-108">However, your network administrator doesn't want you to do this on a physical computer on the network, and the school's computers are too poorly specified to run Windows Hyper-V.</span></span> <span data-ttu-id="e6527-109">O Azure oferece a solução perfeita.</span><span class="sxs-lookup"><span data-stu-id="e6527-109">Azure provides the perfect solution.</span></span>

## <a name="configure-network-and-public-ip-address-settings"></a><span data-ttu-id="e6527-110">Configurar a rede e as definições de endereço IP público</span><span class="sxs-lookup"><span data-stu-id="e6527-110">Configure network and public IP address settings</span></span>

1. <span data-ttu-id="e6527-111">No portal do Azure, certifique-se de que o painel para a máquina virtual que criou mais cedo está aberto.</span><span class="sxs-lookup"><span data-stu-id="e6527-111">In the Azure portal, ensure the blade for the virtual machine that you created earlier is open.</span></span> <span data-ttu-id="e6527-112">Pode encontrar o painel sob **Todos os Recursos** se precisar de abri-lo.</span><span class="sxs-lookup"><span data-stu-id="e6527-112">You can find the blade under **All Resources** if you need to open it.</span></span>

1. <span data-ttu-id="e6527-113">Vá para a secção de **Redes**.</span><span class="sxs-lookup"><span data-stu-id="e6527-113">Go to the **Networking** section.</span></span> <span data-ttu-id="e6527-114">A parte superior desta secção tem ligações à sub-rede virtual e ao endereço IP dinâmico que foi criado juntamente com a nossa VM desde que utilizámos as predefinições.</span><span class="sxs-lookup"><span data-stu-id="e6527-114">The top of this section has links to the virtual subnet and dynamic IP address that were created along with our VM since we used the defaults.</span></span> <span data-ttu-id="e6527-115">Se quiséssemos alterar essas ligações, seguiríamos essas ligações (por exemplo, a alteração para um endereço IP estático).</span><span class="sxs-lookup"><span data-stu-id="e6527-115">We would follow these links if we wanted to change those resources (for example, changing to a static IP address).</span></span>

1. <span data-ttu-id="e6527-116">Clique em **Adicionar regra de porta de entrada**.</span><span class="sxs-lookup"><span data-stu-id="e6527-116">Click **Add inbound port rule**.</span></span>

1. <span data-ttu-id="e6527-117">Na parte superior da caixa de diálogo **Adicionar regra de segurança de entrada**, clique em **básica**.</span><span class="sxs-lookup"><span data-stu-id="e6527-117">At the top of the **Add inbound security rule** dialog box, click **basic**.</span></span>

1. <span data-ttu-id="e6527-118">Em **Serviço**, selecione **RDP** e, em seguida, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e6527-118">Under **Service**, select **RDP**, and then click **Add**.</span></span>

## <a name="connect-to-the-vm-by-using-rdp"></a><span data-ttu-id="e6527-119">Ligar à VM através de RDP</span><span class="sxs-lookup"><span data-stu-id="e6527-119">Connect to the VM by using RDP</span></span>

<span data-ttu-id="e6527-120">Para transferir o ficheiro de RDP e ligar à VM, realize os passos seguintes.</span><span class="sxs-lookup"><span data-stu-id="e6527-120">To download the RDP file and connect to the VM, carry out the following steps.</span></span>

### <a name="download-the-rdp-file"></a><span data-ttu-id="e6527-121">Transferir o ficheiro RDP</span><span class="sxs-lookup"><span data-stu-id="e6527-121">Download the RDP file</span></span>

1. <span data-ttu-id="e6527-122">Na secção do painel da máquina virtual **Descrição geral**, clique em **Ligar**.</span><span class="sxs-lookup"><span data-stu-id="e6527-122">In the **Overview** section of the virtual machine's blade, click **Connect**.</span></span>

1. <span data-ttu-id="e6527-123">No painel **Ligar a máquina virtual**, repare nas definições de **Endereço IP** e **Número de porta** e clique em **Transferir Ficheiro RDP**.</span><span class="sxs-lookup"><span data-stu-id="e6527-123">In the **Connect to virtual machine** blade, note the **IP address** and **Port number** settings, then click **Download RDP File**.</span></span>

1. <span data-ttu-id="e6527-124">No seu browser, clique em **Abrir** ou **Executar** para abrir o ficheiro RDP.</span><span class="sxs-lookup"><span data-stu-id="e6527-124">In your browser, click **Open** or **Run** to open the RDP file.</span></span>

### <a name="connect-to-the-windows-vm"></a><span data-ttu-id="e6527-125">Ligue-se à VM do Windows</span><span class="sxs-lookup"><span data-stu-id="e6527-125">Connect to the Windows VM</span></span>

1. <span data-ttu-id="e6527-126">Na caixa de diálogo **Ligação de Ambiente de Trabalho Remoto**, aponte o aviso de segurança e no endereço IP do computador remoto e clique em **Ligar**.</span><span class="sxs-lookup"><span data-stu-id="e6527-126">In the **Remote Desktop Connection** dialog box, note the security warning and the remote computer IP address, then click **Connect**.</span></span>

1. <span data-ttu-id="e6527-127">Na caixa de diálogo **Segurança do Windows**, introduza o seu nome de utilizador e palavra-passe que utilizou nos passos 6 e 7.</span><span class="sxs-lookup"><span data-stu-id="e6527-127">In the **Windows Security** dialog box, enter your user name and password that you used in steps 6 and 7.</span></span>

1. <span data-ttu-id="e6527-128">Na segunda caixa de diálogo **Ligação de Ambiente de Trabalho Remoto**, repare nos erros de certificado e clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="e6527-128">In the second **Remote Desktop Connection** dialog box, note the certificate errors, then click **Yes**.</span></span>

   > [!Note]
   > <span data-ttu-id="e6527-129">A área de trabalho da máquina virtual demora um pouco a aparecer.</span><span class="sxs-lookup"><span data-stu-id="e6527-129">The virtual machine desktop takes a while to appear.</span></span> <span data-ttu-id="e6527-130">Este efeito deve-se por a imagem B1 estar subespecificada.</span><span class="sxs-lookup"><span data-stu-id="e6527-130">This effect is because the B1 image is under-specified.</span></span> <span data-ttu-id="e6527-131">Pode receber uma mensagem sobre a alocação de memória baixa.</span><span class="sxs-lookup"><span data-stu-id="e6527-131">You may receive a message about low memory allocation.</span></span>

1. <span data-ttu-id="e6527-132">Na caixa de diálogo de **Redes**, clique em **Não**.</span><span class="sxs-lookup"><span data-stu-id="e6527-132">In the **Networks** dialog, click **No**.</span></span>

### <a name="resize-the-vm-in-the-azure-portal"></a><span data-ttu-id="e6527-133">Redimensione a VM no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e6527-133">Resize the VM in the Azure portal</span></span>

1. <span data-ttu-id="e6527-134">Regresse ao portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e6527-134">Switch back to the Azure portal.</span></span> <span data-ttu-id="e6527-135">Na página de propriedades da máquina virtual, em **Definições**, clique em **Tamanho**.</span><span class="sxs-lookup"><span data-stu-id="e6527-135">On the virtual machine properties page, under **Settings**, click **Size**.</span></span>

1. <span data-ttu-id="e6527-136">Clique em **D2s_v3** (2 vCPUs, 8 GB de RAM) e, em seguida, clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="e6527-136">Click **D2s_v3** (2 vCPUs, 8-GB RAM), and then click **Select**.</span></span> <span data-ttu-id="e6527-137">Vai ser apresentada uma mensagem de redimensionamento de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e6527-137">A resizing virtual machine message will display.</span></span> <span data-ttu-id="e6527-138">A VM na janela RDP também vai fechar.</span><span class="sxs-lookup"><span data-stu-id="e6527-138">The VM in the RDP window will also close down.</span></span>

1. <span data-ttu-id="e6527-139">Regresse ao portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e6527-139">Switch back to the Azure portal.</span></span> <span data-ttu-id="e6527-140">No painel do lado esquerdo, clique em **Máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="e6527-140">In the left pane, click **Virtual machines**.</span></span>

1. <span data-ttu-id="e6527-141">Em **Máquinas virtuais**, aguarde até que a sua VM mostre um estado **Em execução**.</span><span class="sxs-lookup"><span data-stu-id="e6527-141">Under **Virtual machines**, wait until your VM shows a status of **Running**.</span></span> <span data-ttu-id="e6527-142">Pode ter de clicar em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="e6527-142">You may need to click **Refresh**.</span></span>

1. <span data-ttu-id="e6527-143">Clique no nome da máquina virtual e em seguida, em **Configurações**, clique em **Tamanho**.</span><span class="sxs-lookup"><span data-stu-id="e6527-143">Click the virtual machine's name, then in **Settings**, click **Size**.</span></span> <span data-ttu-id="e6527-144">Tenha em atenção que o tamanho da VM está agora definido como **D2s_v3**.</span><span class="sxs-lookup"><span data-stu-id="e6527-144">Note the VM size is now set to **D2s_v3**.</span></span>

### <a name="reconnect-to-the-resized-vm"></a><span data-ttu-id="e6527-145">Volte a ligar à VM redimensionada</span><span class="sxs-lookup"><span data-stu-id="e6527-145">Reconnect to the resized VM</span></span>

1. <span data-ttu-id="e6527-146">Clique em **Máquinas virtuais** e então na sua VM.</span><span class="sxs-lookup"><span data-stu-id="e6527-146">Click **Virtual machines**, then click your VM.</span></span> <span data-ttu-id="e6527-147">Repare que o valor de **Endereço IP Público** foi provavelmente alterado.</span><span class="sxs-lookup"><span data-stu-id="e6527-147">Note the **Public IP Address** value has probably changed.</span></span> <span data-ttu-id="e6527-148">Clique em **Ligar** e então em **Executar** ou **Abrir** no seu browser.</span><span class="sxs-lookup"><span data-stu-id="e6527-148">Click **Connect**, and then click **Run** or **Open** in your browser.</span></span>

1. <span data-ttu-id="e6527-149">Na caixa de diálogo **Ligação de Ambiente de Trabalho Remoto**, aponte o aviso de segurança e no endereço IP do computador remoto e clique em **Ligar**.</span><span class="sxs-lookup"><span data-stu-id="e6527-149">In the **Remote Desktop Connection** dialog box, note the security warning and the remote computer IP address, then click **Connect**.</span></span>

1. <span data-ttu-id="e6527-150">Na caixa de diálogo **Segurança do Windows**, introduza o seu nome de utilizador e palavra-passe que utilizou nos passos 6 e 7.</span><span class="sxs-lookup"><span data-stu-id="e6527-150">In the **Windows Security** dialog box, enter your user name and password that you used in steps 6 and 7.</span></span>

1. <span data-ttu-id="e6527-151">Na segunda caixa de diálogo **Ligação de Ambiente de Trabalho Remoto**, repare nos erros de certificado e clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="e6527-151">In the second **Remote Desktop Connection** dialog box, note the certificate errors, then click **Yes**.</span></span> <span data-ttu-id="e6527-152">Repare no quanto mais responsiva está a máquina virtual no processo de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="e6527-152">Notice how much more responsive the virtual machine is to the sign-in process.</span></span>

1. <span data-ttu-id="e6527-153">Clique duas vezes na barra de tarefas e clique em **Gestor de Tarefas**.</span><span class="sxs-lookup"><span data-stu-id="e6527-153">Right-click the taskbar and click **Task Manager**.</span></span>

1. <span data-ttu-id="e6527-154">Na janela de **Gestor de Tarefas**, clique em **Mais detalhes**.</span><span class="sxs-lookup"><span data-stu-id="e6527-154">In the **Task Manager** window, click **More details**.</span></span>

1. <span data-ttu-id="e6527-155">Clique no separador **Desempenho**. Tenha em atenção a memória total disponível de 8 GB, dos quais cerca de 1,2 GB vão estar em utilização.</span><span class="sxs-lookup"><span data-stu-id="e6527-155">Click the **Performance** tab. Note the total available memory is 8 GB of which about 1.2 GB will be in use.</span></span> <span data-ttu-id="e6527-156">Fechar o **Gestor de Tarefas**.</span><span class="sxs-lookup"><span data-stu-id="e6527-156">Close **Task Manager**.</span></span>

## <a name="summary"></a><span data-ttu-id="e6527-157">Resumo</span><span class="sxs-lookup"><span data-stu-id="e6527-157">Summary</span></span>

<span data-ttu-id="e6527-158">Ligou a uma VM do Windows com o RDP.</span><span class="sxs-lookup"><span data-stu-id="e6527-158">You have connected to a Windows VM by using RDP.</span></span> <span data-ttu-id="e6527-159">Com o acesso à IU de Ambiente de Trabalho, pode administrar esta VM como faria com qualquer computador Windows.</span><span class="sxs-lookup"><span data-stu-id="e6527-159">With Desktop UI access, you can administer this VM as you would any Windows computer.</span></span>
