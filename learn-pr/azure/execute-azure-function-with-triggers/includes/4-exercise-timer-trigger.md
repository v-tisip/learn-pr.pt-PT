Neste exercício, iremos criar uma função do Azure que é invocada a cada 20 segundos através de um acionador de temporizador.

> [!NOTE] 
> Para concluir este exercício, certifique-se de que tem sessão iniciada no [portal do Azure](https://portal.azure.com/) com uma conta válida.

## <a name="create-an-azure-function"></a>Criar uma função do Azure

Vamos começar por criar uma função do Azure no portal.

1. Na navegação à esquerda, selecione **Criar um recurso**.

1. Selecione **Computação**.

1. Localize e selecione **Aplicação de Funções**. Opcionalmente, também pode utilizar a barra de pesquisa para localizar o modelo.

    ![Selecione Aplicação de Funções](../media/4-click-function-app.png)

1. Introduza um **Nome de aplicação** exclusivo.

1. Selecione uma **Subscrição**.

1. Crie um novo **Grupo de Recursos**.

1. Selecione **Windows** como o seu **SO**.

1. Selecione **Plano de Consumo** para o **Plano de Alojamento**. É-lhe cobrada cada execução da sua função. Os recursos são automaticamente atribuídos com base na carga de trabalho da aplicação.

1. Selecione uma **Localização**.

1. Crie uma nova conta de **Armazenamento**. (Este valor é obrigatório, mas não vamos utilizá-lo.)

1. Desative o **Application Insights**.

1. Selecione **Criar**.

## <a name="create-a-timer-trigger"></a>Criar um acionador de temporizador

Agora vamos criar um acionador de temporizador dentro da nossa função do Azure.

1. Depois de criar a função do Azure, selecione **Todos os recursos** no painel de navegação esquerdo.

1. Localize e selecione a função do Azure.

1. No novo painel, aponte para **Funções** e selecione o ícone de sinal de adição (+).

    ![Aponte para Funções e selecione o sinal de adição](../media/4-hover-function.png)

1. Selecione **Temporizador**.

1. Selecione **CSharp** como a linguagem.

1. Selecione **Criar esta função**.

## <a name="configure-the-timer-trigger"></a>Configurar o acionador de temporizador

Temos uma função do Azure com a lógica para imprimir uma mensagem na janela de registo. Vamos definir a agenda do temporizador para executar a cada 20 segundos.

1. Selecione **Integrar**.

1. Introduza o seguinte valor na caixa **Agenda**:

    ```
    */20 * * * * *
    ```

1. Selecione **Guardar**.

## <a name="start-the-timer"></a>Iniciar o temporizador

Agora que configurámos o temporizador, estamos prontos para iniciá-lo.

1. Selecione **TimerTriggerCSharp1**. 

    > [!NOTE]
    > **TimerTriggerCSharp1** é um nome predefinido. É selecionado automaticamente quando cria o acionador.

1. Selecione **Executar**. 

Agora deverá ver uma mensagem a cada 20 segundos na janela de registo.

## <a name="clean-up"></a>Limpeza

Para garantir que esta função não lhe é cobrada, acima da janela de registo, selecione **Colocar em pausa** para parar o temporizador.

![Colocar em pausa](../media/4-pause-timer.png)


