Neste exercício, vamos continuar com o nosso exemplo de unidade de engrenagem e adicionar a lógica ao serviço de temperatura. Especificamente, vamos receber dados de um pedido HTTP.

## <a name="function-requirements"></a>Requisitos da função
Vamos definir alguns requisitos para a nossa lógica:
- temperaturas entre 0 e 25 devem ser sinalizadas como **OK**
- temperaturas entre 26 e 50 devem ser sinalizadas como **ATENÇÃO**
- temperaturas acima de 50 devem ser sinalizadas como **PERIGO**

## <a name="adding-a-function-to-an-azure-function-app"></a>Adicionar uma função a uma aplicação de funções do Azure

Como já aprendemos, o Azure pode ajudar quando está a aprender a trabalhar com o Azure Functions. Uma ótima funcionalidade para experimentar o Functions é gerar um com um dos muitos modelos. Neste exercício, irá utilizar o modelo do HttpTrigger para implementar o serviço de temperatura.

1. Inicie sessão no [portal do Azure](https://portal.azure.com) com a sua conta do Azure.
1. Aceda ao grupo de recursos que criou no primeiro exercício ao escolher **Todos os recursos** no menu do lado esquerdo e, em seguida, selecione **escalator-functions-group**.
1. Os recursos para o grupo serão, em seguida, apresentados. Aceda à aplicação de funções que criou no exercício anterior, ao selecionar o item **escalator-functions-xxxxxxx** (também indicado pelo ícone de relâmpago).
  ![Aceder à aplicação de funções](../images/6-access-function-app.png)
1. O painel irá mostrar uma descrição geral da sua aplicação de funções. Também há uma árvore de navegação à esquerda que mostra todas as funções, proxies ou ranhuras que estão definidos. Ainda não temos uma função, pelo que isto estará vazio. Para criar uma função, mova o rato sobre a **Função** na árvore de navegação e clique no botão **+** exibido.
  ![Adicionar navegação da função](../images/5-function-add-button.png)
1. No formulário de função pré-criada do início rápido, selecione a ligação **Função personalizada** na secção **Começar por si mesmo**.
  ![Formulário de função pré-criada](../images/6-custom-function.png)
1. Será apresentada uma lista de modelos. Selecione a implementação JavaScript do modelo de Acionador HTTP.
  ![Modelo de acionador HTTP](../images/6-httptrigger-template.png)
1. Será apresentado um painel, o que lhe permite definir o que o modelo irá gerar. Neste caso, está interessado em gerar uma função JavaScript chamada **DriveGearTemperatureService**. Depois de nomear a sua função, prima o botão **Criar**.
  ![Criar um formulário de acionador HTTP](../images/6-create-httptrigger-form.png)
1. Após alguns instantes, verá o código fonte com modelos para a função. A função pré-criada espera que um nome seja passado e irá devolver **Olá, {nome}**.

    ```javascript
    module.exports = function (context, req) {
        context.log('JavaScript HTTP trigger function processed a request.');

        if (req.query.name || (req.body && req.body.name)) {
            context.res = {
                // status: 200, /* Defaults to 200 */
                body: "Hello " + (req.query.name || req.body.name)
            };
        }
        else {
            context.res = {
                status: 400,
                body: "Please pass a name on the query string or in the request body"
            };
        }
        context.done();
    };
    ```

1. No lado direito da vista de origem, verá dois separadores. Pode ver todos os ficheiros que suportam a função no separador **Ver ficheiros**. Pode selecionar **function.json** para ver a configuração da função. Aqui pode ver o httpTrigger definido, bem como o enlace de saída. Esta configuração descreve que a função é iniciada através de um pedido HTTP e o enlace de saída descreve que a resposta será enviada como uma resposta HTTP.

    ```javascript
    {
      "disabled": false,
      "bindings": [
        {
          "authLevel": "function",
          "type": "httpTrigger",
          "direction": "in",
          "name": "req"
        },
        {
          "type": "http",
          "direction": "out",
          "name": "res"
        }
      ]
    }
    ```

## <a name="running-the-premade-azure-function"></a>Executar a função pré-criada do Azure

Para executar a função, pode iniciar um pedido HTTP de cURL numa linha de comandos. Para encontrar o URL do ponto final, regresse ao seu código de função e selecione a ligação **Obter URL de função**. Copie esta ligação para a área de transferência.  O URL deve ser algo semelhante ao seguinte: https://escalator-functions-xxxxxxx.azurewebsites.net/api/DriveGearTemperatureService?code=RMt1K0AfulJmF4Ui8OSNLXsI3AFjbHznS8BcJsinBox3nDEKEwy1sg== ![Obter URL de ponto final](../images/6-get-function-url.png)

Com esse URL, execute um comando cURL para iniciar a sua função (ao substituir o URL pelo seu):

```bash
curl --header "Content-Type: application/json" --request POST --data "{\"name\": \"Azure Function\"}" https://escalator-functions-xxxxxxx.azurewebsites.net/api/DriveGearTemperatureService?code=RMt1K0AfulJmF4Ui8OSNLXsI3AFjbHznS8BcJsinBox3nDEKEwy1sg==
```

![Resposta de cURL de função pré-criada](../images/6-premadefunction-curl.png)

## <a name="adding-business-logic-to-the-function"></a>Adicionar lógica de negócio à função

A nossa função espera uma matriz de leituras de temperatura do cliente. Este é um exemplo do corpo do pedido:

```javascript
{
    "readings": [
        {
            "driveGearId": 1,
            "timestamp": 1534263995,
            "temperature": 23
        },
        {
            "driveGearId": 3,
            "timestamp": 1534264048,
            "temperature": 45
        },
        {
            "driveGearId": 18,
            "timestamp": 1534264050,
            "temperature": 55
        }
    ]
}
```

Modifique o código de função pré-criada para implementar a lógica de negócio que é precisa. Abra o ficheiro index.js e substitua-o pela listagem a seguir:

```javascript
module.exports = function (context, req) {
    context.log('Drive Gear Temperature Service triggered');
    if (req.body && req.body.readings) {
        for(var i=0; i<req.body.readings.length; i++){
            var reading = req.body.readings[i];
            if(reading.temperature<=25){
                context.log('Reading is OK');
                reading.status = 'OK';
                continue;
            }
            if(reading.temperature<=50){
                context.log('Reading is CAUTION');
                reading.status = 'CAUTION';
                continue;
            }
            context.log('Reading is DANGER');
            reading.status = 'DANGER'
        }
        context.res = {
            // status: 200, /* Defaults to 200 */
            body: {
                "readings": req.body.readings
            }
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please send an array of readings in the request body"
        };
    }
    context.done();
};
```

Tenha em atenção às instruções de registo. Quando a função é executada, eles vão adicionar mensagens na janela de registo.

## <a name="testing-your-business-logic"></a>Testar a lógica de negócio

Abra a janela de teste no submenu do lado direito e cole o pedido de exemplo acima na caixa de texto do corpo de pedido. Prima o botão **Executar** e veja o resultado. Também pode abrir a janela de registo do submenu na parte inferior para ver as instruções de registo no registo.
![Testar Lógica de negócio](../images/6-portal-testing.png) Pode ver nos dados JSON na janela de saída que o nosso campo de estado de temperatura foi adicionado corretamente a cada uma das leituras. Também pode visitar o dashboard de Monitorização para ver que o pedido foi registado no Application Insights.
![Pedido no Application Insights](../images/6-app-insights.png)
