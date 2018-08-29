<span data-ttu-id="33f58-101">Neste momento, a aplicação móvel está concluída e envia a localização do utilizador e a lista de números de telefone para uma função do Azure que pode anular a serialização dos dados.</span><span class="sxs-lookup"><span data-stu-id="33f58-101">At this point, the mobile app is complete and sends the user's location and list of phone numbers to an Azure function that can deserialize the data.</span></span> <span data-ttu-id="33f58-102">Nesta unidade, vai vincular a função do Azure ao Twilio para enviar mensagens SMS.</span><span class="sxs-lookup"><span data-stu-id="33f58-102">In this unit, you bind the Azure function to Twilio to send SMS messages.</span></span>

<span data-ttu-id="33f58-103">As Funções do Azure podem ser ligadas a outros serviços, sejam do Azure ou de terceiros.</span><span class="sxs-lookup"><span data-stu-id="33f58-103">Azure Functions can be connected to other services, either services in Azure or third-party services.</span></span> <span data-ttu-id="33f58-104">Estas ligações, denominadas enlaces, existem em duas formas: entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="33f58-104">These connections, called bindings, exist in two forms - input and output bindings.</span></span> <span data-ttu-id="33f58-105">Os enlaces de entrada fornecem dados à sua função e os enlaces de saída retiram os dados da sua função e enviam-nos para outro serviço.</span><span class="sxs-lookup"><span data-stu-id="33f58-105">Input bindings provide data to your function and output bindings take data from your function and send it to another service.</span></span> <span data-ttu-id="33f58-106">Pode ler sobre enlaces nos [documentos de Enlace de Funções do Azure](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings).</span><span class="sxs-lookup"><span data-stu-id="33f58-106">You can read about bindings in the [Azure Functions Binding docs](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings).</span></span>

<span data-ttu-id="33f58-107">Os enlaces das Funções do Azure criados no Visual Studio são definidos através de parâmetros para a função, decorados com atributos.</span><span class="sxs-lookup"><span data-stu-id="33f58-107">Bindings for Azure Functions created in Visual Studio are defined using parameters to the function, decorated with attributes.</span></span>

## <a name="bind-the-azure-function-to-twilio"></a><span data-ttu-id="33f58-108">Vincular a função do Azure ao Twilio</span><span class="sxs-lookup"><span data-stu-id="33f58-108">Bind the Azure function to Twilio</span></span>

<span data-ttu-id="33f58-109">O envio de mensagens SMS através do Twilio requer um enlace de saída configurado com o ID da subscrição da sua conta (SID) e o Token de Autenticação.</span><span class="sxs-lookup"><span data-stu-id="33f58-109">Sending SMS messages via Twilio requires an output binding that is configured with your account subscription ID (SID) and Auth Token.</span></span>

1. <span data-ttu-id="33f58-110">Pare o runtime das funções do Azure local se ainda estiverem em execução na unidade anterior.</span><span class="sxs-lookup"><span data-stu-id="33f58-110">Stop the local Azure Functions runtime if it's still running from the previous unit.</span></span>

2. <span data-ttu-id="33f58-111">Adicione o pacote NuGet "Microsoft.Azure.WebJobs.Extensions.Twilio" ao projeto `ImHere.Functions`.</span><span class="sxs-lookup"><span data-stu-id="33f58-111">Add the "Microsoft.Azure.WebJobs.Extensions.Twilio" NuGet package to the `ImHere.Functions` project.</span></span> <span data-ttu-id="33f58-112">Este pacote NuGet contém as classes relevantes para o enlace.</span><span class="sxs-lookup"><span data-stu-id="33f58-112">This NuGet package contains the relevant classes for the binding.</span></span>

3. <span data-ttu-id="33f58-113">Adicione um novo parâmetro ao método `Run` na classe estática `SendLocation` denominada `messages`.</span><span class="sxs-lookup"><span data-stu-id="33f58-113">Add a new parameter to the static `Run` method on the `SendLocation` static class called `messages`.</span></span> <span data-ttu-id="33f58-114">Este parâmetro terá um tipo de `ICollector<SMSMessage>`.</span><span class="sxs-lookup"><span data-stu-id="33f58-114">This parameter will have a type of `ICollector<SMSMessage>`.</span></span> <span data-ttu-id="33f58-115">Terá de adicionar uma diretiva para o espaço de nomes `Twilio`.</span><span class="sxs-lookup"><span data-stu-id="33f58-115">You'll need to add a using directive for the `Twilio` namespace.</span></span>

    ```cs
    [FunctionName("SendLocation")]
    public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                                   "get", "post",
                                                                   Route = null)]HttpRequestMessage req,
                                                      ICollector<SMSMessage> messages,
                                                      TraceWriter log)
    ```

4. <span data-ttu-id="33f58-116">Decore o novo parâmetro `messages` com o atributo `TwilioSms`.</span><span class="sxs-lookup"><span data-stu-id="33f58-116">Decorate the new `messages` parameter with the `TwilioSms` attribute.</span></span> <span data-ttu-id="33f58-117">Este atributo tem três parâmetros que tem de definir.</span><span class="sxs-lookup"><span data-stu-id="33f58-117">This attribute has three parameters you need to set.</span></span>

    | <span data-ttu-id="33f58-118">Definição</span><span class="sxs-lookup"><span data-stu-id="33f58-118">Setting</span></span>      |  <span data-ttu-id="33f58-119">Valor</span><span class="sxs-lookup"><span data-stu-id="33f58-119">Value</span></span>   | <span data-ttu-id="33f58-120">Descrição</span><span class="sxs-lookup"><span data-stu-id="33f58-120">Description</span></span>                                        |
    | --- | --- | ---|
    | <span data-ttu-id="33f58-121">**AccountSidSetting**</span><span class="sxs-lookup"><span data-stu-id="33f58-121">**AccountSidSetting**</span></span> | <span data-ttu-id="33f58-122">"TwilioAccountSid"</span><span class="sxs-lookup"><span data-stu-id="33f58-122">"TwilioAccountSid"</span></span> | <span data-ttu-id="33f58-123">O SID da sua conta do Twilio.</span><span class="sxs-lookup"><span data-stu-id="33f58-123">The SID for your Twilio account.</span></span> <span data-ttu-id="33f58-124">Em vez de definir o SID diretamente, este parâmetro é o nome de um valor nas definições da aplicação de função que será utilizado para obter o SID.</span><span class="sxs-lookup"><span data-stu-id="33f58-124">Rather than set the SID directly, this parameter is the name of a value in the function app settings that will be used to retrieve the SID.</span></span> |
    | <span data-ttu-id="33f58-125">**AuthTokenSetting**</span><span class="sxs-lookup"><span data-stu-id="33f58-125">**AuthTokenSetting**</span></span> | <span data-ttu-id="33f58-126">"TwilioAuthToken"</span><span class="sxs-lookup"><span data-stu-id="33f58-126">"TwilioAuthToken"</span></span> | <span data-ttu-id="33f58-127">O Token de Autenticação para a sua conta do Twilio.</span><span class="sxs-lookup"><span data-stu-id="33f58-127">The Auth Token for your Twilio account.</span></span> <span data-ttu-id="33f58-128">Em vez de definir o Token de Autenticação diretamente, este parâmetro é o nome de um valor nas definições da aplicação de função que será utilizado para obter o Token de Autenticação.</span><span class="sxs-lookup"><span data-stu-id="33f58-128">Rather than set the Auth Token directly, this parameter is the name of a value in the function app settings that will be used to retrieve the Auth Token.</span></span> |
    | <span data-ttu-id="33f58-129">**De**</span><span class="sxs-lookup"><span data-stu-id="33f58-129">**From**</span></span> | <span data-ttu-id="33f58-130">O número de telefone do Twilio</span><span class="sxs-lookup"><span data-stu-id="33f58-130">Your Twilio phone number</span></span> | <span data-ttu-id="33f58-131">O número de telefone do Twilio a partir do qual serão enviadas as mensagens SMS em formato internacional (+\<indicativo do país\>\<número de telefone\>, por exemplo "+1555123456").</span><span class="sxs-lookup"><span data-stu-id="33f58-131">The Twilio phone number that the SMS messages will come from in international format (+\<country code\>\<phone number\>, for example "+1555123456").</span></span> |

    <span data-ttu-id="33f58-132">Quando cria uma conta do Twilio, é-lhe atribuído um número de telefone que pode utilizar para enviar mensagens.</span><span class="sxs-lookup"><span data-stu-id="33f58-132">When you create a Twilio account, you are assigned a phone number that you can send messages from.</span></span> <span data-ttu-id="33f58-133">Pode encontrar este número de telefone no dashboard **Phone Numbers** (Números de Telefone) do Twilio.</span><span class="sxs-lookup"><span data-stu-id="33f58-133">You can find this phone number on the Twilio **Phone Numbers** dashboard.</span></span> <span data-ttu-id="33f58-134">A partir do site do Twilio, selecione as reticências na parte inferior do menu do lado esquerdo.</span><span class="sxs-lookup"><span data-stu-id="33f58-134">From the Twilio site, select the ellipses at the bottom of the left-hand menu.</span></span> <span data-ttu-id="33f58-135">Em seguida, selecione *SUPER NETWORK->Phone Numbers* (SUPER REDE->Números de Telefone).</span><span class="sxs-lookup"><span data-stu-id="33f58-135">Then, select *SUPER NETWORK->Phone Numbers*.</span></span> <span data-ttu-id="33f58-136">Pode afixar este dashboard ao menu do lado esquerdo através do ícone de alfinete.</span><span class="sxs-lookup"><span data-stu-id="33f58-136">You can pin this dashboard to the left-hand menu using the pin icon.</span></span> <span data-ttu-id="33f58-137">O seu número do Twilio estará em *Manage Numbers->Active Numbers* (Gerir Números->Números Ativos).</span><span class="sxs-lookup"><span data-stu-id="33f58-137">Your Twilio number will be under *Manage Numbers->Active Numbers*.</span></span> <span data-ttu-id="33f58-138">Terá de remover todos os espaços do número.</span><span class="sxs-lookup"><span data-stu-id="33f58-138">You'll need to remove any spaces from the number.</span></span>

    ![Localizar o número do Twilio](../media/7-twilio-find-number.png)

    ```cs
    [TwilioSms(AccountSidSetting = "TwilioAccountSid",
               AuthTokenSetting = "TwilioAuthToken",
               From = "+1xxxxxxxxx")]ICollector<SMSMessage> messages,
    ```

5. <span data-ttu-id="33f58-140">As definições da aplicação de função podem ser configuradas localmente no ficheiro `local.settings.json`.</span><span class="sxs-lookup"><span data-stu-id="33f58-140">Function app settings can be configured locally inside the `local.settings.json` file.</span></span> <span data-ttu-id="33f58-141">Adicione o SID da conta do Twilio e o Token de Autenticação a este ficheiro JSON com os nomes de definição que foram transmitidos ao atributo `TwilioSMS`.</span><span class="sxs-lookup"><span data-stu-id="33f58-141">Add your Twilio account SID and Auth Token to this JSON file using the setting names that were passed to the `TwilioSMS` attribute.</span></span>

    ```json
    {
        "IsEncrypted": false,
        "Values": {
            "AzureWebJobsStorage": "UseDevelopmentStorage=true",
            "AzureWebJobsDashboard": "UseDevelopmentStorage=true",
            "TwilioAccountSid": "<Your SID>",
            "TwilioAuthToken": "<Your Auth Token>"
        }
    }
    ```

    <span data-ttu-id="33f58-142">Substitua \<Your SID\> (O Seu SID) e \<Your Auth Token\> (O Seu Token de Autenticação) pelos valores do dashboard do Twilio.</span><span class="sxs-lookup"><span data-stu-id="33f58-142">Replace \<Your SID\> and \<Your Auth Token\> with the values from your Twilio dashboard.</span></span>

    > <span data-ttu-id="33f58-143">Estas definições locais destinam-se apenas para execução localmente.</span><span class="sxs-lookup"><span data-stu-id="33f58-143">These local settings will be only for running locally.</span></span> <span data-ttu-id="33f58-144">Numa aplicação de produção, estes valores seriam as credenciais de desenvolvimento ou da conta de teste locais.</span><span class="sxs-lookup"><span data-stu-id="33f58-144">In a production app, these value would be your local development or test account credentials.</span></span> <span data-ttu-id="33f58-145">Assim que a Função do Azure tiver sido implementada no Azure, poderá configurar os valores de produção.</span><span class="sxs-lookup"><span data-stu-id="33f58-145">Once the Azure Function has been deployed to Azure, you'll be able to configure the production values.</span></span>
    > <span data-ttu-id="33f58-146">Se introduzir o código no controlo de origem, estes valores de definição de aplicação local também serão introduzidos, por isso tenha cuidado para não introduzir os valores reais nesses ficheiros, caso o código seja aberto ou público de alguma forma.</span><span class="sxs-lookup"><span data-stu-id="33f58-146">If you check your code into source control, these local application setting values will be checked in, too, so be careful not to check in any actual values in these files if your code is open source or public in any form.</span></span>

## <a name="create-the-sms-messages"></a><span data-ttu-id="33f58-147">Criar as mensagens SMS</span><span class="sxs-lookup"><span data-stu-id="33f58-147">Create the SMS messages</span></span>

<span data-ttu-id="33f58-148">O parâmetro `ICollector<SMSMessage>` é uma coleção de instâncias `SMSMessage` e é utilizado para recolher as mensagens SMS que deseja enviar.</span><span class="sxs-lookup"><span data-stu-id="33f58-148">The `ICollector<SMSMessage>` parameter is a collection of `SMSMessage` instances and is used to collect the SMS messages you want to send.</span></span> <span data-ttu-id="33f58-149">Depois de a execução da função estar concluída, todas as ocorrências de `SMSMessage` adicionadas a esta coleção são transmitidas ao Twilio e enviadas para os destinatários relevantes.</span><span class="sxs-lookup"><span data-stu-id="33f58-149">After the function has finished running, any instances of `SMSMessage` added to this collection are passed to Twilio and sent to the relevant recipients.</span></span>

1. <span data-ttu-id="33f58-150">Na função `SendLocation`, adicione código ao ciclo através dos números de telefone em `PostData` e crie uma mensagem SMS para cada um deles.</span><span class="sxs-lookup"><span data-stu-id="33f58-150">In the `SendLocation` function, add code to loop through the phone numbers in the `PostData` and create an SMS message for each one.</span></span>

    ```cs
    foreach (string toNo in data.ToNumbers)
    {
        SMSMessage message = new SMSMessage
        {
            Body = $"I'm here! {url}",
            To = toNo
        };
    }
    ```

    <span data-ttu-id="33f58-151">A mensagem precisa do número de telefone para onde será enviada e de um corpo com o URL do Google Maps criado a partir da localização do utilizador.</span><span class="sxs-lookup"><span data-stu-id="33f58-151">The message needs the phone number to send to and a body that contains the Google Maps URL created from the user's location.</span></span>

2. <span data-ttu-id="33f58-152">Registe cada mensagem e, em seguida, adicione-a à coleção `messages`.</span><span class="sxs-lookup"><span data-stu-id="33f58-152">Log each message, and then add it to the `messages` collection.</span></span>

    ```cs
    foreach (string toNo in data.ToNumbers)
    {
        ...
        log.Info($"Creating SMS message to {message.To}, message is '{message.Body}'.");
        messages.Add(message);
    }
    ```

<span data-ttu-id="33f58-153">O método `SendLocation` completo é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="33f58-153">The complete `SendLocation` method is shown below.</span></span>

```cs
[FunctionName("SendLocation")]
public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                                "get", "post",
                                                                Route = null)]HttpRequestMessage req,
                                                    [TwilioSms(AccountSidSetting = "TwilioAccountSid",
                                                                AuthTokenSetting = "TwilioAuthToken",
                                                                From = "<your Twilio phone number>")]ICollector<SMSMessage> messages,
                                                    TraceWriter log)
{
    log.Info("C# HTTP trigger function processed a request.");
    PostData data = await req.Content.ReadAsAsync<PostData>();
    string url = $"https://www.google.com/maps/search/?api=1&query={data.Latitude},{data.Longitude}";
    log.Info($"URL created - {url}");
    foreach (string toNo in data.ToNumbers)
    {
        SMSMessage message = new SMSMessage
        {
            Body = $"I'm here! {url}",
            To = toNo
        };
        log.Info($"Creating SMS message to {message.To}, message is '{message.Body}'.");
        messages.Add(message);
    }
    return req.CreateResponse(HttpStatusCode.OK);
}
```

## <a name="test-it-out"></a><span data-ttu-id="33f58-154">Teste</span><span class="sxs-lookup"><span data-stu-id="33f58-154">Test it out</span></span>

1. <span data-ttu-id="33f58-155">Defina a aplicação `ImHere.Functions` como projeto de arranque e inicie-a sem depuração.</span><span class="sxs-lookup"><span data-stu-id="33f58-155">Set the `ImHere.Functions` app as the startup project and start it without debugging.</span></span>

2. <span data-ttu-id="33f58-156">Defina a aplicação `ImHere.UWP` como projeto de arranque e execute-a.</span><span class="sxs-lookup"><span data-stu-id="33f58-156">Set the `ImHere.UWP` app as the startup project and run it.</span></span>

3. <span data-ttu-id="33f58-157">Introduza o seu número de telefone em formato internacional (+\<indicativo do país\>\<número de telefone\>) na aplicação Xamarin.Forms.</span><span class="sxs-lookup"><span data-stu-id="33f58-157">Enter your own phone number in international format (+\<country code\>\<phone number\>) into the Xamarin.Forms app.</span></span> <span data-ttu-id="33f58-158">As contas de avaliação do Twilio apenas podem enviar mensagens para números de telefone verificados, por isso, por enquanto, apenas poderá enviar mensagens para si próprio, a menos que atualize para uma conta paga ou valide outros números.</span><span class="sxs-lookup"><span data-stu-id="33f58-158">Twilio trial accounts can send  messages only to verified phone numbers, so for now, you'll only be able to message yourself unless you upgrade to a paid account or verify other numbers.</span></span>

4. <span data-ttu-id="33f58-159">Clique no botão **Enviar Localização**.</span><span class="sxs-lookup"><span data-stu-id="33f58-159">Click the **Send Location** button.</span></span> <span data-ttu-id="33f58-160">Se a mensagem SMS foi enviada com êxito, verá uma mensagem na aplicação Xamarin.Forms a indicar que "A localização foi enviada com êxito".</span><span class="sxs-lookup"><span data-stu-id="33f58-160">If the SMS message was sent successfully, you'll see a message in the Xamarin.Forms app saying "Location sent successfully".</span></span>

    ![A aplicação Xamarin.Forms a mostrar a localização como enviada](../media/7-ui-location-sent.png)

5. <span data-ttu-id="33f58-162">Nos registos da consola da função do Azure, verá a mensagem a ser criada e enviada.</span><span class="sxs-lookup"><span data-stu-id="33f58-162">In the console logs for the Azure function, you'll see the message being created and sent.</span></span> <span data-ttu-id="33f58-163">Se ocorrerem erros (como o número estar no formato errado), estes serão registados aqui.</span><span class="sxs-lookup"><span data-stu-id="33f58-163">If any errors occur (such as, the number is in the wrong format), they will be logged out here.</span></span>

    ![A consola da função do Azure a mostrar que a mensagem foi enviada](../media/7-function-message-sent.png)

6. <span data-ttu-id="33f58-165">Consulte o seu telemóvel para verificar se recebeu uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="33f58-165">Check your phone for a message.</span></span> <span data-ttu-id="33f58-166">Siga a ligação na mensagem para ver a sua localização.</span><span class="sxs-lookup"><span data-stu-id="33f58-166">Follow the link in the message to see your location.</span></span>

    ![A mensagem SMS recebida num telemóvel](../media/7-message-received.png)

## <a name="summary"></a><span data-ttu-id="33f58-168">Resumo</span><span class="sxs-lookup"><span data-stu-id="33f58-168">Summary</span></span>

<span data-ttu-id="33f58-169">Nesta unidade, aprendeu a criar um enlace com o Twilio para a função do Azure e a enviar uma mensagem SMS com a localização do utilizador para uma função que estava a ser executada localmente.</span><span class="sxs-lookup"><span data-stu-id="33f58-169">In this unit, you learned how to create a Twilio binding for the Azure function and send an SMS message with the user's location to a function that was running locally.</span></span> <span data-ttu-id="33f58-170">Na unidade seguinte, vai publicar a função no Azure.</span><span class="sxs-lookup"><span data-stu-id="33f58-170">In the next unit, you publish the function to Azure.</span></span>