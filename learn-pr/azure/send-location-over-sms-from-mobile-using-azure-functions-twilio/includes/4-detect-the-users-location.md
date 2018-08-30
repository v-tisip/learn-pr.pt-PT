<span data-ttu-id="ca070-101">A aplicação tem uma interface de utilizador e um ViewModel.</span><span class="sxs-lookup"><span data-stu-id="ca070-101">The app has a UI and a ViewModel.</span></span> <span data-ttu-id="ca070-102">Nesta unidade, vai adicionar a pesquisa de localizações ao ViewModel com o Xamarin.Essentials.</span><span class="sxs-lookup"><span data-stu-id="ca070-102">In this unit, you add location lookup to the ViewModel using Xamarin.Essentials.</span></span>

## <a name="enable-location-permissions"></a><span data-ttu-id="ca070-103">Ativar as permissões de localização</span><span class="sxs-lookup"><span data-stu-id="ca070-103">Enable location permissions</span></span>

<span data-ttu-id="ca070-104">Todas as plataformas móveis têm segurança no que diz respeito às informações do utilizador e a determinado hardware, como a câmara, a biblioteca de fotografias e a localização do utilizador.</span><span class="sxs-lookup"><span data-stu-id="ca070-104">All mobile platforms have security around user information and certain hardware, such as the camera, photo library, and the user's location.</span></span> <span data-ttu-id="ca070-105">Para que uma aplicação possa aceder à localização do utilizador, este terá de dar permissão: ao conceder implicitamente essas permissões na altura da instalação ou ao optar por conceder a permissão no momento da execução.</span><span class="sxs-lookup"><span data-stu-id="ca070-105">Before an app can access the user's location, the user has to grant permission - either by implicitly granting these permissions at install time or by choosing to grant a permission at runtime.</span></span> <span data-ttu-id="ca070-106">Quando vê uma aplicação UWP na loja, a listagem mostrará as permissões necessárias para aceder à aplicação.</span><span class="sxs-lookup"><span data-stu-id="ca070-106">When you view a UWP app on the store, the listing will show the permissions that the app needs.</span></span> <span data-ttu-id="ca070-107">Ao instalar a aplicação, concede implicitamente permissão.</span><span class="sxs-lookup"><span data-stu-id="ca070-107">By installing the app, you implicitly grant permission.</span></span> <span data-ttu-id="ca070-108">Estas permissões são configuradas num ficheiro de manifesto da aplicação.</span><span class="sxs-lookup"><span data-stu-id="ca070-108">These permissions are configured in an app manifest file.</span></span>

1. <span data-ttu-id="ca070-109">No projeto da aplicação `ImHere.UWP`, abra o ficheiro `Package.appxmanifest`.</span><span class="sxs-lookup"><span data-stu-id="ca070-109">In the `ImHere.UWP` app project, open the `Package.appxmanifest` file.</span></span>

2. <span data-ttu-id="ca070-110">Vá para o separador **Capacidades** e verifique a capacidade *Localização*.</span><span class="sxs-lookup"><span data-stu-id="ca070-110">Head to the **Capabilities** tab and check the *Location* capability.</span></span>

    ![O separador de capacidades da UWP](../media/4-uwp-location-capability.png)

> <span data-ttu-id="ca070-112">Se quiser suporte para Android ou iOS, as permissões terão de ser configuradas de forma diferente.</span><span class="sxs-lookup"><span data-stu-id="ca070-112">If you want to support Android or iOS, the permissions need to be configured differently.</span></span> <span data-ttu-id="ca070-113">Esse procedimento é detalhado nos [documentos de Geolocalização do Xamarin.Essentials](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=android#getting-started).</span><span class="sxs-lookup"><span data-stu-id="ca070-113">This is detailed in the [Xamarin.Essentials Geolocation docs](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=android#getting-started).</span></span>

## <a name="query-for-the-users-location"></a><span data-ttu-id="ca070-114">Consulta da localização do utilizador</span><span class="sxs-lookup"><span data-stu-id="ca070-114">Query for the user's location</span></span>

<span data-ttu-id="ca070-115">Existem duas formas de obter a localização do utilizador: a última conhecida ou a atual.</span><span class="sxs-lookup"><span data-stu-id="ca070-115">There are two ways to get the user's location - the last known or the current.</span></span> <span data-ttu-id="ca070-116">A obtenção da localização atual pode demorar algum tempo, uma vez que o dispositivo poderá ter de estabelecer uma ligação GPS e esperar até que a localização exata seja obtida.</span><span class="sxs-lookup"><span data-stu-id="ca070-116">The current location can take some time to get because the device may need to establish a GPS link and wait for the accurate location to be retrieved.</span></span> <span data-ttu-id="ca070-117">A forma mais rápida é obter a última localização detetada pelo dispositivo conhecida.</span><span class="sxs-lookup"><span data-stu-id="ca070-117">The fastest way is to get the last known location detected by the device.</span></span> <span data-ttu-id="ca070-118">A última localização conhecida é potencialmente menos precisa, mas é uma chamada muito mais rápida.</span><span class="sxs-lookup"><span data-stu-id="ca070-118">The last known location is potentially less accurate but is a much faster call.</span></span> <span data-ttu-id="ca070-119">As localizações são fornecidas com a latitude e a longitude em [graus decimais](https://en.wikipedia.org/wiki/Decimal_degrees) e a altitude do dispositivo em metros acima do nível do mar.</span><span class="sxs-lookup"><span data-stu-id="ca070-119">Locations come as the latitude and longitude in [decimal degrees](https://en.wikipedia.org/wiki/Decimal_degrees) and the altitude of the device in meters above sea level.</span></span>

1. <span data-ttu-id="ca070-120">Abra a classe `MainViewModel` no projeto .NET `ImHere` padrão.</span><span class="sxs-lookup"><span data-stu-id="ca070-120">Open the `MainViewModel` class in the `ImHere` .NET standard project.</span></span>

2. <span data-ttu-id="ca070-121">No método `SendLocation`, crie uma chamada para o método estático `GetLastKnownLocationAsync` na classe `Geolocation` no espaço de nomes `Xamarin.Essentials`.</span><span class="sxs-lookup"><span data-stu-id="ca070-121">In the `SendLocation` method, make a call to the `GetLastKnownLocationAsync` static method on the `Geolocation` class in the `Xamarin.Essentials` namespace.</span></span>

    ```cs
    Location location = await Geolocation.GetLastKnownLocationAsync();
    ```

3. <span data-ttu-id="ca070-122">Atualize a propriedade `Message` com a localização do utilizador, caso encontre alguma.</span><span class="sxs-lookup"><span data-stu-id="ca070-122">Update the `Message` property with the user's location if one is found.</span></span>

    ```cs
    if (location != null)
    {
        Message = $"Location found: {location.Latitude}, {location.Longitude}.";
    }
    ```

<span data-ttu-id="ca070-123">O código completo para este método é apresentado abaixo.</span><span class="sxs-lookup"><span data-stu-id="ca070-123">The full code for this method is below.</span></span>

```cs
async Task SendLocation()
{
    Location location = await Geolocation.GetLastKnownLocationAsync();

    if (location != null)
    {
        Message = $"Location found: {location.Latitude}, {location.Longitude}.";
    }
}
```

<span data-ttu-id="ca070-124">Execute a aplicação e clique no botão **Enviar Localização** para ver a localização na interface do utilizador.</span><span class="sxs-lookup"><span data-stu-id="ca070-124">Run the app and click the **Send Location** button to see the location on the UI.</span></span>

![A aplicação em execução a mostrar a localização do utilizador](../media/4-running-app-showing-location.png)

> <span data-ttu-id="ca070-126">Esta aplicação utiliza a última localização conhecida.</span><span class="sxs-lookup"><span data-stu-id="ca070-126">This app uses the last known location.</span></span> <span data-ttu-id="ca070-127">Numa aplicação com qualidade de produção, poderá querer obter a localização exata atual dentro de um limite de tempo e, se nenhuma for encontrada, reverter para a última conhecida.</span><span class="sxs-lookup"><span data-stu-id="ca070-127">In a production-quality app, you would want to get the current accurate location with a time-out, and if one is not found in time, fall back to the last known.</span></span> <span data-ttu-id="ca070-128">Pode ler mais sobre como fazê-lo nos [documentos de Geolocalização do Xamarin.Essentials](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=uwp#using-geolocation). Esta aplicação não tem processamento de erros.</span><span class="sxs-lookup"><span data-stu-id="ca070-128">You can read more on how to do this in the [Xamarin.Essentials Geolocation docs](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=uwp#using-geolocation). This app does not have error handling.</span></span> <span data-ttu-id="ca070-129">Numa aplicação com qualidade de produção, deve processar as possíveis exceções, por exemplo, se a localização não estava disponível e tiver sido emitida uma exceção.</span><span class="sxs-lookup"><span data-stu-id="ca070-129">In a production-quality app, you should handle any exceptions that occur, for example, if the location was not available and an exception was thrown.</span></span>

## <a name="summary"></a><span data-ttu-id="ca070-130">Resumo</span><span class="sxs-lookup"><span data-stu-id="ca070-130">Summary</span></span>

<span data-ttu-id="ca070-131">Nesta unidade, aprendeu a utilizar o Xamarin.Essentials para obter a localização do utilizador.</span><span class="sxs-lookup"><span data-stu-id="ca070-131">In this unit, you learned how to use Xamarin.Essentials to get the user's location.</span></span> <span data-ttu-id="ca070-132">Na unidade seguinte, vai criar uma função do Azure para atuar como um back-end da aplicação móvel.</span><span class="sxs-lookup"><span data-stu-id="ca070-132">In the next unit, you'll create an Azure function to act as a back end for the mobile app.</span></span>