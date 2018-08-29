<span data-ttu-id="e26df-101">Neste exercício, vamos continuar com o nosso exemplo de unidade de engrenagem e adicionar a lógica ao serviço de temperatura.</span><span class="sxs-lookup"><span data-stu-id="e26df-101">In this exercise, we'll continue with our gear drive example and add the logic for the temperature service.</span></span> <span data-ttu-id="e26df-102">Especificamente, vamos receber dados de um pedido HTTP.</span><span class="sxs-lookup"><span data-stu-id="e26df-102">Specifically, we're going to receive data from an HTTP request.</span></span>

## <a name="function-requirements"></a><span data-ttu-id="e26df-103">Requisitos da função</span><span class="sxs-lookup"><span data-stu-id="e26df-103">Function requirements</span></span>
<span data-ttu-id="e26df-104">Vamos definir alguns requisitos para a nossa lógica:</span><span class="sxs-lookup"><span data-stu-id="e26df-104">Let's define some requirements for our logic:</span></span>
- <span data-ttu-id="e26df-105">temperaturas entre 0 e 25 devem ser sinalizadas como **OK**</span><span class="sxs-lookup"><span data-stu-id="e26df-105">temperatures between 0-25 should be flagged as **OK**</span></span>
- <span data-ttu-id="e26df-106">temperaturas entre 26 e 50 devem ser sinalizadas como **ATENÇÃO**</span><span class="sxs-lookup"><span data-stu-id="e26df-106">temperatures between 26-50 should be flagged as **CAUTION**</span></span>
- <span data-ttu-id="e26df-107">temperaturas acima de 50 devem ser sinalizadas como **PERIGO**</span><span class="sxs-lookup"><span data-stu-id="e26df-107">temperatures above 50 should be flagged as **DANGER**</span></span>

## <a name="adding-a-function-to-an-azure-function-app"></a><span data-ttu-id="e26df-108">Adicionar uma função a uma aplicação de funções do Azure</span><span class="sxs-lookup"><span data-stu-id="e26df-108">Adding a function to an Azure function app</span></span>

<span data-ttu-id="e26df-109">Como já aprendemos, o Azure pode ajudar quando está a aprender a trabalhar com o Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="e26df-109">As we have already learned, Azure provides a helping hand when you're learning how to work with Azure Functions.</span></span> <span data-ttu-id="e26df-110">Uma ótima funcionalidade para experimentar o Functions é gerar um com um dos muitos modelos.</span><span class="sxs-lookup"><span data-stu-id="e26df-110">One great feature to get your feet wet with Functions is to generate one using one of many templates.</span></span> <span data-ttu-id="e26df-111">Neste exercício, irá utilizar o modelo do HttpTrigger para implementar o serviço de temperatura.</span><span class="sxs-lookup"><span data-stu-id="e26df-111">In this exercise, you will be using the HttpTrigger template to implement the temperature service.</span></span>

1. <span data-ttu-id="e26df-112">Inicie sessão no [portal do Azure](https://portal.azure.com) com a sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="e26df-112">Sign in to the [Azure portal](https://portal.azure.com) using your Azure account.</span></span>
1. <span data-ttu-id="e26df-113">Aceda ao grupo de recursos que criou no primeiro exercício ao escolher **Todos os recursos** no menu do lado esquerdo e, em seguida, selecione **escalator-functions-group**.</span><span class="sxs-lookup"><span data-stu-id="e26df-113">Access the resource group you created in the first exercise by choosing **All resources** in the left-hand menu, and then selecting **escalator-functions-group**.</span></span>
1. <span data-ttu-id="e26df-114">Os recursos para o grupo serão, em seguida, apresentados.</span><span class="sxs-lookup"><span data-stu-id="e26df-114">The resources for the group will then be displayed.</span></span> <span data-ttu-id="e26df-115">Aceda à aplicação de funções que criou no exercício anterior, ao selecionar o item **escalator-functions-xxxxxxx** (também indicado pelo ícone de relâmpago).</span><span class="sxs-lookup"><span data-stu-id="e26df-115">Access the function app that you created in the previous exercise by selecting the **escalator-functions-xxxxxxx** item (also indicated by the lightning bolt icon).</span></span>
  <span data-ttu-id="e26df-116">![Aceder à aplicação de funções](../images/6-access-function-app.png)</span><span class="sxs-lookup"><span data-stu-id="e26df-116">![Access the function app](../images/6-access-function-app.png)</span></span>
1. <span data-ttu-id="e26df-117">O painel irá mostrar uma descrição geral da sua aplicação de funções.</span><span class="sxs-lookup"><span data-stu-id="e26df-117">The blade will show an overview of your function app.</span></span> <span data-ttu-id="e26df-118">Também há uma árvore de navegação à esquerda que mostra todas as funções, proxies ou ranhuras que estão definidos.</span><span class="sxs-lookup"><span data-stu-id="e26df-118">There is also a navigation tree on the left that shows any functions, proxies or slots that are defined.</span></span> <span data-ttu-id="e26df-119">Ainda não temos uma função, pelo que isto estará vazio.</span><span class="sxs-lookup"><span data-stu-id="e26df-119">We don't have a function yet, so this  will be empty.</span></span> <span data-ttu-id="e26df-120">Para criar uma função, mova o rato sobre a **Função** na árvore de navegação e clique no botão **+** exibido.</span><span class="sxs-lookup"><span data-stu-id="e26df-120">To create a function, move your mouse over **Function** in the navigation tree and click  the **+** button that appears.</span></span>
  <span data-ttu-id="e26df-121">![Adicionar navegação da função](../images/5-function-add-button.png)</span><span class="sxs-lookup"><span data-stu-id="e26df-121">![Add function navigation](../images/5-function-add-button.png)</span></span>
1. <span data-ttu-id="e26df-122">No formulário de função pré-criada do início rápido, selecione a ligação **Função personalizada** na secção **Começar por si mesmo**.</span><span class="sxs-lookup"><span data-stu-id="e26df-122">In the quickstart premade function form, select the **Custom function** link in the **Get started on your own** section.</span></span>
  <span data-ttu-id="e26df-123">![Formulário de função pré-criada](../images/6-custom-function.png)</span><span class="sxs-lookup"><span data-stu-id="e26df-123">![Premade function form](../images/6-custom-function.png)</span></span>
1. <span data-ttu-id="e26df-124">Será apresentada uma lista de modelos.</span><span class="sxs-lookup"><span data-stu-id="e26df-124">You are now presented with a list of templates.</span></span> <span data-ttu-id="e26df-125">Selecione a implementação JavaScript do modelo de Acionador HTTP.</span><span class="sxs-lookup"><span data-stu-id="e26df-125">Select the JavaScript implementation of the HTTP trigger template.</span></span>
  <span data-ttu-id="e26df-126">![Modelo de acionador HTTP](../images/6-httptrigger-template.png)</span><span class="sxs-lookup"><span data-stu-id="e26df-126">![HTTP trigger template](../images/6-httptrigger-template.png)</span></span>
1. <span data-ttu-id="e26df-127">Será apresentado um painel, o que lhe permite definir o que o modelo irá gerar.</span><span class="sxs-lookup"><span data-stu-id="e26df-127">A blade will appear, allowing you to define what the template will generate.</span></span> <span data-ttu-id="e26df-128">Neste caso, está interessado em gerar uma função JavaScript chamada **DriveGearTemperatureService**.</span><span class="sxs-lookup"><span data-stu-id="e26df-128">In this case, you are interested in generating a JavaScript function named **DriveGearTemperatureService**.</span></span> <span data-ttu-id="e26df-129">Depois de nomear a sua função, prima o botão **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e26df-129">After you have named your function, press the **Create** button.</span></span>
  <span data-ttu-id="e26df-130">![Criar um formulário de acionador HTTP](../images/6-create-httptrigger-form.png)</span><span class="sxs-lookup"><span data-stu-id="e26df-130">![Create HTTP trigger form](../images/6-create-httptrigger-form.png)</span></span>
1. <span data-ttu-id="e26df-131">Após alguns instantes, verá o código fonte com modelos para a função.</span><span class="sxs-lookup"><span data-stu-id="e26df-131">After a few moments, you will be presented with the templated source code for your function.</span></span> <span data-ttu-id="e26df-132">A função pré-criada espera que um nome seja passado e irá devolver **Olá, {nome}**.</span><span class="sxs-lookup"><span data-stu-id="e26df-132">The premade function expects a name to be passed in, and it will return **Hello, {name}**.</span></span>

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

1. <span data-ttu-id="e26df-133">No lado direito da vista de origem, verá dois separadores.</span><span class="sxs-lookup"><span data-stu-id="e26df-133">On the right-hand side of the source view, you will see two tabs.</span></span> <span data-ttu-id="e26df-134">Pode ver todos os ficheiros que suportam a função no separador **Ver ficheiros**. Pode selecionar **function.json** para ver a configuração da função.</span><span class="sxs-lookup"><span data-stu-id="e26df-134">You are able to view all the files supporting the function in the **View files** tab. You can select **function.json** to view the configuration of the function.</span></span> <span data-ttu-id="e26df-135">Aqui pode ver o httpTrigger definido, bem como o enlace de saída.</span><span class="sxs-lookup"><span data-stu-id="e26df-135">Here you can see the httpTrigger defined, as well as the output binding.</span></span> <span data-ttu-id="e26df-136">Esta configuração descreve que a função é iniciada através de um pedido HTTP e o enlace de saída descreve que a resposta será enviada como uma resposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="e26df-136">This configuration describes that the function is initiated by an HTTP request, and the output binding describes that the response will be sent as an HTTP response.</span></span>

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

## <a name="running-the-premade-azure-function"></a><span data-ttu-id="e26df-137">Executar a função pré-criada do Azure</span><span class="sxs-lookup"><span data-stu-id="e26df-137">Running the premade Azure function</span></span>

<span data-ttu-id="e26df-138">Para executar a função, pode iniciar um pedido HTTP de cURL numa linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="e26df-138">To run the function, you can initiate an HTTP request from cURL from a command prompt.</span></span> <span data-ttu-id="e26df-139">Para encontrar o URL do ponto final, regresse ao seu código de função e selecione a ligação **Obter URL de função**.</span><span class="sxs-lookup"><span data-stu-id="e26df-139">To find the endpoint URL, return to your function code and select the **Get function URL** link.</span></span> <span data-ttu-id="e26df-140">Copie esta ligação para a área de transferência.</span><span class="sxs-lookup"><span data-stu-id="e26df-140">Copy this link to your clipboard.</span></span>  <span data-ttu-id="e26df-141">O URL deve ser algo semelhante ao seguinte: https://escalator-functions-xxxxxxx.azurewebsites.net/api/DriveGearTemperatureService?code=RMt1K0AfulJmF4Ui8OSNLXsI3AFjbHznS8BcJsinBox3nDEKEwy1sg== ![Obter URL de ponto final](../images/6-get-function-url.png)</span><span class="sxs-lookup"><span data-stu-id="e26df-141">Your URL should look something similar to the following: https://escalator-functions-xxxxxxx.azurewebsites.net/api/DriveGearTemperatureService?code=RMt1K0AfulJmF4Ui8OSNLXsI3AFjbHznS8BcJsinBox3nDEKEwy1sg== ![Get endpoint URL](../images/6-get-function-url.png)</span></span>

<span data-ttu-id="e26df-142">Com esse URL, execute um comando cURL para iniciar a sua função (ao substituir o URL pelo seu):</span><span class="sxs-lookup"><span data-stu-id="e26df-142">With that URL, run a cURL command to initiate your function (replacing the URL with your own):</span></span>

```bash
curl --header "Content-Type: application/json" --request POST --data "{\"name\": \"Azure Function\"}" https://escalator-functions-xxxxxxx.azurewebsites.net/api/DriveGearTemperatureService?code=RMt1K0AfulJmF4Ui8OSNLXsI3AFjbHznS8BcJsinBox3nDEKEwy1sg==
```

![Resposta de cURL de função pré-criada](../images/6-premadefunction-curl.png)

## <a name="adding-business-logic-to-the-function"></a><span data-ttu-id="e26df-144">Adicionar lógica de negócio à função</span><span class="sxs-lookup"><span data-stu-id="e26df-144">Adding business logic to the function</span></span>

<span data-ttu-id="e26df-145">A nossa função espera uma matriz de leituras de temperatura do cliente.</span><span class="sxs-lookup"><span data-stu-id="e26df-145">Our function is expecting an array of temperature readings from the customer.</span></span> <span data-ttu-id="e26df-146">Este é um exemplo do corpo do pedido:</span><span class="sxs-lookup"><span data-stu-id="e26df-146">This is an example of the request body:</span></span>

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

<span data-ttu-id="e26df-147">Modifique o código de função pré-criada para implementar a lógica de negócio que é precisa.</span><span class="sxs-lookup"><span data-stu-id="e26df-147">Modify the premade function code to implement the required business logic.</span></span> <span data-ttu-id="e26df-148">Abra o ficheiro index.js e substitua-o pela listagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="e26df-148">Open the index.js file, and replace it with the following listing:</span></span>

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

<span data-ttu-id="e26df-149">Tenha em atenção às instruções de registo.</span><span class="sxs-lookup"><span data-stu-id="e26df-149">Notice the log statements.</span></span> <span data-ttu-id="e26df-150">Quando a função é executada, eles vão adicionar mensagens na janela de registo.</span><span class="sxs-lookup"><span data-stu-id="e26df-150">When the function runs, they will add messages in the log window.</span></span>

## <a name="testing-your-business-logic"></a><span data-ttu-id="e26df-151">Testar a lógica de negócio</span><span class="sxs-lookup"><span data-stu-id="e26df-151">Testing your business logic</span></span>

<span data-ttu-id="e26df-152">Abra a janela de teste no submenu do lado direito e cole o pedido de exemplo acima na caixa de texto do corpo de pedido.</span><span class="sxs-lookup"><span data-stu-id="e26df-152">Open the test window from the right-hand side flyout menu, and paste the sample request from above into the request body text box.</span></span> <span data-ttu-id="e26df-153">Prima o botão **Executar** e veja o resultado.</span><span class="sxs-lookup"><span data-stu-id="e26df-153">Press the **Run** button and view the output.</span></span> <span data-ttu-id="e26df-154">Também pode abrir a janela de registo do submenu na parte inferior para ver as instruções de registo no registo.</span><span class="sxs-lookup"><span data-stu-id="e26df-154">You can also open the log window from the bottom flyout menu to see the logging statements in the log.</span></span>
<span data-ttu-id="e26df-155">![Testar Lógica de negócio](../images/6-portal-testing.png) Pode ver nos dados JSON na janela de saída que o nosso campo de estado de temperatura foi adicionado corretamente a cada uma das leituras.</span><span class="sxs-lookup"><span data-stu-id="e26df-155">![Testing the business Logic](../images/6-portal-testing.png) You can see from the JSON data in the output window that our temperature status field has been added to each of the readings correctly.</span></span> <span data-ttu-id="e26df-156">Também pode visitar o dashboard de Monitorização para ver que o pedido foi registado no Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e26df-156">You may also visit the Monitor dashboard to see that the request has been logged to Application Insights.</span></span>
<span data-ttu-id="e26df-157">![Pedido no Application Insights](../images/6-app-insights.png)</span><span class="sxs-lookup"><span data-stu-id="e26df-157">![Request in Application Insights](../images/6-app-insights.png)</span></span>
