A aplicação e a função do Azure estão agora concluídas e em execução localmente. Nesta unidade, publica a função do Azure para o Azure ser executado na cloud.

> Nesta unidade, irá publicar a sua função a partir do Visual Studio. Esta é uma ótima forma de começar a utilizar as provas de conceito, os protótipos e a aprendizagem, mas para uma aplicação de qualidade de produção **não** deve utilizar este método. Deve utilizar alguma forma de implementação baseada em CI. Pode ler mais sobre como fazê-lo nos [documentos de Implementação de Funções do Azure](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment).
>
> [![Os amigos não deixam os amigos publicarem com o botão direito do rato](../media/8-friends-dont-let-friends-publish.png)](https://damianbrady.com.au/2018/02/01/friends-dont-let-friends-right-click-publish/)

## <a name="publishing-your-app-to-azure"></a>Publicar a sua aplicação no Azure

As funções do Azure podem ser publicadas no Azure a partir do Visual Studio.

1. Pare o runtime das funções do Azure local se ainda estiverem em execução na unidade anterior.

2. Clique com o botão direito do rato na aplicação `ImHere.Functions` no explorador e selecione *Publicar...*.

    ![Clique com o botão direito na aplicação de Funções](../media/8-right-click-publish.png)

3. Na caixa de diálogo **Escolher um destino da publicação**, selecione *Aplicação de Funções do Azure* e no **Serviço de Aplicações do Azure**, selecione *Criar Novo*. Clique em **Publicar**.

    ![Criar um novo Serviço de Aplicações do Azure para publicar](../media/8-pick-publish-target.png)

4. Selecione a sua conta do Azure na lista suspensa no canto superior direito se tiver mais de uma conta do Azure e não estiver selecionada a correta.

5. Dê um nome à sua aplicação de Funções. Este nome tem de ser globalmente exclusivo em todas as aplicações de Funções em todo o Azure, por isso utilize algo como "ImHere-\<YourName\>".

6. Selecione a subscrição com a qual pretende criar a aplicação de Funções.

7. Crie um novo grupo de recursos para esta aplicação de Funções, ao clicar no botão **Novo...** junto à lista pendente **Grupo de Recursos** e atribua um nome como "ImHere". Os nomes de grupo de recursos têm de ser exclusivos na sua subscrição, não globalmente exclusivos em todo o Azure. Em seguida, clique em **OK**.

    ![Criar um novo grupo de recursos](../media/8-create-new-resource-group.png)

   Criar um novo grupo de recursos facilita a limpeza posterior. Pode eliminar o grupo de recursos e saber que tudo o que criou para esta aplicação de Funções será eliminado ao mesmo tempo.

8. Crie um novo plano de alojamento ao clicar em **Novo...** junto à lista pendente **Plano de Alojamento**. O nome do plano do Serviço de Aplicações será predefinido para o nome da sua aplicação com "Plano" no final. Defina a **Localização** para a localização mais próxima para si e certifique-se de que o **Tamanho** está definido para consumo. Em seguida, clique em **OK**.

    ![Configurar o plano de alojamento](../media/8-configure-hosting-plan.png)

9. Crie uma nova conta de armazenamento ao clicar no botão **Novo...** junto à lista pendente **Conta de Armazenamento**. Será indicado um nome predefinido, pelo que deve manter todos os valores predefinidos e clicar em **OK**.

    ![Criar uma conta de armazenamento](../media/8-create-storage-account.png)

10. Clique em **Criar** para aprovisionar todos os recursos no Azure e publicar a sua aplicação de Funções do Azure.

    ![Criar o Serviço de Aplicações](../media/8-create-app-service.png)

O aprovisionamento irá demorar alguns minutos a executar. Serão aprovisionados os seguintes recursos:

* Uma conta de armazenamento para armazenar os ficheiros exigidos para a aplicação de Funções do Azure
* Um plano do Serviço de Aplicações para gerir os recursos de computação exigidos pela aplicação de Funções do Azure
* O Serviço de Aplicações que executa a função do Azure

A função será agora publicada e está disponível para chamar em https://<nome-da-sua-aplicação>.azurewebsites.net/api/SendLocation.

## <a name="configuring-your-app"></a>Configurar a sua aplicação

Quando a função do Azure estava a ser executada localmente, estava a utilizar credenciais do Twilio que estavam armazenadas num ficheiro `local.settings.json`. Como o nome sugere, este ficheiro destina-se a configurações locais, e não definições do Azure. Antes de a função do Azure poder ser chamada no Azure, as definições `TwilioAccountSid` e `TwilioAuthToken` têm de ser configuradas.

1. No separador Publicar, clique na opção **Gerir Definições da Aplicação**.

    ![A opção Gerir Definições da Aplicação](../media/8-application-settings-option.png)

2. Clique no botão **Adicionar** para adicionar uma nova definição. Dê-lhe o nome "TwilioAccountSid" e defina o valor para o seu SID da conta do Twilio. Repita este passo para o Token de Autenticação que utiliza o nome "TwilioAuthToken".

    ![Definir as credenciais do Twilio nas definições da aplicação](../media/8-set-creds-in-app-settings.png)

3. Clique em **OK**.

4. Clique em **Publicar** para voltar a publicar a aplicação de Funções do Azure com as novas definições de aplicação.

    ![O botão de publicação](../media/8-publish-application-button.png)

## <a name="pointing-the-mobile-app-to-azure"></a>Apontar a aplicação móvel para o Azure

1. No separador Publicar, copie o **URL do Site** com o botão de cópia junto ao valor.

    ![Copie o URL do site no separador de publicação](../media/8-copy-site-url.png)

2. Abra o `MainViewModel` a partir do projeto `ImHere`.

3. Atualize o valor do campo `baseUrl` para ser o URL do site copiado do separador Publicar.

4. Altere o protocolo para este valor de `http` para `https`. O URL do site é sempre dado com HTTP, mas tem de utilizar HTTPS para chamar uma função do Azure.

## <a name="test-it-out"></a>Teste

1. Defina a aplicação `ImHere.UWP` como a aplicação de arranque e execute-a.

2. Introduza um número de telefone e clique no botão **Enviar Localização**.

3. Deverá receber a localização como uma mensagem SMS.

## <a name="summary"></a>Resumo

Nesta unidade aprendeu a publicar um projeto de Funções do Azure para o Azure a partir do Visual Studio e a configurar as definições da aplicação.