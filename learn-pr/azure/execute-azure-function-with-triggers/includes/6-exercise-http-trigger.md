Neste exercício, iremos criar uma função do Azure que aceita um pedido HTTP com uma única cadeia. A função devolve uma cadeia ao chamador para representar sucesso ou falha.

> [!NOTE]
> Para concluir este exercício, certifique-se de que tem sessão iniciada no [portal do Azure](https://portal.azure.com/) com uma conta válida.

## <a name="create-an-http-trigger"></a>Criar um acionador HTTP

Vamos continuar a utilizar a nossa Aplicação de funções do Azure existente e adicionar um acionador HTTP.

1. Aponte para **Funções** e selecione o ícone de sinal de adição (+).

    ![Aponte para Funções e selecione o sinal de adição](../media-drafts/4-hover-function.png)

1. Selecione **Acionador HTTP**.

1. Selecione **C#** como linguagem. 

1. Deixe o **Nome** definido no valor predefinido.

1. Defina o **Nível de autorização** para **Anónimo**.

1. Selecione **Criar**.

1. Dê uma breve vista de olhos no código gerado automaticamente para ter uma ideia do que se está a passar. O parâmetro *req* representa o pedido de entrada e contém um parâmetro de *nome*. Vemos se *nome* tem um valor. Se tiver, devolvemos uma saudação. Se não, devolvemos uma mensagem de erro.

## <a name="get-your-function-url"></a>Obter o URL de função

Agora que criámos o acionador HTTP, vamos obter o URL de função para iniciar um pedido.

1. Selecione o acionador HTTP para abrir o ecrã de código.

1. À direita de **Executar**, selecione **Obter URL de função**.

1. Selecione **Copiar**.

1. Selecione **Executar** para iniciar a sua função.

## <a name="issue-a-get-request-to-your-http-trigger"></a>Emitir um pedido GET para o acionador HTTP

Temos agora o URL de função copiado para a área de transferência. Vamos emitir um pedido GET para ver se obtemos uma resposta.

1. Abra um novo separador no browser.

1. Cole o URL na barra de endereço.

1. Adicione um parâmetro de cadeia de consulta chamado *nome* com o seu nome, por exemplo:

    ```
    .../api/HttpTriggerCSharp1?name=Jesse
    ```

1. Selecione ENTER para submeter o pedido.

## <a name="clean-up"></a>Limpeza

Para garantir que esta função não lhe é cobrada, selecione **Colocar em pausa** por cima da janela de registo.

![Colocar em pausa](../media-drafts/4-pause-timer.png)


