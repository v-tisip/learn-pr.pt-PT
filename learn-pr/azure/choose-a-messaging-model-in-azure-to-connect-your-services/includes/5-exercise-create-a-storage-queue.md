Neste exercício, irá criar uma nova Conta de Armazenamento na sua subscrição do Azure. Em seguida, vai utilizar o Azure Cloud Shell para criar uma nova fila, adicionar uma mensagem à mesma e, em seguida, ler essa mensagem e removê-la da fila.

Estas são as mesmas ações executadas por componentes numa aplicação distribuída. Por exemplo, uma aplicação móvel pode adicionar uma mensagem a uma fila, onde aguarda por um serviço da Web para recuperá-la e processá-la.

## <a name="create-a-storage-account"></a>Criar uma Conta de Armazenamento

Uma vez que as filas de Armazenamento fazem parte de contas de Armazenamento do Azure para fins gerais. Tem de começar por criar uma conta de Armazenamento:

1. Num browser, navegue para o [Portal do Azure](http://portal.azure.com) e inicie sessão com as suas credenciais normais.
1. No canto superior esquerdo, clique em **Todos os serviços**.
1. Desloque para baixo para a secção **Armazenamento** e, em seguida, clique em **Contas de armazenamento**.
1. Na parte superior esquerda do painel **Contas de armazenamento**, clique em **Adicionar**.

    ![Criar uma Conta de Armazenamento](../images/5-create-a-storage-account-1.png)

1. Na caixa de texto **Nome**, escreva um nome único para a conta de armazenamento.
1. No **Modelo de implementação**, certifique-se de que o **Resource Manager** está selecionado.
1. Na lista pendente **Tipo de conta**, selecione **Armazenamento (fins gerais v2)**.
1. Na lista pendente **Localização**, selecione uma região perto de si.
1. Na lista pendente **Replicação**, selecione **Armazenamento localmente redundante (LRS)**.
1. Em **Desempenho**, selecione **Standard**.
1. Em **Camada de acesso**, selecione **Esporádico**.
1. Em **Transferência segura exigida**, selecione **Desativado**.
1. Em **Subscrição**, selecione a sua subscrição.

    ![Criar uma Conta de Armazenamento](../images/5-create-a-storage-account-2.png)

1. Em **Grupo de recursos**, selecione **Criar novo** e, em seguida, no tipo de caixa de texto **MusicSharingResourceGroup**.
1. Em **Redes virtuais**, selecione **Desativado** e, em seguida, clique em **Criar**.

    ![Criar uma Conta de Armazenamento](../images/5-create-a-storage-account-3.png)

O Azure cria a nova conta de armazenamento e o novo grupo de recursos.

## <a name="create-a-queue"></a>Criar uma Fila

Agora que a conta de armazenamento foi criada, pode adicionar uma nova fila à mesma. Tem de criar a fila com os comandos do PowerShell:

1. No canto superior direito do portal, clique na ligação **Cloud Shell**.

    ![Iniciar Cloud Shell](../images/5-create-a-storage-queue-1.png)

1. No ecrã **Bem-vindo ao Azure Cloud Shell**, clique em **PowerShell (Linux)**.
1. Se o ecrã **Não tem armazenamento montado** for apresentado, clique em **Criar armazenamento**.
1. Quando o comando `PS Azure` aparecer, para obter a conta de armazenamento, escreva o seguinte comando, ao substituir `<storageaccountname>` pelo nome exclusivo da sua conta de armazenamento e, em seguida, prima Enter:

    ```powershell
    $storageaccount = Get-AzureRmStorageAccount -Name <storageaccountname> -ResourceGroup  MusicSharingResourceGroup
    ```

1. Para obter o contexto da conta de armazenamento, escreva o seguinte comando e, em seguida, prima Enter:

    ```powershell
    $context = $storageaccount.Context
    ```

1. Para criar uma nova fila, escreva o seguinte comando e, em seguida, prima Enter:

    ```powershell
    $messageQueue = New-AzureStorageQueue -Name musicsharingmessages -Context $context
    ```

## <a name="add-a-message-to-the-queue"></a>Adicione uma Mensagem à Fila

Agora que criou uma fila na conta de armazenamento, pode adicionar uma mensagem à mesma.

1. Para criar uma nova mensagem, escreva o seguinte comando e, em seguida, prima Enter:

    ```powershell
    $newSongMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList "A new song has been added."
    ```

1. Para adicionar a nova mensagem à nova fila, escreva o seguinte comando e, em seguida, prima Enter:

    ```powershell
    $messageQueue.CloudQueue.AddMessageAsync($newSongMessage)
    ```

1. No Portal do Azure, na navegação à esquerda, clique em **Todos os recursos**.
1. Na lista de recursos, clique na conta de armazenamento que criou anteriormente.
1. No painel da conta de armazenamento, clique em **Explorador de Armazenamento (Pré-visualização)**.
1. No Explorador de Armazenamento, em **FILAS**, clique em **musicsharingmessages**. O Explorador de Armazenamento apresenta a mensagem que acabou de adicionar.

## <a name="retrieve-and-remove-the-message"></a>Recuperar e Remover a Mensagem

Um componente de destino para uma mensagem numa fila de Armazenamento, deve obter a mensagem na frente da fila, processá-la e, em seguida, eliminá-la da fila para que outros componentes não possam recuperá-la:

1. No Azure Cloud Shell, para obter a mensagem na frente da fila, escreva o seguinte comando e, em seguida, prima Enter:

    ```powershell
    $retrievedMessage = $messageQueue.CloudQueue.GetMessageAsync().Result
    ```

1. Para apresentar a mensagem, escreva o seguinte comando e, em seguida, prima Enter:

    ```powershell
    $retrievedMessage.AsString
    ```

1. Para apresentar todas as propriedades da mensagem, escreva o seguinte comando e, em seguida, prima Enter:

    ```powershell
    $retrievedMessage
    ```

1. Para remover a mensagem da fila, escreva o seguinte comando e, em seguida, prima Enter:

    ```powershell
    $messageQueue.CloudQueue.DeleteMessageAsync($retrievedMessage)
    ```

1. No Portal do Azure, para atualizar a visualização da fila, no painel Conta de Armazenamento, clique em **Descrição geral** e, em seguida, clique em **Explorador de Armazenamento**.
1. Em **FILAS**, clique em **musicsharingmessages**. O Explorador de Armazenamento mostra que a fila está vazia por ter removido a única mensagem.

## <a name="cleanup"></a>Limpeza

Para remover todos os recursos criados durante este exercício introduza o seguinte comando no Azure Cloud Shell 
```powershell
Remove-AzureRmResourceGroup -Name "MusicSharingResourceGroup" -Force
```


## <a name="summary"></a>Resumo

Aqui, criou uma Conta de Armazenamento na sua subscrição do Azure e criou uma nova fila na mesma. Também utilizou o PowerShell para simular as ações de componentes de aplicações distribuídas ao adicionar uma mensagem à fila e, em seguida, obtê-la e removê-la.

As filas da Conta de Armazenamento do Azure são uma boa solução quando pretende passar mensagens entre os componentes de uma aplicação distribuída. Não escolha Filas de armazenamento quando deseja publicar eventos.