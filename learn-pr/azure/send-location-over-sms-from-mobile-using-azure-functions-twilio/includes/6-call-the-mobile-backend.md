<span data-ttu-id="95936-101">A aplicação móvel é executada e a versão inicial da função do Azure é criada.</span><span class="sxs-lookup"><span data-stu-id="95936-101">The mobile app runs and the initial version of the Azure function has been created.</span></span> <span data-ttu-id="95936-102">Nesta unidade, vai chamar a função do Azure a partir da aplicação móvel, ao passar a localização do utilizador e a lista de números de telefone para os quais o utilizador deseja enviar mensagens SMS.</span><span class="sxs-lookup"><span data-stu-id="95936-102">In this unit, you call the Azure function from the mobile app, passing in the user's location and the list of phone numbers the user wants to send SMS messages to.</span></span>

## <a name="calling-the-azure-function-from-the-mobile-app"></a><span data-ttu-id="95936-103">Chamar a função do Azure a partir da aplicação móvel</span><span class="sxs-lookup"><span data-stu-id="95936-103">Calling the Azure function from the mobile app</span></span>

1. <span data-ttu-id="95936-104">Abra o `MainViewModel`.</span><span class="sxs-lookup"><span data-stu-id="95936-104">Open the `MainViewModel`.</span></span>

2. <span data-ttu-id="95936-105">Nesta classe, adicione um campo privado `HttpClient` chamado `client`.</span><span class="sxs-lookup"><span data-stu-id="95936-105">In this class, add a private `HttpClient` field called `client`.</span></span> <span data-ttu-id="95936-106">Vai precisar de adicionar uma referência ao espaço de nomes `System.Net.Http`.</span><span class="sxs-lookup"><span data-stu-id="95936-106">You'll need to add a reference to the `System.Net.Http` namespace.</span></span>

    ```cs
    HttpClient client = new HttpClient();
    ```

3. <span data-ttu-id="95936-107">Adicione um campo constante para o URL base da função.</span><span class="sxs-lookup"><span data-stu-id="95936-107">Add a constant field for the base URL for the function.</span></span> <span data-ttu-id="95936-108">Defina-o como o endereço que o tempo de execução local das Funções do Azure está a escutar.</span><span class="sxs-lookup"><span data-stu-id="95936-108">Set this to the address that the local Azure Functions runtime is listening on.</span></span> <span data-ttu-id="95936-109">Quando a função estiver implementada no Azure, esta constante poderá ser alterada para ser o URL do Azure.</span><span class="sxs-lookup"><span data-stu-id="95936-109">Once the function is deployed to Azure, this constant can be changed to be the Azure URL.</span></span>

    ```cs
    const string baseUrl = "http://localhost:7071";
    ```

4. <span data-ttu-id="95936-110">No método `SendLocation`, depois de encontrar a localização, crie uma nova instância de `PostData` com a localização e a lista de números de telefone introduzidos pelo utilizador.</span><span class="sxs-lookup"><span data-stu-id="95936-110">Inside the `SendLocation` method, after the location has been found, create a new instance of `PostData` using the location and the list of phone numbers entered by the user.</span></span> <span data-ttu-id="95936-111">Terá de adicionar uma diretiva using para o espaço de nomes `ImHere.Data`.</span><span class="sxs-lookup"><span data-stu-id="95936-111">You'll need to add a using directive for the `ImHere.Data` namespace.</span></span>

    ```cs
    PostData postData = new PostData
    {
        Latitude = location.Latitude,
        Longitude = location.Longitude,
        ToNumbers = PhoneNumbers.Split('\n')
    };
    ```

    > <span data-ttu-id="95936-112">Este procedimento assume que os números de telefone foram introduzidos no formato correto, um por linha no controlo `Editor`.</span><span class="sxs-lookup"><span data-stu-id="95936-112">This assumes that the phone numbers have been entered in the correct format, one per line in the `Editor` control.</span></span> <span data-ttu-id="95936-113">Numa aplicação com qualidade de produção, existiria validação em todo este procedimento para garantir que um ou mais números de telefone foram introduzidos e também no formato correto.</span><span class="sxs-lookup"><span data-stu-id="95936-113">In a production-quality app, there would be validation around this to ensure one or more phone numbers were entered and were in the correct format.</span></span>

5. <span data-ttu-id="95936-114">Para serializar o `PostData` como JSON, a maneira mais fácil é utilizar o pacote NuGet Newtonsoft.JSON.</span><span class="sxs-lookup"><span data-stu-id="95936-114">To serialize the `PostData` as JSON, the easiest way is to use the Newtonsoft.JSON NuGet package.</span></span> <span data-ttu-id="95936-115">Adicione este pacote NuGet ao projeto `ImHere` da mesma forma que adicionou o Xamarin.Essentials numa unidade anterior.</span><span class="sxs-lookup"><span data-stu-id="95936-115">Add this NuGet package to the `ImHere` project in the same way that you added Xamarin.Essentials in an earlier unit.</span></span>

6. <span data-ttu-id="95936-116">Serialize o `PostData` para um `string` coma classe estática `JsonConvert`.</span><span class="sxs-lookup"><span data-stu-id="95936-116">Serialize the `PostData` to a `string` using the `JsonConvert` static class.</span></span> <span data-ttu-id="95936-117">Terá de adicionar uma diretiva using para o espaço de nomes `Newtonsoft.Json`.</span><span class="sxs-lookup"><span data-stu-id="95936-117">You'll need to add a using directive for the `Newtonsoft.Json` namespace.</span></span> <span data-ttu-id="95936-118">Codifique esta cadeia de caracteres numa classe `StringContent`, para que possa ser passada para a função Azure como JSON.</span><span class="sxs-lookup"><span data-stu-id="95936-118">Encode this string into a `StringContent` class so that it can be passed to the Azure function as JSON.</span></span>

    ```cs
    string data = JsonConvert.SerializeObject(postData);
    StringContent content = new StringContent(data, Encoding.UTF8, "application/json");
    ```

7. <span data-ttu-id="95936-119">Publique estes dados na função e obtenha o resultado.</span><span class="sxs-lookup"><span data-stu-id="95936-119">Post this data to the function and get the result back.</span></span>

   ```cs
    HttpResponseMessage result = await client.PostAsync($"{baseUrl}/api/SendLocation",
                                                        content);
   ```

   <span data-ttu-id="95936-120">As funções do Azure são acedidas com `/api/<function name>`; por isso, supondo que a porta escolhida pelo tempo de execução local das Funções é 7071, a função `SendLocation` estará acessível em `http://localhost:7071/api/SendLocation`.</span><span class="sxs-lookup"><span data-stu-id="95936-120">Azure functions are accessed using `/api/<function name>`, so assuming the port chosen by the local Functions runtime is 7071, the `SendLocation` function will be accessible at `http://localhost:7071/api/SendLocation`.</span></span>

8. <span data-ttu-id="95936-121">Consoante o resultado, mostre uma mensagem na interface de utilizador.</span><span class="sxs-lookup"><span data-stu-id="95936-121">Depending on the result, show a message on the UI.</span></span>

    ```cs
    if (result.IsSuccessStatusCode)
        Message = "Location sent successfully";
    else
        Message = $"Error - {result.ReasonPhrase}";
    ```

<span data-ttu-id="95936-122">O código completo dos novos campos e o método `SendLocation` são apresentados abaixo.</span><span class="sxs-lookup"><span data-stu-id="95936-122">The full code for the new fields and the `SendLocation` method is below.</span></span>

```cs
HttpClient client = new HttpClient();
const string baseUrl = "http://localhost:7071";

async Task SendLocation()
{
    Location location = await Geolocation.GetLastKnownLocationAsync();

    if (location != null)
    {
        Message = $"Location found: {location.Latitude}, {location.Longitude}.";

        PostData postData = new PostData
        {
            Latitude = location.Latitude,
            Longitude = location.Longitude,
            ToNumbers = PhoneNumbers.Split('\n')
        };

        string data = JsonConvert.SerializeObject(postData);
        StringContent content = new StringContent(data, Encoding.UTF8, "application/json");
        HttpResponseMessage result = await client.PostAsync($"{baseUrl}/api/SendLocation",
                                                            content);

        if (result.IsSuccessStatusCode)
            Message = "Location sent successfully";
        else
            Message = $"Error - {result.ReasonPhrase}";
    }
}
```

## <a name="testing-it-out"></a><span data-ttu-id="95936-123">Teste</span><span class="sxs-lookup"><span data-stu-id="95936-123">Testing it out</span></span>

1. <span data-ttu-id="95936-124">Verifique se a função do Azure ainda está em execução localmente e se a porta corresponde ao método `SendLocation`.</span><span class="sxs-lookup"><span data-stu-id="95936-124">Make sure the Azure function is still running locally and the port matches the `SendLocation` method.</span></span>

2. <span data-ttu-id="95936-125">Defina a aplicação UWP como a aplicação de arranque e execute-a.</span><span class="sxs-lookup"><span data-stu-id="95936-125">Set the UWP app as the startup app and run it.</span></span> <span data-ttu-id="95936-126">Clique no botão **Enviar Localização**.</span><span class="sxs-lookup"><span data-stu-id="95936-126">Click the **Send Location** button.</span></span> <span data-ttu-id="95936-127">Verá a saída na janela de consola do tempo de execução das Funções a mostrar a função a ser chamada e o registo que mostra o URL gerado.</span><span class="sxs-lookup"><span data-stu-id="95936-127">You'll see output in the Functions runtime console window showing the function being called, and the logging showing the generated URL.</span></span>

    ![Saída da função que é chamada](../media/6-function-called.png)

3. <span data-ttu-id="95936-129">Para testar a geração do URL, cole-o num browser na consola.</span><span class="sxs-lookup"><span data-stu-id="95936-129">To test the URL generation, paste it from the console into a browser.</span></span> <span data-ttu-id="95936-130">Deverá mostrar a localização atual.</span><span class="sxs-lookup"><span data-stu-id="95936-130">It should show your current location.</span></span>

## <a name="summary"></a><span data-ttu-id="95936-131">Resumo</span><span class="sxs-lookup"><span data-stu-id="95936-131">Summary</span></span>

<span data-ttu-id="95936-132">Nesta unidade, aprendeu como chamar uma função do Azure a partir da aplicação móvel.</span><span class="sxs-lookup"><span data-stu-id="95936-132">In this unit, you learned how to call an Azure function from the mobile app.</span></span> <span data-ttu-id="95936-133">Esta chamada passa a localização do utilizador e os números de telefone que introduziram como JSON.</span><span class="sxs-lookup"><span data-stu-id="95936-133">This call passed the user's location and the phone numbers they entered as JSON.</span></span> <span data-ttu-id="95936-134">Na unidade seguinte, vai vincular a função do Azure ao Twilio para enviar esta localização como uma mensagem SMS.</span><span class="sxs-lookup"><span data-stu-id="95936-134">In the next unit, you'll bind the Azure function to Twilio to send this location as an SMS message.</span></span>