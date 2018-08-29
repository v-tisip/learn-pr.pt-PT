Agora que sabe qual a forma de ativar o MSI que cria uma identidade para a nossa aplicação utilizar na autenticação, vamos criar uma aplicação que utiliza essa identidade para aceder aos segredos no cofre.

## <a name="reading-secrets-in-an-aspnet-core-app"></a>Ler segredos numa aplicação ASP.NET Core

A API do Azure Key Vault é uma API REST que lida com a gestão e utilização de chaves e cofres. Cada segredo num cofre tem um URL exclusivo e os valores dos segredos são obtidos através de pedidos HTTP GET.

A biblioteca de cliente do Key Vault oficial para o .NET Core é a classe `KeyVaultClient` no pacote Microsoft.Azure.KeyVault NuGet. Não tem de o utilizar diretamente, porém, com o método &mdash;ASP.NET Core `AddAzureKeyVault`, pode carregar todos os segredos de um cofre para a API de Configuração durante o arranque. Esta técnica permite-lhe aceder a todos os segredos por nome, utilizando a mesma interface `IConfiguration` que utiliza para o resto da sua configuração. As aplicações que utilizam `AddAzureKeyVault` exigem ambas as permissões **Obter** e **Listar** para o cofre.

> [!TIP]
> Independentemente da arquitetura ou idioma que utiliza para construir a sua aplicação, carregue segredos para a memória durante o arranque, a não ser que tenha uma razão específica para não o fazer. Lê-los diretamente a partir do cofre, sempre que precisar deles, é um processo desnecessariamente lento e caro.

`AddAzureKeyVault` requer apenas o nome do cofre como entrada, que obteremos a partir da nossa configuração de aplicação local. Também gere a autenticação de MSI automaticamente &mdash; quando usado numa aplicação implementada no Serviço de Aplicações do Azure com o MSI ativado, vai detetar o serviço de token do MSI e utilizá-lo para autenticar. É uma boa opção para a maioria dos cenários e implementa todas as melhores práticas, e vamos utilizá-lo no exercício desta unidade.

## <a name="handling-secrets-in-an-app"></a>Gerir segredos numa aplicação

Depois de um segredo ser carregado na sua aplicação, esta é responsável por geri-lo de forma segura. Na aplicação que vamos criar neste módulo, escrevemos o nosso valor secreto para a resposta do cliente e vemo-lo num browser para demonstrar que foi carregado com êxito. **Devolver um valor secreto para o cliente *não* é um procedimento recorrente!** Normalmente, utilizam-se segredos para ações como inicializar as bibliotecas do cliente para bases de dados ou APIs remotas.

> [!IMPORTANT]
> Reveja sempre cuidadosamente o código para garantir que a sua aplicação nunca vai gravar segredos para qualquer tipo de saída, incluindo registos, armazenamento e respostas.

## <a name="exercise"></a>Exercício

Vamos criar uma nova API WEB do ASP.NET Core e utilizar `AddAzureKeyVault` para carregar o segredo do nosso cofre.

### <a name="create-the-app"></a>Criar a aplicação

No terminal do Azure Cloud Shell, execute o seguinte para criar uma nova aplicação API WEB do ASP.NET Core e abra-a no editor.

```console
dotnet new webapi -o KeyVaultDemoApp
cd KeyVaultDemoApp
code .
```

Depois de carregar o editor, execute os seguintes comandos na shell para adicionar o pacote NuGet que contém `AddAzureKeyVault` e restaurar todas as dependências da aplicação.

```console
dotnet add package Microsoft.Extensions.Configuration.AzureKeyVault
dotnet restore
```

### <a name="add-code-to-load-and-use-secrets"></a>Adicionar código para carregar e usar segredos

Para demonstrar a boa utilização do Key Vault, iremos modificamos a nossa aplicação para carregar segredos do cofre durante o arranque. Também vamos adicionar um novo controlador com um ponto final que obtém nosso segredo **SecretPassword** do cofre.

Primeiro, o arranque da aplicação: abra `Program.cs`, elimine o conteúdo e substitua-o com o código seguinte:

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
> Certifique-se de que guarda os ficheiros com `Ctrl+S` quando terminar a edição dos mesmos.

A única alteração ao código do dispositivo de arranque é a adição de `ConfigureAppConfiguration`. Aqui é onde podemos carregar o nome do cofre a partir da configuração e utilizá-lo para chamar `AddAzureKeyVault`.

Em seguida, o controlador: crie um novo ficheiro na pasta `Controllers` chamada `SecretTestController.cs` e cole o seguinte código.

> [!NOTE]
> Para criar um novo ficheiro, utilize o comando `touch` no shell. Neste caso, utilize `touch Controllers/SecretTestController.cs`. Terá de clicar no botão Atualizar no painel Ficheiros do editor para vê-lo lá.

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

Execute `dotnet build` no shell para se certificar de que tudo é compilado. A aplicação está pronta para executara &mdash;, vamos agora levá-la para o Azure!