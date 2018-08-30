Neste exercício, vamos criar uma aplicação de funções do Azure.

1. Inicie sessão no [portal do Azure](https://portal.azure.com) com a sua conta do Azure.
1. Selecione o botão **Criar um recurso**, no canto superior esquerdo do portal do Azure, e, em seguida, **Computação > Aplicação de funções**.
  ![Criar o recurso da aplicação de funções](../images/4-create-function-app-blade.png)
1. Escolha um nome exclusivo globalmente para a aplicação. Este nome vai funcionar como o URL base do serviço. Pode atribuir o nome **escalator-functions-xxxxxxx**, em que os x podem ser substituídos pelas suas iniciais e pelo seu ano de nascimento. Se o nome não for exclusivo globalmente, poderá tentar qualquer outra combinação. Os carateres válidos são a-z, 0-9 e -.
1. Selecione a subscrição do Azure onde pretende alojar a aplicação de funções.
1. Crie um novo grupo de recursos chamado **escalator-functions-group**. Este procedimento ajudará na limpeza posteriormente.
1. Selecione **Windows** para o sistema operativo.
1. Em **Plano de Alojamento**, selecione o **Plano de Consumo**, para podermos tirar partido das funcionalidades do Azure sem servidor.
1. Selecione a localização geográfica mais próxima de si (ou dos seus clientes).
1. Crie uma nova conta de armazenamento e designe-a **escalatorfunctions**.
1. Verifique se o Azure Application Insights está **Ativado**e selecione a região mais próxima de si.
1. Selecione **Criar**; a implementação demora alguns minutos. Receberá uma notificação quando estiver concluída.
  ![Definições da aplicação de funções](../images/4-create-function-app-settings.png)

## <a name="verify-your-azure-function-app"></a>Verificar a aplicação de funções do Azure

1. No menu esquerdo do portal do Azure, selecione **Grupo de recursos**. Em seguida, deverá ver **escalator-functions-group** na lista de grupos disponíveis.
  ![Grupo de recursos](../images/4-resource-group.png)
1. Selecione **escalator-functions-group**. Em seguida, deverá ver uma lista de recursos semelhante à seguinte: ![Lista de recursos](../images/4-resource-list.png)
