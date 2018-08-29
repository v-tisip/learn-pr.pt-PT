<span data-ttu-id="a7141-101">Neste exercício, iremos criar uma função do Azure que apresenta o nome e o tamanho de um blob quando este é criado ou atualizado.</span><span class="sxs-lookup"><span data-stu-id="a7141-101">In this exercise, we're going to create an Azure function that displays the name and size of a blob when it's created or updated.</span></span> 

> [!NOTE]
> <span data-ttu-id="a7141-102">Para concluir este exercício, certifique-se de que tem sessão iniciada no [portal do Azure](https://portal.azure.com/) com uma conta válida.</span><span class="sxs-lookup"><span data-stu-id="a7141-102">To complete this exercise, make sure you're signed in to the [Azure portal](https://portal.azure.com/) with a valid account.</span></span>

## <a name="create-a-blob-trigger"></a><span data-ttu-id="a7141-103">Criar um acionador de blobs</span><span class="sxs-lookup"><span data-stu-id="a7141-103">Create a blob trigger</span></span>

<span data-ttu-id="a7141-104">Uma vez mais, iremos continuar a utilizar a nossa Aplicação de funções do Azure existente e adicionar um acionador de blobs.</span><span class="sxs-lookup"><span data-stu-id="a7141-104">Again, let's continue using our existing Azure Functions application and add a blob trigger.</span></span>

1. <span data-ttu-id="a7141-105">Aponte para **Funções** e selecione o ícone de sinal de adição (+).</span><span class="sxs-lookup"><span data-stu-id="a7141-105">Point to **Functions** and select the plus (+) icon.</span></span>

    ![Aponte para Funções e selecione o sinal de adição](../media/4-hover-function.png)

1. <span data-ttu-id="a7141-107">Selecione **Acionador de blobs**.</span><span class="sxs-lookup"><span data-stu-id="a7141-107">Select **Blob trigger**.</span></span>

1. <span data-ttu-id="a7141-108">Selecione **C#** como a linguagem.</span><span class="sxs-lookup"><span data-stu-id="a7141-108">Select **C#** as the language.</span></span> 

1. <span data-ttu-id="a7141-109">Deixe o **Nome** definido no valor predefinido.</span><span class="sxs-lookup"><span data-stu-id="a7141-109">Leave the **Name** set to the default value.</span></span>

1. <span data-ttu-id="a7141-110">Deixe o **Caminho** definido no valor predefinido.</span><span class="sxs-lookup"><span data-stu-id="a7141-110">Leave the **Path** set to the default value.</span></span>

1. <span data-ttu-id="a7141-111">Selecione uma Conta de armazenamento do Azure existente ou selecione **Criar**, se quiser que o Azure crie uma nova conta.</span><span class="sxs-lookup"><span data-stu-id="a7141-111">Select an existing Azure Storage account, or select **Create** if you want Azure to create a new account for you.</span></span>

## <a name="download-storage-explorer"></a><span data-ttu-id="a7141-112">Transferir o Explorador de Armazenamento</span><span class="sxs-lookup"><span data-stu-id="a7141-112">Download Storage explorer</span></span>

<span data-ttu-id="a7141-113">Agora que criámos um acionador de blobs, vamos transferir o Explorador de Armazenamento, que nos irá permitir criar facilmente um blob.</span><span class="sxs-lookup"><span data-stu-id="a7141-113">Now that we've created a blob trigger, let's download Storage explorer, which will allow us to easily create a blob.</span></span>

- <span data-ttu-id="a7141-114">Transfira o [Explorador de Armazenamento](http://storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="a7141-114">Download [Storage explorer](http://storageexplorer.com).</span></span>

## <a name="connect-to-your-azure-storage-account"></a><span data-ttu-id="a7141-115">Ligar à sua conta de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="a7141-115">Connect to your Azure Storage account</span></span>

<span data-ttu-id="a7141-116">Já temos o Explorador de Armazenamento transferido.</span><span class="sxs-lookup"><span data-stu-id="a7141-116">We now have Storage explorer downloaded.</span></span> <span data-ttu-id="a7141-117">Vamos iniciar sessão com as credenciais que foram fornecidas.</span><span class="sxs-lookup"><span data-stu-id="a7141-117">Let's sign in using the credentials that were supplied.</span></span>

1. <span data-ttu-id="a7141-118">No Explorador de Armazenamento, selecione o ícone de sinal de adição (+) à esquerda.</span><span class="sxs-lookup"><span data-stu-id="a7141-118">In Storage explorer, select the plus (+) icon on the left.</span></span>

1. <span data-ttu-id="a7141-119">Selecione **Use a storage account name and key** (Utilizar o nome e a chave de uma conta de armazenamento).</span><span class="sxs-lookup"><span data-stu-id="a7141-119">Select **Use a storage account name and key**.</span></span>

1. <span data-ttu-id="a7141-120">Selecione **Next** (Seguinte).</span><span class="sxs-lookup"><span data-stu-id="a7141-120">Select **Next**.</span></span>

1. <span data-ttu-id="a7141-121">No Azure, no seu acionador de blobs, selecione **Integrar**.</span><span class="sxs-lookup"><span data-stu-id="a7141-121">In Azure, under your blob trigger, select **Integrate**.</span></span>

1. <span data-ttu-id="a7141-122">Selecione **Documentação** para expandir a vista.</span><span class="sxs-lookup"><span data-stu-id="a7141-122">Select **Documentation** to expand the view.</span></span>

1. <span data-ttu-id="a7141-123">Copie o **Nome da Conta** e a **Chave da Conta**.</span><span class="sxs-lookup"><span data-stu-id="a7141-123">Copy the **Account Name** and **Account Key**.</span></span>

1. <span data-ttu-id="a7141-124">Novamente no Explorador de Armazenamento, cole o **Account Name** (Nome da Conta) e a **Account Key** (Chave da Conta).</span><span class="sxs-lookup"><span data-stu-id="a7141-124">Back in Storage explorer, paste in the **Account Name** and **Account Key**.</span></span>

1. <span data-ttu-id="a7141-125">Introduza um **Display name** (Nome a apresentar).</span><span class="sxs-lookup"><span data-stu-id="a7141-125">Enter a **Display name**.</span></span> <span data-ttu-id="a7141-126">Este valor é o nome da ligação no Explorador de Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a7141-126">This value is the name of the connection in Storage explorer.</span></span>

1. <span data-ttu-id="a7141-127">Selecione **Next** (Seguinte).</span><span class="sxs-lookup"><span data-stu-id="a7141-127">Select **Next**.</span></span>

1. <span data-ttu-id="a7141-128">Selecione **Connect** (Ligar).</span><span class="sxs-lookup"><span data-stu-id="a7141-128">Select **Connect**.</span></span> 

## <a name="create-a-blob-container"></a><span data-ttu-id="a7141-129">Criar um contentor de blobs</span><span class="sxs-lookup"><span data-stu-id="a7141-129">Create a blob container</span></span>

<span data-ttu-id="a7141-130">Não estamos ligados à nossa Conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="a7141-130">We aren't connected to our Azure Storage account.</span></span> <span data-ttu-id="a7141-131">Não se esqueça de que o nosso acionador de blobs está a monitorizar apenas a localização descrita no campo **Path** (Caminho).</span><span class="sxs-lookup"><span data-stu-id="a7141-131">Remember that our blob trigger is monitoring only the location described in the **Path** field.</span></span> <span data-ttu-id="a7141-132">Por predefinição, o nosso caminho deve ser:</span><span class="sxs-lookup"><span data-stu-id="a7141-132">By default, our path should be:</span></span>

> <span data-ttu-id="a7141-133">samples-workitems/{name}</span><span class="sxs-lookup"><span data-stu-id="a7141-133">samples-workitems/{name}</span></span>

<span data-ttu-id="a7141-134">Temos de criar um contentor chamado **samples-workitems**.</span><span class="sxs-lookup"><span data-stu-id="a7141-134">We need to create a container called **samples-workitems**.</span></span>

1. <span data-ttu-id="a7141-135">No Explorador de Armazenamento, expanda a sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a7141-135">In Storage explorer, expand your storage account.</span></span> <span data-ttu-id="a7141-136">O nome deve ser o **Display name** (Nome a apresentar) que indicou durante o processo de ligação.</span><span class="sxs-lookup"><span data-stu-id="a7141-136">The name should be the **Display name** that you provided during the connection process.</span></span>

1. <span data-ttu-id="a7141-137">Clique com o botão direito do rato em **Blob Containers** (Contentores de Blobs) e selecione **Create blob container** (Criar contentor de blobs).</span><span class="sxs-lookup"><span data-stu-id="a7141-137">Right-click **Blob Containers** and select **Create blob container**.</span></span>

1. <span data-ttu-id="a7141-138">Introduza **samples-workitems**.</span><span class="sxs-lookup"><span data-stu-id="a7141-138">Enter **samples-workitems**.</span></span>

## <a name="turn-on-your-blob-trigger"></a><span data-ttu-id="a7141-139">Ativar o acionador de blobs</span><span class="sxs-lookup"><span data-stu-id="a7141-139">Turn on your blob trigger</span></span>

<span data-ttu-id="a7141-140">Agora que criámos o nosso contentor para monitorizar, vamos executar a nossa função para podermos ver os resultados quando um blob é criado.</span><span class="sxs-lookup"><span data-stu-id="a7141-140">Now that we've created our container to monitor, let's run our function so we can see output when a blob is created.</span></span>

1. <span data-ttu-id="a7141-141">Selecione o acionador de blobs para abrir o ecrã de código.</span><span class="sxs-lookup"><span data-stu-id="a7141-141">Select your blob trigger to open the code screen.</span></span>

1. <span data-ttu-id="a7141-142">Selecione **Run** (Executar).</span><span class="sxs-lookup"><span data-stu-id="a7141-142">Select **Run**.</span></span>

## <a name="create-a-blob"></a><span data-ttu-id="a7141-143">Criar um blob</span><span class="sxs-lookup"><span data-stu-id="a7141-143">Create a blob</span></span>

<span data-ttu-id="a7141-144">O nosso acionador de blobs está a funcionar e à escuta de atividades.</span><span class="sxs-lookup"><span data-stu-id="a7141-144">Our blob trigger is now up and listening for activity.</span></span> <span data-ttu-id="a7141-145">Vamos criar um blob para ver se recebemos uma mensagem de registo.</span><span class="sxs-lookup"><span data-stu-id="a7141-145">Let's create a blob to see if we get a log message.</span></span>

1. <span data-ttu-id="a7141-146">No Explorador de Armazenamento, selecione o contentor **samples-workitems**.</span><span class="sxs-lookup"><span data-stu-id="a7141-146">In Storage explorer, select the **samples-workitems** container.</span></span>

1. <span data-ttu-id="a7141-147">Selecione **Upload** (Carregar).</span><span class="sxs-lookup"><span data-stu-id="a7141-147">Select **Upload**.</span></span> 

1. <span data-ttu-id="a7141-148">Selecione **Upload Files** (Carregar Ficheiros).</span><span class="sxs-lookup"><span data-stu-id="a7141-148">Select **Upload Files**.</span></span>

1. <span data-ttu-id="a7141-149">Selecione qualquer ficheiro a partir do seu computador.</span><span class="sxs-lookup"><span data-stu-id="a7141-149">Select any file from your computer.</span></span>

1. <span data-ttu-id="a7141-150">Selecione **Upload** (Carregar).</span><span class="sxs-lookup"><span data-stu-id="a7141-150">Select **Upload**.</span></span>

1. <span data-ttu-id="a7141-151">Volte ao Azure.</span><span class="sxs-lookup"><span data-stu-id="a7141-151">Go back to Azure.</span></span> <span data-ttu-id="a7141-152">Procure nos registos uma mensagem que apresente o ficheiro que foi carregado.</span><span class="sxs-lookup"><span data-stu-id="a7141-152">Check your logs for a message that displays what file was uploaded.</span></span>

## <a name="clean-up"></a><span data-ttu-id="a7141-153">Limpeza</span><span class="sxs-lookup"><span data-stu-id="a7141-153">Clean up</span></span>

<span data-ttu-id="a7141-154">Para garantir que esta função não lhe é cobrada, selecione **Colocar em pausa** por cima da janela de registo.</span><span class="sxs-lookup"><span data-stu-id="a7141-154">To ensure that you aren't charged for this function, select **Pause** above the log window.</span></span>

![Colocar em pausa](../media/4-pause-timer.png)


