<span data-ttu-id="e392f-101">Neste momento, a aplicação está a trabalhar para obter a localização do utilizador e está pronta para ser enviada para uma função do Azure.</span><span class="sxs-lookup"><span data-stu-id="e392f-101">At this point, the app is working to get the user's location and is ready to be sent to an Azure function.</span></span> <span data-ttu-id="e392f-102">Nesta unidade, vai criar a função do Azure.</span><span class="sxs-lookup"><span data-stu-id="e392f-102">In this unit, you build the Azure function.</span></span>

## <a name="create-an-azure-functions-project"></a><span data-ttu-id="e392f-103">Criar um projeto das Funções do Azure</span><span class="sxs-lookup"><span data-stu-id="e392f-103">Create an Azure Functions project</span></span>

1. <span data-ttu-id="e392f-104">Adicione um novo projeto à solução `ImHere` ao clicar com o botão direito do rato na solução e selecione *Adicionar->Novo Projeto...*.</span><span class="sxs-lookup"><span data-stu-id="e392f-104">Add a new project to the `ImHere` solution by right-clicking on the solution and selecting *Add->New Project...*.</span></span>

2. <span data-ttu-id="e392f-105">Na árvore do lado esquerdo, selecione *Visual C#->Cloud* e, em seguida, selecione *Funções do Azure* no painel do centro.</span><span class="sxs-lookup"><span data-stu-id="e392f-105">From the tree on the left-hand side, select *Visual C#->Cloud*, and then select *Azure Functions* from the panel in the center.</span></span>

3. <span data-ttu-id="e392f-106">Nomeie o projeto "ImHere.Functions" e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="e392f-106">Name the project "ImHere.Functions", and then click **OK**.</span></span>

    ![A caixa de diálogo Adicionar Novo Projeto](../media/5-add-new-functions-project.png)

4. <span data-ttu-id="e392f-108">Na caixa de diálogo de configuração **Novo Projeto**, deixe a versão das Funções definida como *Funções do Azure v1 (.NET Framework)*.</span><span class="sxs-lookup"><span data-stu-id="e392f-108">In the **New Project** configuration dialog, leave the Functions version set to *Azure Functions v1 (.NET Framework)*.</span></span> <span data-ttu-id="e392f-109">Selecione *Acionador Http*, deixe a conta de armazenamento definida como *Emulador de Armazenamento* e defina os direitos de acesso para *Anónimo*.</span><span class="sxs-lookup"><span data-stu-id="e392f-109">Select *Http Trigger*, leave the storage account set to *Storage Emulator*, and set the access rights to *Anonymous*.</span></span> <span data-ttu-id="e392f-110">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="e392f-110">Then click **OK**.</span></span>

    ![A caixa de diálogo de configuração de projeto da Função do Azure](../media/5-configure-trigger.png)

<span data-ttu-id="e392f-112">O novo projeto será criado e tem uma função predefinida denominada `Function1`.</span><span class="sxs-lookup"><span data-stu-id="e392f-112">The new project will be created and have a default function called `Function1`.</span></span>

> <span data-ttu-id="e392f-113">Esta função foi criada com acesso anónimo.</span><span class="sxs-lookup"><span data-stu-id="e392f-113">This function was created with anonymous access.</span></span> <span data-ttu-id="e392f-114">Depois de estar publicado no Azure, qualquer pessoa que conhece o URL poderá chamar esta função.</span><span class="sxs-lookup"><span data-stu-id="e392f-114">Once published to Azure, anybody who knows the URL will be able to call this function.</span></span> <span data-ttu-id="e392f-115">Num cenário do mundo real, teria de proteger isto com algum tipo de autenticação, como a [autenticação do Serviço de Aplicações do Azure](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview) ou o [Azure Active Directory B2C](https://docs.microsoft.com/azure/active-directory-b2c).</span><span class="sxs-lookup"><span data-stu-id="e392f-115">In a real-world scenario, you would protect this with some form of authentication, such as [Azure App Service authentication](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview) or [Azure Active Directory B2C](https://docs.microsoft.com/azure/active-directory-b2c).</span></span>

## <a name="create-the-function"></a><span data-ttu-id="e392f-116">Criar a função</span><span class="sxs-lookup"><span data-stu-id="e392f-116">Create the function</span></span>

<span data-ttu-id="e392f-117">O projeto das Funções do Azure é criado com uma única função de acionador HTTP chamada `Function1`.</span><span class="sxs-lookup"><span data-stu-id="e392f-117">The Azure Functions project is created with a single HTTP trigger function called `Function1`.</span></span> <span data-ttu-id="e392f-118">A função em si é implementada como um método `Run` estático na classe `Function1`.</span><span class="sxs-lookup"><span data-stu-id="e392f-118">The function itself is implemented as a static `Run` method in the `Function1` class.</span></span>

1. <span data-ttu-id="e392f-119">Renomeie o ficheiro no Explorador de Soluções de "Function1.cs" para "SendLocation.cs".</span><span class="sxs-lookup"><span data-stu-id="e392f-119">Rename the file in Solution Explorer from "Function1.cs" to "SendLocation.cs".</span></span> <span data-ttu-id="e392f-120">Quando lhe for pedido para mudar o nome de todas as referências do elemento de código `Function1`, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="e392f-120">When prompted to rename all references to the code element `Function1`, click **Yes**.</span></span>

2. <span data-ttu-id="e392f-121">Mude o nome da função no atributo para "SendLocation".</span><span class="sxs-lookup"><span data-stu-id="e392f-121">Rename the function name in the attribute to "SendLocation".</span></span>

    ```cs
    [FunctionName("SendLocation")]
    ```

3. <span data-ttu-id="e392f-122">Elimine o conteúdo da função, exceto a primeira linha que escreve uma mensagem de informações no logger.</span><span class="sxs-lookup"><span data-stu-id="e392f-122">Delete the contents of the function, except the first line that writes an information message to the logger.</span></span>

    ```cs
    public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                                   "get", "post",
                                                                   Route = null)]HttpRequestMessage req,
                                                       TraceWriter log)
    {
        log.Info("C# HTTP trigger function processed a request.");
    }
    ```

## <a name="create-a-class-to-share-data-between-the-mobile-app-and-function"></a><span data-ttu-id="e392f-123">Crie uma classe para partilhar dados entre a aplicação móvel e a função</span><span class="sxs-lookup"><span data-stu-id="e392f-123">Create a class to share data between the mobile app and function</span></span>

<span data-ttu-id="e392f-124">Quando os dados são enviados para a função do Azure, serão enviados como JSON.</span><span class="sxs-lookup"><span data-stu-id="e392f-124">When data is sent to the Azure function, it will be sent as JSON.</span></span> <span data-ttu-id="e392f-125">A aplicação móvel vai serializar dados no JSON e a função vai anular a serialização do JSON.</span><span class="sxs-lookup"><span data-stu-id="e392f-125">The mobile app will serialize data into JSON and the function will deserialize from JSON.</span></span> <span data-ttu-id="e392f-126">Para manter estes dados consistentes entre a aplicação móvel e a função, crie um novo projeto que contém uma classe para manter a localização e os dados do número de telefone.</span><span class="sxs-lookup"><span data-stu-id="e392f-126">To keep this data consistent between the mobile app and the function, create a new project that contains a class to hold the location and phone number data.</span></span> <span data-ttu-id="e392f-127">Este projeto será, em seguida, referenciado pela aplicação e pela função.</span><span class="sxs-lookup"><span data-stu-id="e392f-127">This project will then be referenced by the app and function.</span></span>

1. <span data-ttu-id="e392f-128">Crie um novo projeto sob a solução `ImHere` ao clicar com o botão direito do rato na solução e selecionar *Adicionar->Novo Projeto...*.</span><span class="sxs-lookup"><span data-stu-id="e392f-128">Create a new project under the `ImHere` solution by right-clicking on the solution and selecting *Add->New Project...*.</span></span>

2. <span data-ttu-id="e392f-129">Na árvore do lado esquerdo, selecione *Visual C#->.NET Standard* e, em seguida, selecione *Biblioteca de Classes (.NET Standard)* no painel do centro.</span><span class="sxs-lookup"><span data-stu-id="e392f-129">From the tree on the left-hand side, select *Visual C#->.NET Standard*, and then select *Class Library (.NET Standard)* from the panel in the center.</span></span>

3. <span data-ttu-id="e392f-130">Nomeie o projeto "ImHere.Data" e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="e392f-130">Name the project "ImHere.Data", and then click **OK**.</span></span>

    ![A caixa de diálogo Adicionar Novo Projeto](../media/5-add-new-net-standard-project.png)

4. <span data-ttu-id="e392f-132">Elimine o ficheiro "Class1.cs" gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e392f-132">Delete the auto-generated "Class1.cs" file.</span></span>

5. <span data-ttu-id="e392f-133">Crie uma nova classe no projeto `ImHere.Data` chamada `PostData` ao clicar com o botão direito do rato no projeto e, em seguida, selecione *Adicionar->Classe...* . Nomeie a nova classe "PostData" e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="e392f-133">Create a new class in the `ImHere.Data` project called `PostData` by right-clicking on the project and then selecting *Add->Class...*. Name the new class "PostData" and click **OK**.</span></span>

6. <span data-ttu-id="e392f-134">Adicione as propriedades `double` para a latitude e a longitude, bem como uma propriedade `string[]` para os números de telefone a enviar.</span><span class="sxs-lookup"><span data-stu-id="e392f-134">Add `double` properties for the latitude and longitude, as well as a `string[]` property for the phone numbers to send to.</span></span>

    ```cs
    public class PostData
    {
        public double Latitude { get; set; }
        public double Longitude { get; set; }
        public string[] ToNumbers { get; set; }
    }
    ```

7. <span data-ttu-id="e392f-135">Adicione uma referência a este projeto para os projetos `ImHere.Functions` e `ImHere` ao clicar com o botão direito do rato no projeto e, em seguida, selecione *Adicionar->Referência...* . Selecione *Projetos* na árvore do lado esquerdo e, em seguida, assinale a caixa junto a *ImHere.Data*.</span><span class="sxs-lookup"><span data-stu-id="e392f-135">Add a reference to this project to both the `ImHere.Functions` and `ImHere` projects by right-clicking on the project and then selecting *Add->Reference...*. Select *Projects* from the tree on the left-hand side, and then check the box next to *ImHere.Data*.</span></span>

    ![Configurar referências do projeto](../media/5-configure-project-references.png)

## <a name="read-the-data-sent-to-the-function"></a><span data-ttu-id="e392f-137">Ler os dados enviados para a função</span><span class="sxs-lookup"><span data-stu-id="e392f-137">Read the data sent to the function</span></span>

<span data-ttu-id="e392f-138">Na função do Azure, o parâmetro `req` contém o pedido HTTP que foi feito e os dados contidos neste pedido serão um objeto `PostData` serializado JSON.</span><span class="sxs-lookup"><span data-stu-id="e392f-138">In the Azure function, the `req` parameter contains the HTTP request that was made and the data inside this request will be a JSON serialized `PostData` object.</span></span>

1. <span data-ttu-id="e392f-139">Abra a classe `SendLocation` no projeto `ImHere.Functions`.</span><span class="sxs-lookup"><span data-stu-id="e392f-139">Open the `SendLocation` class in the `ImHere.Functions` project.</span></span>

2. <span data-ttu-id="e392f-140">Leia o conteúdo do pedido HTTP para um objeto `PostData`, ao adicionar uma diretiva em utilização para o espaço de nomes `ImHere.Data`.</span><span class="sxs-lookup"><span data-stu-id="e392f-140">Read the contents of the HTTP request into a `PostData` object, adding a using directive for the `ImHere.Data` namespace.</span></span>

    ```cs
    PostData data = await req.Content.ReadAsAsync<PostData>();
    ```

3. <span data-ttu-id="e392f-141">Construa um URL do Google Maps com a latitude e a longitude a partir de `PostData`.</span><span class="sxs-lookup"><span data-stu-id="e392f-141">Construct a Google Maps URL using the latitude and longitude from the `PostData`.</span></span>

   ```cs
   string url = $"https://www.google.com/maps/search/?api=1&query={data.Latitude},{data.Longitude}";
   ```

4. <span data-ttu-id="e392f-142">Registe o URL.</span><span class="sxs-lookup"><span data-stu-id="e392f-142">Log the URL.</span></span>

    ```cs
    log.Info($"URL created - {url}");
    ```

5. <span data-ttu-id="e392f-143">Devolva um código de estado 200 para mostrar a função que foi concluída sem erros.</span><span class="sxs-lookup"><span data-stu-id="e392f-143">Return a 200 status code to show the function completed without error.</span></span>

    ```cs
    return req.CreateResponse(HttpStatusCode.OK);
    ```

<span data-ttu-id="e392f-144">A função concluída é mostrada abaixo.</span><span class="sxs-lookup"><span data-stu-id="e392f-144">The complete function is shown below.</span></span>

```cs
public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                                "get", "post",
                                                                Route = null)]HttpRequestMessage req,
                                                    TraceWriter log)
{
    log.Info("C# HTTP trigger function processed a request.");
    PostData data = await req.Content.ReadAsAsync<PostData>();
    string url = $"https://www.google.com/maps/search/?api=1&query={data.Latitude},{data.Longitude}";
    log.Info($"URL created - {url}");
    return req.CreateResponse(HttpStatusCode.OK);
}
```

## <a name="run-the-azure-function-locally"></a><span data-ttu-id="e392f-145">Executar a função do Azure localmente</span><span class="sxs-lookup"><span data-stu-id="e392f-145">Run the Azure function locally</span></span>

<span data-ttu-id="e392f-146">As funções podem ser executadas localmente com uma conta de armazenamento local e o runtime das Funções do Azure local.</span><span class="sxs-lookup"><span data-stu-id="e392f-146">Functions can be run locally using a local storage account and local Azure Functions runtime.</span></span> <span data-ttu-id="e392f-147">Este runtime local permite-lhe testar a sua função antes de o implementar no Azure.</span><span class="sxs-lookup"><span data-stu-id="e392f-147">This local runtime allows you to test out your function before deploying it to Azure.</span></span>

1. <span data-ttu-id="e392f-148">Clique com o botão direito do rato no projeto `ImHere.Functions` no explorador de soluções e, em seguida, selecione *Configurar como Projeto de Arranque*.</span><span class="sxs-lookup"><span data-stu-id="e392f-148">Right-click on the `ImHere.Functions` project in the solution explorer, and then select *Set as StartUp project*.</span></span>

2. <span data-ttu-id="e392f-149">No menu *Depurar*, selecione *Iniciar Sem Depuração*.</span><span class="sxs-lookup"><span data-stu-id="e392f-149">From the *Debug* menu, select *Start Without Debugging*.</span></span> <span data-ttu-id="e392f-150">O runtime local das Funções do Azure será lançado dentro de uma janela de consola e irá iniciar a sua função, ao escutar numa porta disponível no `localhost`.</span><span class="sxs-lookup"><span data-stu-id="e392f-150">The local Azure Functions runtime will launch inside a console window and start your function, listening on an available port on `localhost`.</span></span>

    ![A função do Azure em execução localmente](../media/5-function-running-locally.png)

3. <span data-ttu-id="e392f-152">Tome nota da porta que a função está a escutar.</span><span class="sxs-lookup"><span data-stu-id="e392f-152">Take a note of the port that the function is listening on.</span></span> <span data-ttu-id="e392f-153">Irá precisar da unidade seguinte para testar a aplicação móvel.</span><span class="sxs-lookup"><span data-stu-id="e392f-153">You'll need this in the next unit to test out the mobile app.</span></span> <span data-ttu-id="e392f-154">Na imagem acima, a função está a escutar na porta **7071**.</span><span class="sxs-lookup"><span data-stu-id="e392f-154">In the image above, the function is listening on port **7071**.</span></span>

    ```sh
    Listening on http://localhost:7071/
    ```

4. <span data-ttu-id="e392f-155">Deixe a função em execução para que possa testar a aplicação móvel na unidade seguinte.</span><span class="sxs-lookup"><span data-stu-id="e392f-155">Leave the function running so that you can test the mobile app in the next unit.</span></span>

## <a name="summary"></a><span data-ttu-id="e392f-156">Resumo</span><span class="sxs-lookup"><span data-stu-id="e392f-156">Summary</span></span>

<span data-ttu-id="e392f-157">Nessa unidade, aprendeu a criar um projeto das Funções do Azure no Visual Studio, adicionou um projeto partilhado com um objeto de dados para ser partilhado entre a aplicação móvel e a função, e aprendeu a criar uma implementação básica da função para anular a serialização de dados passados.</span><span class="sxs-lookup"><span data-stu-id="e392f-157">In this unit, you learned how to create an Azure Functions project in Visual Studio, added a shared project with a data object to be shared between the mobile app and the function, and learned how to create a basic implementation of the function to deserialize the data passed in.</span></span> <span data-ttu-id="e392f-158">Também aprendeu a executar localmente uma função do Azure.</span><span class="sxs-lookup"><span data-stu-id="e392f-158">You also learned how to run an Azure function locally.</span></span> <span data-ttu-id="e392f-159">Na unidade seguinte, irá chamar a função do Azure a partir da aplicação móvel.</span><span class="sxs-lookup"><span data-stu-id="e392f-159">In the next unit, you'll call the Azure function from the mobile app.</span></span>