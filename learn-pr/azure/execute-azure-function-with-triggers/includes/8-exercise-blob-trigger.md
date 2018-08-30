Neste exercício, iremos criar uma função do Azure que apresenta o nome e o tamanho de um blob quando este é criado ou atualizado. 

> [!NOTE]
> Para concluir este exercício, certifique-se de que tem sessão iniciada no [portal do Azure](https://portal.azure.com/) com uma conta válida.

## <a name="create-a-blob-trigger"></a>Criar um acionador de blobs

Uma vez mais, iremos continuar a utilizar a nossa Aplicação de funções do Azure existente e adicionar um acionador de blobs.

1. Aponte para **Funções** e selecione o ícone de sinal de adição (+).

    ![Aponte para Funções e selecione o sinal de adição](../media-drafts/4-hover-function.png)

1. Selecione **Acionador de blobs**.

1. Selecione **C#** como a linguagem. 

1. Deixe o **Nome** definido no valor predefinido.

1. Deixe o **Caminho** definido no valor predefinido.

1. Selecione uma Conta de armazenamento do Azure existente ou selecione **Criar**, se quiser que o Azure crie uma nova conta.

## <a name="download-storage-explorer"></a>Transferir o Explorador de Armazenamento

Agora que criámos um acionador de blobs, vamos transferir o Explorador de Armazenamento, que nos irá permitir criar facilmente um blob.

- Transfira o [Explorador de Armazenamento](http://storageexplorer.com).

## <a name="connect-to-your-azure-storage-account"></a>Ligar à sua conta de Armazenamento do Azure

Já temos o Explorador de Armazenamento transferido. Vamos iniciar sessão com as credenciais que foram fornecidas.

1. No Explorador de Armazenamento, selecione o ícone de sinal de adição (+) à esquerda.

1. Selecione **Use a storage account name and key** (Utilizar o nome e a chave de uma conta de armazenamento).

1. Selecione **Next** (Seguinte).

1. No Azure, no seu acionador de blobs, selecione **Integrar**.

1. Selecione **Documentação** para expandir a vista.

1. Copie o **Nome da Conta** e a **Chave da Conta**.

1. Novamente no Explorador de Armazenamento, cole o **Account Name** (Nome da Conta) e a **Account Key** (Chave da Conta).

1. Introduza um **Display name** (Nome a apresentar). Este valor é o nome da ligação no Explorador de Armazenamento.

1. Selecione **Next** (Seguinte).

1. Selecione **Connect** (Ligar). 

## <a name="create-a-blob-container"></a>Criar um contentor de blobs

Não estamos ligados à nossa Conta de Armazenamento do Azure. Não se esqueça de que o nosso acionador de blobs está a monitorizar apenas a localização descrita no campo **Path** (Caminho). Por predefinição, o nosso caminho deve ser:

> samples-workitems/{name}

Temos de criar um contentor chamado **samples-workitems**.

1. No Explorador de Armazenamento, expanda a sua conta de armazenamento. O nome deve ser o **Display name** (Nome a apresentar) que indicou durante o processo de ligação.

1. Clique com o botão direito do rato em **Blob Containers** (Contentores de Blobs) e selecione **Create blob container** (Criar contentor de blobs).

1. Introduza **samples-workitems**.

## <a name="turn-on-your-blob-trigger"></a>Ativar o acionador de blobs

Agora que criámos o nosso contentor para monitorizar, vamos executar a nossa função para podermos ver os resultados quando um blob é criado.

1. Selecione o acionador de blobs para abrir o ecrã de código.

1. Selecione **Run** (Executar).

## <a name="create-a-blob"></a>Criar um blob

O nosso acionador de blobs está a funcionar e à escuta de atividades. Vamos criar um blob para ver se recebemos uma mensagem de registo.

1. No Explorador de Armazenamento, selecione o contentor **samples-workitems**.

1. Selecione **Upload** (Carregar). 

1. Selecione **Upload Files** (Carregar Ficheiros).

1. Selecione qualquer ficheiro a partir do seu computador.

1. Selecione **Upload** (Carregar).

1. Volte ao Azure. Procure nos registos uma mensagem que apresente o ficheiro que foi carregado.

## <a name="clean-up"></a>Limpeza

Para garantir que esta função não lhe é cobrada, selecione **Colocar em pausa** por cima da janela de registo.

![Colocar em pausa](../media-drafts/4-pause-timer.png)


