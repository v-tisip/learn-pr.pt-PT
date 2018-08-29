<span data-ttu-id="219f6-101">Agora que sabe qual a forma de ativar o MSI que cria uma identidade para a nossa aplicação utilizar na autenticação, vamos criar uma aplicação que utiliza essa identidade para aceder aos segredos no cofre.</span><span class="sxs-lookup"><span data-stu-id="219f6-101">Now that you know how enabling MSI creates an identity for our app to use for authentication, we'll create an app that uses that identity to access secrets in the vault.</span></span>

## <a name="reading-secrets-in-an-aspnet-core-app"></a><span data-ttu-id="219f6-102">Ler segredos numa aplicação ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="219f6-102">Reading secrets in an ASP.NET Core app</span></span>

<span data-ttu-id="219f6-103">A API do Azure Key Vault é uma API REST que lida com a gestão e utilização de chaves e cofres.</span><span class="sxs-lookup"><span data-stu-id="219f6-103">The Azure Key Vault API is a REST API that handles all management and usage of keys and vaults.</span></span> <span data-ttu-id="219f6-104">Cada segredo num cofre tem um URL exclusivo e os valores dos segredos são obtidos através de pedidos HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="219f6-104">Each secret in a vault has a unique URL, and secret values are retrieved with HTTP GET requests.</span></span>

<span data-ttu-id="219f6-105">A biblioteca de cliente do Key Vault oficial para o .NET Core é a classe `KeyVaultClient` no pacote Microsoft.Azure.KeyVault NuGet.</span><span class="sxs-lookup"><span data-stu-id="219f6-105">The official Key Vault client library for .NET Core is the `KeyVaultClient` class in the Microsoft.Azure.KeyVault NuGet package.</span></span> <span data-ttu-id="219f6-106">Não tem de o utilizar diretamente, porém, com o método &mdash;ASP.NET Core `AddAzureKeyVault`, pode carregar todos os segredos de um cofre para a API de Configuração durante o arranque.</span><span class="sxs-lookup"><span data-stu-id="219f6-106">You don't need to use it directly, though &mdash; with ASP.NET Core's `AddAzureKeyVault` method, you can load all the secrets from a vault into the Configuration API at startup.</span></span> <span data-ttu-id="219f6-107">Esta técnica permite-lhe aceder a todos os segredos por nome, utilizando a mesma interface `IConfiguration` que utiliza para o resto da sua configuração.</span><span class="sxs-lookup"><span data-stu-id="219f6-107">This technique enables you to access all of your secrets by name using the same `IConfiguration` interface you use for the rest of your configuration.</span></span> <span data-ttu-id="219f6-108">As aplicações que utilizam `AddAzureKeyVault` exigem ambas as permissões **Obter** e **Listar** para o cofre.</span><span class="sxs-lookup"><span data-stu-id="219f6-108">Apps that use `AddAzureKeyVault` require both **Get** and **List** permissions to the vault.</span></span>

> [!TIP]
> <span data-ttu-id="219f6-109">Independentemente da arquitetura ou idioma que utiliza para construir a sua aplicação, carregue segredos para a memória durante o arranque, a não ser que tenha uma razão específica para não o fazer.</span><span class="sxs-lookup"><span data-stu-id="219f6-109">Regardless of the framework or language you use to build your app, load secrets into memory once at app startup unless you have a specific reason not to.</span></span> <span data-ttu-id="219f6-110">Lê-los diretamente a partir do cofre, sempre que precisar deles, é um processo desnecessariamente lento e caro.</span><span class="sxs-lookup"><span data-stu-id="219f6-110">Reading them directly from the vault every time you need them is unnecessarily slow and expensive.</span></span>

<span data-ttu-id="219f6-111">`AddAzureKeyVault` requer apenas o nome do cofre como entrada, que obteremos a partir da nossa configuração de aplicação local.</span><span class="sxs-lookup"><span data-stu-id="219f6-111">`AddAzureKeyVault` only requires the vault name as an input, which we'll get from our local app configuration.</span></span> <span data-ttu-id="219f6-112">Também gere a autenticação de MSI automaticamente &mdash; quando usado numa aplicação implementada no Serviço de Aplicações do Azure com o MSI ativado, vai detetar o serviço de token do MSI e utilizá-lo para autenticar.</span><span class="sxs-lookup"><span data-stu-id="219f6-112">It also automatically handles MSI authentication &mdash; when used in an app deployed to Azure App Service with MSI enabled, it will detect the MSI token service and use it to authenticate.</span></span> <span data-ttu-id="219f6-113">É uma boa opção para a maioria dos cenários e implementa todas as melhores práticas, e vamos utilizá-lo no exercício desta unidade.</span><span class="sxs-lookup"><span data-stu-id="219f6-113">It's a good fit for most scenarios and implements all best practices, and we'll use it in this unit's exercise.</span></span>

## <a name="handling-secrets-in-an-app"></a><span data-ttu-id="219f6-114">Gerir segredos numa aplicação</span><span class="sxs-lookup"><span data-stu-id="219f6-114">Handling secrets in an app</span></span>

<span data-ttu-id="219f6-115">Depois de um segredo ser carregado na sua aplicação, esta é responsável por geri-lo de forma segura.</span><span class="sxs-lookup"><span data-stu-id="219f6-115">Once a secret is loaded into your app, it's up to your app to handle it securely.</span></span> <span data-ttu-id="219f6-116">Na aplicação que vamos criar neste módulo, escrevemos o nosso valor secreto para a resposta do cliente e vemo-lo num browser para demonstrar que foi carregado com êxito.</span><span class="sxs-lookup"><span data-stu-id="219f6-116">In the app we build in this module, we write our secret value out to the client response and view it in a web browser to demonstrate that it has been loaded successfully.</span></span> <span data-ttu-id="219f6-117">**Devolver um valor secreto para o cliente *não* é um procedimento recorrente!**</span><span class="sxs-lookup"><span data-stu-id="219f6-117">**Returning a secret value to the client is *not* something you'd normally do!**</span></span> <span data-ttu-id="219f6-118">Normalmente, utilizam-se segredos para ações como inicializar as bibliotecas do cliente para bases de dados ou APIs remotas.</span><span class="sxs-lookup"><span data-stu-id="219f6-118">Usually, you'll use secrets to do things like initialize client libraries for databases or remote APIs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="219f6-119">Reveja sempre cuidadosamente o código para garantir que a sua aplicação nunca vai gravar segredos para qualquer tipo de saída, incluindo registos, armazenamento e respostas.</span><span class="sxs-lookup"><span data-stu-id="219f6-119">Always carefully review your code to ensure that your app never writes secrets to any kind of output, including logs, storage, and responses.</span></span>

## <a name="exercise"></a><span data-ttu-id="219f6-120">Exercício</span><span class="sxs-lookup"><span data-stu-id="219f6-120">Exercise</span></span>

<span data-ttu-id="219f6-121">Vamos criar uma nova API WEB do ASP.NET Core e utilizar `AddAzureKeyVault` para carregar o segredo do nosso cofre.</span><span class="sxs-lookup"><span data-stu-id="219f6-121">We'll create a new ASP.NET Core web API and use `AddAzureKeyVault` to load the secret from our vault.</span></span>

### <a name="create-the-app"></a><span data-ttu-id="219f6-122">Criar a aplicação</span><span class="sxs-lookup"><span data-stu-id="219f6-122">Create the app</span></span>

<span data-ttu-id="219f6-123">No terminal do Azure Cloud Shell, execute o seguinte para criar uma nova aplicação API WEB do ASP.NET Core e abra-a no editor.</span><span class="sxs-lookup"><span data-stu-id="219f6-123">In the Azure Cloud Shell terminal, run the following to create a new ASP.NET Core web API application and open it in the editor.</span></span>

```console
dotnet new webapi -o KeyVaultDemoApp
cd KeyVaultDemoApp
code .
```

<span data-ttu-id="219f6-124">Depois de carregar o editor, execute os seguintes comandos na shell para adicionar o pacote NuGet que contém `AddAzureKeyVault` e restaurar todas as dependências da aplicação.</span><span class="sxs-lookup"><span data-stu-id="219f6-124">After the editor loads, run the following commands in the shell to add the NuGet package containing `AddAzureKeyVault` and restore all of the app's dependencies.</span></span>

```console
dotnet add package Microsoft.Extensions.Configuration.AzureKeyVault
dotnet restore
```

### <a name="add-code-to-load-and-use-secrets"></a><span data-ttu-id="219f6-125">Adicionar código para carregar e usar segredos</span><span class="sxs-lookup"><span data-stu-id="219f6-125">Add code to load and use secrets</span></span>

<span data-ttu-id="219f6-126">Para demonstrar a boa utilização do Key Vault, iremos modificamos a nossa aplicação para carregar segredos do cofre durante o arranque.</span><span class="sxs-lookup"><span data-stu-id="219f6-126">To demonstrate good usage of Key Vault, we will modify our app to load secrets from the vault at startup.</span></span> <span data-ttu-id="219f6-127">Também vamos adicionar um novo controlador com um ponto final que obtém nosso segredo **SecretPassword** do cofre.</span><span class="sxs-lookup"><span data-stu-id="219f6-127">We'll also add a new controller with an endpoint that gets our **SecretPassword** secret from the vault.</span></span>

<span data-ttu-id="219f6-128">Primeiro, o arranque da aplicação: abra `Program.cs`, elimine o conteúdo e substitua-o com o código seguinte:</span><span class="sxs-lookup"><span data-stu-id="219f6-128">First, the app startup: Open `Program.cs`, delete the contents and replace them with the following code:</span></span>

```csharp
using Microsoft.AspNetCore;
using Microsoft.AspNetCore.Hosting;
using Microsoft.Extensions.Configuration;

namespace KeyVaultDemoApp
{
    public class Program
    {
        public static void Main(string[] args)
        {
            CreateWebHostBuilder(args).Build().Run();
        }

        public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
            WebHost.CreateDefaultBuilder(args)
                .ConfigureAppConfiguration((context, config) =>
                {
                    // Build the current set of configuration to load values from
                    // JSON files and environment variables, including VaultName.
                    var builtConfig = config.Build();

                    // Use VaultName from the configuration to create the full vault URL.
                    var vaultUrl = $"https://{builtConfig["VaultName"]}.vault.azure.net/";

                    // Load all secrets from the vault into configuration. This will automatically
                    // authenticate to the vault using MSI. If MSI is not available, it will
                    // check if Visual Studio and/or the Azure CLI are installed locally and
                    // see if they are configured with credentials that can access the vault.
                    config.AddAzureKeyVault(vaultUrl);
                })
                .UseStartup<Startup>();
    }
}
```

> [!NOTE]
> <span data-ttu-id="219f6-129">Certifique-se de que guarda os ficheiros com `Ctrl+S` quando terminar a edição dos mesmos.</span><span class="sxs-lookup"><span data-stu-id="219f6-129">Make sure to save files with `Ctrl+S` when you're done editing them.</span></span>

<span data-ttu-id="219f6-130">A única alteração ao código do dispositivo de arranque é a adição de `ConfigureAppConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="219f6-130">The only change from the starter code is the addition of `ConfigureAppConfiguration`.</span></span> <span data-ttu-id="219f6-131">Aqui é onde podemos carregar o nome do cofre a partir da configuração e utilizá-lo para chamar `AddAzureKeyVault`.</span><span class="sxs-lookup"><span data-stu-id="219f6-131">This is where we load the vault name from configuration and call `AddAzureKeyVault` with it.</span></span>

<span data-ttu-id="219f6-132">Em seguida, o controlador: crie um novo ficheiro na pasta `Controllers` chamada `SecretTestController.cs` e cole o seguinte código.</span><span class="sxs-lookup"><span data-stu-id="219f6-132">Next, the controller: Create a new file in the `Controllers` folder called `SecretTestController.cs` and paste the following code into it.</span></span>

> [!NOTE]
> <span data-ttu-id="219f6-133">Para criar um novo ficheiro, utilize o comando `touch` no shell.</span><span class="sxs-lookup"><span data-stu-id="219f6-133">To create a new file, use the `touch` command in the shell.</span></span> <span data-ttu-id="219f6-134">Neste caso, utilize `touch Controllers/SecretTestController.cs`.</span><span class="sxs-lookup"><span data-stu-id="219f6-134">In this case, use `touch Controllers/SecretTestController.cs`.</span></span> <span data-ttu-id="219f6-135">Terá de clicar no botão Atualizar no painel Ficheiros do editor para vê-lo lá.</span><span class="sxs-lookup"><span data-stu-id="219f6-135">You'll need to click the refresh button in the Files pane of the editor to see it there.</span></span>

```csharp
using System;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Configuration;

namespace KeyVaultDemoApp.Controllers
{
    [Route("api/[controller]")]
    public class SecretTestController : ControllerBase
    {
        private readonly IConfiguration _configuration;

        public SecretTestController(IConfiguration configuration)
        {
            _configuration = configuration;
        }

        [HttpGet]
        public IActionResult Get()
        {
            // Get the secret value from configuration. This can be done anywhere
            // we have access to IConfiguration. This does not call the Key Vault
            // API, because the secrets were loaded at startup.
            var secretName = "SecretPassword";
            var secretValue = _configuration[secretName];

            if (secretValue == null)
            {
                return StatusCode(
                    StatusCodes.Status500InternalServerError,
                    $"Error: No secret named {secretName} was found...");
            }
            else {
                return Content($"Secret value: {secretValue}" +
                    Environment.NewLine + Environment.NewLine +
                    "This is for testing only! Never output a secret " +
                    "to a response or anywhere else in a real app!");
            }
        }
    }
}
```

<span data-ttu-id="219f6-136">Execute `dotnet build` no shell para se certificar de que tudo é compilado.</span><span class="sxs-lookup"><span data-stu-id="219f6-136">Run `dotnet build` in the shell to make sure everything compiles.</span></span> <span data-ttu-id="219f6-137">A aplicação está pronta para executara &mdash;, vamos agora levá-la para o Azure!</span><span class="sxs-lookup"><span data-stu-id="219f6-137">The app is ready to run &mdash; now let's get it into Azure!</span></span>