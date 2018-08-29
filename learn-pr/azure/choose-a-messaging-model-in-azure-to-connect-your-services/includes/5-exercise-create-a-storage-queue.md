<span data-ttu-id="bdf75-101">Neste exercício, irá criar uma nova Conta de Armazenamento na sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="bdf75-101">In this exercise, you will create a new Storage Account in your Azure subscription.</span></span> <span data-ttu-id="bdf75-102">Em seguida, vai utilizar o Azure Cloud Shell para criar uma nova fila, adicionar uma mensagem à mesma e, em seguida, ler essa mensagem e removê-la da fila.</span><span class="sxs-lookup"><span data-stu-id="bdf75-102">You will then use the Azure Cloud Shell to create a new queue, add a message to it, and then read that message and remove it from the queue.</span></span>

<span data-ttu-id="bdf75-103">Estas são as mesmas ações executadas por componentes numa aplicação distribuída.</span><span class="sxs-lookup"><span data-stu-id="bdf75-103">These are the same actions taken by components in a distributed application.</span></span> <span data-ttu-id="bdf75-104">Por exemplo, uma aplicação móvel pode adicionar uma mensagem a uma fila, onde aguarda por um serviço da Web para recuperá-la e processá-la.</span><span class="sxs-lookup"><span data-stu-id="bdf75-104">For example, a mobile app may add a message to a queue, where it waits for a web service to retrieve it and process it.</span></span>

## <a name="create-a-storage-account"></a><span data-ttu-id="bdf75-105">Criar uma Conta de Armazenamento</span><span class="sxs-lookup"><span data-stu-id="bdf75-105">Create a Storage Account</span></span>

<span data-ttu-id="bdf75-106">Uma vez que as filas de Armazenamento fazem parte de contas de Armazenamento do Azure para fins gerais.</span><span class="sxs-lookup"><span data-stu-id="bdf75-106">Since Storage queues are part of Azure general purpose Storage accounts.</span></span> <span data-ttu-id="bdf75-107">Tem de começar por criar uma conta de Armazenamento:</span><span class="sxs-lookup"><span data-stu-id="bdf75-107">You must start by creating a Storage account:</span></span>

1. <span data-ttu-id="bdf75-108">Num browser, navegue para o [Portal do Azure](http://portal.azure.com) e inicie sessão com as suas credenciais normais.</span><span class="sxs-lookup"><span data-stu-id="bdf75-108">In a browser, navigate to the [Azure Portal](http://portal.azure.com) and sign in with your normal credentials.</span></span>
1. <span data-ttu-id="bdf75-109">No canto superior esquerdo, clique em **Todos os serviços**.</span><span class="sxs-lookup"><span data-stu-id="bdf75-109">In the top left, click **All services**.</span></span>
1. <span data-ttu-id="bdf75-110">Desloque para baixo para a secção **Armazenamento** e, em seguida, clique em **Contas de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="bdf75-110">Scroll down to the **Storage** section, and then click **Storage accounts**.</span></span>
1. <span data-ttu-id="bdf75-111">Na parte superior esquerda do painel **Contas de armazenamento**, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="bdf75-111">At the top left of the **Storage accounts** blade, click **Add**.</span></span>

    ![Criar uma Conta de Armazenamento](../images/5-create-a-storage-account-1.png)

1. <span data-ttu-id="bdf75-113">Na caixa de texto **Nome**, escreva um nome único para a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="bdf75-113">In the **Name** text box, type a unique name for the storage account.</span></span>
1. <span data-ttu-id="bdf75-114">No **Modelo de implementação**, certifique-se de que o **Resource Manager** está selecionado.</span><span class="sxs-lookup"><span data-stu-id="bdf75-114">Under **Deployment model**, ensure that **Resource Manager** is selected.</span></span>
1. <span data-ttu-id="bdf75-115">Na lista pendente **Tipo de conta**, selecione **Armazenamento (fins gerais v2)**.</span><span class="sxs-lookup"><span data-stu-id="bdf75-115">In the **Account kind** drop-down list, select **Storage (general purpose v2)**.</span></span>
1. <span data-ttu-id="bdf75-116">Na lista pendente **Localização**, selecione uma região perto de si.</span><span class="sxs-lookup"><span data-stu-id="bdf75-116">In the **Location** drop-down list, select a region near you.</span></span>
1. <span data-ttu-id="bdf75-117">Na lista pendente **Replicação**, selecione **Armazenamento localmente redundante (LRS)**.</span><span class="sxs-lookup"><span data-stu-id="bdf75-117">In the **Replication** drop-down list, select **Locally-redundant storage (LRS)**.</span></span>
1. <span data-ttu-id="bdf75-118">Em **Desempenho**, selecione **Standard**.</span><span class="sxs-lookup"><span data-stu-id="bdf75-118">Under **Performance**, select **Standard**.</span></span>
1. <span data-ttu-id="bdf75-119">Em **Camada de acesso**, selecione **Esporádico**.</span><span class="sxs-lookup"><span data-stu-id="bdf75-119">Under **Access tier**, select **Cool**.</span></span>
1. <span data-ttu-id="bdf75-120">Em **Transferência segura exigida**, selecione **Desativado**.</span><span class="sxs-lookup"><span data-stu-id="bdf75-120">Under **Secure transfer required** select, **Disabled**.</span></span>
1. <span data-ttu-id="bdf75-121">Em **Subscrição**, selecione a sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="bdf75-121">Under **Subscription**, select your subscription.</span></span>

    ![Criar uma Conta de Armazenamento](../images/5-create-a-storage-account-2.png)

1. <span data-ttu-id="bdf75-123">Em **Grupo de recursos**, selecione **Criar novo** e, em seguida, no tipo de caixa de texto **MusicSharingResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="bdf75-123">Under **Resource group** select **Create new**, and then in the textbox type **MusicSharingResourceGroup**.</span></span>
1. <span data-ttu-id="bdf75-124">Em **Redes virtuais**, selecione **Desativado** e, em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="bdf75-124">Under **Virtual networks** select **Disabled** and then click **Create**.</span></span>

    ![Criar uma Conta de Armazenamento](../images/5-create-a-storage-account-3.png)

<span data-ttu-id="bdf75-126">O Azure cria a nova conta de armazenamento e o novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="bdf75-126">Azure creates the new storage account and the new resource group.</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="bdf75-127">Criar uma Fila</span><span class="sxs-lookup"><span data-stu-id="bdf75-127">Create a Queue</span></span>

<span data-ttu-id="bdf75-128">Agora que a conta de armazenamento foi criada, pode adicionar uma nova fila à mesma.</span><span class="sxs-lookup"><span data-stu-id="bdf75-128">Now that the Storage Account has been created, you can add a new queue to it.</span></span> <span data-ttu-id="bdf75-129">Tem de criar a fila com os comandos do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="bdf75-129">You must create the queue by using PowerShell commands:</span></span>

1. <span data-ttu-id="bdf75-130">No canto superior direito do portal, clique na ligação **Cloud Shell**.</span><span class="sxs-lookup"><span data-stu-id="bdf75-130">In the top right of the portal, click the **Cloud Shell** link.</span></span>

    ![Iniciar Cloud Shell](../images/5-create-a-storage-queue-1.png)

1. <span data-ttu-id="bdf75-132">No ecrã **Bem-vindo ao Azure Cloud Shell**, clique em **PowerShell (Linux)**.</span><span class="sxs-lookup"><span data-stu-id="bdf75-132">In the **Welcome to Azure Cloud Shell** screen, click **PowerShell (Linux)**.</span></span>
1. <span data-ttu-id="bdf75-133">Se o ecrã **Não tem armazenamento montado** for apresentado, clique em **Criar armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="bdf75-133">If the **You have no storage mounted** screen appears, click **Create storage**.</span></span>
1. <span data-ttu-id="bdf75-134">Quando o comando `PS Azure` aparecer, para obter a conta de armazenamento, escreva o seguinte comando, ao substituir `<storageaccountname>` pelo nome exclusivo da sua conta de armazenamento e, em seguida, prima Enter:</span><span class="sxs-lookup"><span data-stu-id="bdf75-134">When the `PS Azure` prompt appears, to obtain the storage account, type the following command, substituting `<storageaccountname>` with the unique name of your storage account, and then press Enter:</span></span>

    ```powershell
    $storageaccount = Get-AzureRmStorageAccount -Name <storageaccountname> -ResourceGroup  MusicSharingResourceGroup
    ```

1. <span data-ttu-id="bdf75-135">Para obter o contexto da conta de armazenamento, escreva o seguinte comando e, em seguida, prima Enter:</span><span class="sxs-lookup"><span data-stu-id="bdf75-135">To obtain the context of the storage account, type the following command and then press Enter:</span></span>

    ```powershell
    $context = $storageaccount.Context
    ```

1. <span data-ttu-id="bdf75-136">Para criar uma nova fila, escreva o seguinte comando e, em seguida, prima Enter:</span><span class="sxs-lookup"><span data-stu-id="bdf75-136">To create a new queue, type the following command and then press Enter:</span></span>

    ```powershell
    $messageQueue = New-AzureStorageQueue -Name musicsharingmessages -Context $context
    ```

## <a name="add-a-message-to-the-queue"></a><span data-ttu-id="bdf75-137">Adicione uma Mensagem à Fila</span><span class="sxs-lookup"><span data-stu-id="bdf75-137">Add a Message to the Queue</span></span>

<span data-ttu-id="bdf75-138">Agora que criou uma fila na conta de armazenamento, pode adicionar uma mensagem à mesma.</span><span class="sxs-lookup"><span data-stu-id="bdf75-138">Now that you have created a queue in the storage account, you can add a message to it.</span></span>

1. <span data-ttu-id="bdf75-139">Para criar uma nova mensagem, escreva o seguinte comando e, em seguida, prima Enter:</span><span class="sxs-lookup"><span data-stu-id="bdf75-139">To create a new message, type the following command and then press Enter:</span></span>

    ```powershell
    $newSongMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList "A new song has been added."
    ```

1. <span data-ttu-id="bdf75-140">Para adicionar a nova mensagem à nova fila, escreva o seguinte comando e, em seguida, prima Enter:</span><span class="sxs-lookup"><span data-stu-id="bdf75-140">To add the new message to the new queue, type the following command and then press Enter:</span></span>

    ```powershell
    $messageQueue.CloudQueue.AddMessageAsync($newSongMessage)
    ```

1. <span data-ttu-id="bdf75-141">No Portal do Azure, na navegação à esquerda, clique em **Todos os recursos**.</span><span class="sxs-lookup"><span data-stu-id="bdf75-141">In the Azure Portal, in the navigation on the left, click **All resources**.</span></span>
1. <span data-ttu-id="bdf75-142">Na lista de recursos, clique na conta de armazenamento que criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="bdf75-142">In the list of resources, click the storage account you created earlier.</span></span>
1. <span data-ttu-id="bdf75-143">No painel da conta de armazenamento, clique em **Explorador de Armazenamento (Pré-visualização)**.</span><span class="sxs-lookup"><span data-stu-id="bdf75-143">In the storage account blade, click **Storage Explorer (Preview)**.</span></span>
1. <span data-ttu-id="bdf75-144">No Explorador de Armazenamento, em **FILAS**, clique em **musicsharingmessages**.</span><span class="sxs-lookup"><span data-stu-id="bdf75-144">In the Storage Explorer, under **QUEUES**, click **musicsharingmessages**.</span></span> <span data-ttu-id="bdf75-145">O Explorador de Armazenamento apresenta a mensagem que acabou de adicionar.</span><span class="sxs-lookup"><span data-stu-id="bdf75-145">The Storage Explorer displays the message you just added.</span></span>

## <a name="retrieve-and-remove-the-message"></a><span data-ttu-id="bdf75-146">Recuperar e Remover a Mensagem</span><span class="sxs-lookup"><span data-stu-id="bdf75-146">Retrieve and Remove the Message</span></span>

<span data-ttu-id="bdf75-147">Um componente de destino para uma mensagem numa fila de Armazenamento, deve obter a mensagem na frente da fila, processá-la e, em seguida, eliminá-la da fila para que outros componentes não possam recuperá-la:</span><span class="sxs-lookup"><span data-stu-id="bdf75-147">A destination component for a message in a Storage queue, must retrieve the message at the front of the queue, process it, and then delete it from the queue so that other components do not retrieve it:</span></span>

1. <span data-ttu-id="bdf75-148">No Azure Cloud Shell, para obter a mensagem na frente da fila, escreva o seguinte comando e, em seguida, prima Enter:</span><span class="sxs-lookup"><span data-stu-id="bdf75-148">In the Azure Cloud Shell, to get the message at the front of the queue, type the following command and then press Enter:</span></span>

    ```powershell
    $retrievedMessage = $messageQueue.CloudQueue.GetMessageAsync().Result
    ```

1. <span data-ttu-id="bdf75-149">Para apresentar a mensagem, escreva o seguinte comando e, em seguida, prima Enter:</span><span class="sxs-lookup"><span data-stu-id="bdf75-149">To display the message, type the following command and then press Enter:</span></span>

    ```powershell
    $retrievedMessage.AsString
    ```

1. <span data-ttu-id="bdf75-150">Para apresentar todas as propriedades da mensagem, escreva o seguinte comando e, em seguida, prima Enter:</span><span class="sxs-lookup"><span data-stu-id="bdf75-150">To display all the properties of the message, type the following command and then press Enter:</span></span>

    ```powershell
    $retrievedMessage
    ```

1. <span data-ttu-id="bdf75-151">Para remover a mensagem da fila, escreva o seguinte comando e, em seguida, prima Enter:</span><span class="sxs-lookup"><span data-stu-id="bdf75-151">To remove the message from the queue, type the following command and then press Enter:</span></span>

    ```powershell
    $messageQueue.CloudQueue.DeleteMessageAsync($retrievedMessage)
    ```

1. <span data-ttu-id="bdf75-152">No Portal do Azure, para atualizar a visualização da fila, no painel Conta de Armazenamento, clique em **Descrição geral** e, em seguida, clique em **Explorador de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="bdf75-152">In the Azure Portal, to refresh the queue display, in the Storage Account blade, click **Overview** and then click **Storage Explorer**.</span></span>
1. <span data-ttu-id="bdf75-153">Em **FILAS**, clique em **musicsharingmessages**.</span><span class="sxs-lookup"><span data-stu-id="bdf75-153">Under **QUEUES**, click **musicsharingmessages**.</span></span> <span data-ttu-id="bdf75-154">O Explorador de Armazenamento mostra que a fila está vazia por ter removido a única mensagem.</span><span class="sxs-lookup"><span data-stu-id="bdf75-154">The Storage Explorer shows that the queue is empty because you removed the only message.</span></span>

## <a name="cleanup"></a><span data-ttu-id="bdf75-155">Limpeza</span><span class="sxs-lookup"><span data-stu-id="bdf75-155">Cleanup</span></span>

<span data-ttu-id="bdf75-156">Para remover todos os recursos criados durante este exercício introduza o seguinte comando no Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="bdf75-156">To remove all resources created during this exercise enter the following command in the Azure Cloud Shell</span></span> 
```powershell
Remove-AzureRmResourceGroup -Name "MusicSharingResourceGroup" -Force
```


## <a name="summary"></a><span data-ttu-id="bdf75-157">Resumo</span><span class="sxs-lookup"><span data-stu-id="bdf75-157">Summary</span></span>

<span data-ttu-id="bdf75-158">Aqui, criou uma Conta de Armazenamento na sua subscrição do Azure e criou uma nova fila na mesma.</span><span class="sxs-lookup"><span data-stu-id="bdf75-158">Here, you created a Storage Account in your Azure subscription and created a new queue in it.</span></span> <span data-ttu-id="bdf75-159">Também utilizou o PowerShell para simular as ações de componentes de aplicações distribuídas ao adicionar uma mensagem à fila e, em seguida, obtê-la e removê-la.</span><span class="sxs-lookup"><span data-stu-id="bdf75-159">You also used PowerShell to simulate the actions of distributed application components by adding a message to the queue and then retrieving and removing it.</span></span>

<span data-ttu-id="bdf75-160">As filas da Conta de Armazenamento do Azure são uma boa solução quando pretende passar mensagens entre os componentes de uma aplicação distribuída.</span><span class="sxs-lookup"><span data-stu-id="bdf75-160">Azure Storage Account queues are a good solution when you want to pass messages between the components of a distributed application.</span></span> <span data-ttu-id="bdf75-161">Não escolha Filas de armazenamento quando deseja publicar eventos.</span><span class="sxs-lookup"><span data-stu-id="bdf75-161">Do not choose Storage queues when you want to publish events.</span></span>