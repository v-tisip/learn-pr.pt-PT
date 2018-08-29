Neste momento, a aplicação móvel está concluída e envia a localização do utilizador e a lista de números de telefone para uma função do Azure que pode anular a serialização dos dados. Nesta unidade, vai vincular a função do Azure ao Twilio para enviar mensagens SMS.

As Funções do Azure podem ser ligadas a outros serviços, sejam do Azure ou de terceiros. Estas ligações, denominadas enlaces, existem em duas formas: entrada e saída. Os enlaces de entrada fornecem dados à sua função e os enlaces de saída retiram os dados da sua função e enviam-nos para outro serviço. Pode ler sobre enlaces nos [documentos de Enlace de Funções do Azure](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings).

Os enlaces das Funções do Azure criados no Visual Studio são definidos através de parâmetros para a função, decorados com atributos.

## <a name="bind-the-azure-function-to-twilio"></a>Vincular a função do Azure ao Twilio

O envio de mensagens SMS através do Twilio requer um enlace de saída configurado com o ID da subscrição da sua conta (SID) e o Token de Autenticação.

1. Pare o runtime das funções do Azure local se ainda estiverem em execução na unidade anterior.

2. Adicione o pacote NuGet "Microsoft.Azure.WebJobs.Extensions.Twilio" ao projeto `ImHere.Functions`. Este pacote NuGet contém as classes relevantes para o enlace.

3. Adicione um novo parâmetro ao método `Run` na classe estática `SendLocation` denominada `messages`. Este parâmetro terá um tipo de `ICollector<SMSMessage>`. Terá de adicionar uma diretiva para o espaço de nomes `Twilio`.

    ```cs
    [FunctionName("SendLocation")]
    public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                                   "get", "post",
                                                                   Route = null)]HttpRequestMessage req,
                                                      ICollector<SMSMessage> messages,
                                                      TraceWriter log)
    ```

4. Decore o novo parâmetro `messages` com o atributo `TwilioSms`. Este atributo tem três parâmetros que tem de definir.

    | Definição      |  Valor   | Descrição                                        |
    | --- | --- | ---|
    | **AccountSidSetting** | "TwilioAccountSid" | O SID da sua conta do Twilio. Em vez de definir o SID diretamente, este parâmetro é o nome de um valor nas definições da aplicação de função que será utilizado para obter o SID. |
    | **AuthTokenSetting** | "TwilioAuthToken" | O Token de Autenticação para a sua conta do Twilio. Em vez de definir o Token de Autenticação diretamente, este parâmetro é o nome de um valor nas definições da aplicação de função que será utilizado para obter o Token de Autenticação. |
    | **De** | O número de telefone do Twilio | O número de telefone do Twilio a partir do qual serão enviadas as mensagens SMS em formato internacional (+\<indicativo do país\>\<número de telefone\>, por exemplo "+1555123456"). |

    Quando cria uma conta do Twilio, é-lhe atribuído um número de telefone que pode utilizar para enviar mensagens. Pode encontrar este número de telefone no dashboard **Phone Numbers** (Números de Telefone) do Twilio. A partir do site do Twilio, selecione as reticências na parte inferior do menu do lado esquerdo. Em seguida, selecione *SUPER NETWORK->Phone Numbers* (SUPER REDE->Números de Telefone). Pode afixar este dashboard ao menu do lado esquerdo através do ícone de alfinete. O seu número do Twilio estará em *Manage Numbers->Active Numbers* (Gerir Números->Números Ativos). Terá de remover todos os espaços do número.

    ![Localizar o número do Twilio](../media/7-twilio-find-number.png)

    ```cs
    [TwilioSms(AccountSidSetting = "TwilioAccountSid",
               AuthTokenSetting = "TwilioAuthToken",
               From = "+1xxxxxxxxx")]ICollector<SMSMessage> messages,
    ```

5. As definições da aplicação de função podem ser configuradas localmente no ficheiro `local.settings.json`. Adicione o SID da conta do Twilio e o Token de Autenticação a este ficheiro JSON com os nomes de definição que foram transmitidos ao atributo `TwilioSMS`.

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

    Substitua \<Your SID\> (O Seu SID) e \<Your Auth Token\> (O Seu Token de Autenticação) pelos valores do dashboard do Twilio.

    > Estas definições locais destinam-se apenas para execução localmente. Numa aplicação de produção, estes valores seriam as credenciais de desenvolvimento ou da conta de teste locais. Assim que a Função do Azure tiver sido implementada no Azure, poderá configurar os valores de produção.
    > Se introduzir o código no controlo de origem, estes valores de definição de aplicação local também serão introduzidos, por isso tenha cuidado para não introduzir os valores reais nesses ficheiros, caso o código seja aberto ou público de alguma forma.

## <a name="create-the-sms-messages"></a>Criar as mensagens SMS

O parâmetro `ICollector<SMSMessage>` é uma coleção de instâncias `SMSMessage` e é utilizado para recolher as mensagens SMS que deseja enviar. Depois de a execução da função estar concluída, todas as ocorrências de `SMSMessage` adicionadas a esta coleção são transmitidas ao Twilio e enviadas para os destinatários relevantes.

1. Na função `SendLocation`, adicione código ao ciclo através dos números de telefone em `PostData` e crie uma mensagem SMS para cada um deles.

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

    A mensagem precisa do número de telefone para onde será enviada e de um corpo com o URL do Google Maps criado a partir da localização do utilizador.

2. Registe cada mensagem e, em seguida, adicione-a à coleção `messages`.

    ```cs
    foreach (string toNo in data.ToNumbers)
    {
        ...
        log.Info($"Creating SMS message to {message.To}, message is '{message.Body}'.");
        messages.Add(message);
    }
    ```

O método `SendLocation` completo é mostrado abaixo.

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

## <a name="test-it-out"></a>Teste

1. Defina a aplicação `ImHere.Functions` como projeto de arranque e inicie-a sem depuração.

2. Defina a aplicação `ImHere.UWP` como projeto de arranque e execute-a.

3. Introduza o seu número de telefone em formato internacional (+\<indicativo do país\>\<número de telefone\>) na aplicação Xamarin.Forms. As contas de avaliação do Twilio apenas podem enviar mensagens para números de telefone verificados, por isso, por enquanto, apenas poderá enviar mensagens para si próprio, a menos que atualize para uma conta paga ou valide outros números.

4. Clique no botão **Enviar Localização**. Se a mensagem SMS foi enviada com êxito, verá uma mensagem na aplicação Xamarin.Forms a indicar que "A localização foi enviada com êxito".

    ![A aplicação Xamarin.Forms a mostrar a localização como enviada](../media/7-ui-location-sent.png)

5. Nos registos da consola da função do Azure, verá a mensagem a ser criada e enviada. Se ocorrerem erros (como o número estar no formato errado), estes serão registados aqui.

    ![A consola da função do Azure a mostrar que a mensagem foi enviada](../media/7-function-message-sent.png)

6. Consulte o seu telemóvel para verificar se recebeu uma mensagem. Siga a ligação na mensagem para ver a sua localização.

    ![A mensagem SMS recebida num telemóvel](../media/7-message-received.png)

## <a name="summary"></a>Resumo

Nesta unidade, aprendeu a criar um enlace com o Twilio para a função do Azure e a enviar uma mensagem SMS com a localização do utilizador para uma função que estava a ser executada localmente. Na unidade seguinte, vai publicar a função no Azure.