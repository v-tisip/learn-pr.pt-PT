<span data-ttu-id="09a27-101">Neste módulo, vai criar uma simples aplicação de consola ao utilizar o terminal integrado, instalar pacotes NuGet e utilizar a extensão do Azure Cosmos DB para ver as bases de dados e coleções criadas no módulo anterior.</span><span class="sxs-lookup"><span data-stu-id="09a27-101">In this module you will create a simple console app using the integrated terminal, install NuGet packages, and use the Azure Cosmos DB extension to see databases and collections created in the previous module.</span></span> <span data-ttu-id="09a27-102">Vai obter a sua cadeia de ligação do Azure Cosmos DB a partir da extensão e então começar a programar em relação ao Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="09a27-102">You'll retrieve your Azure Cosmos DB connection string from the extension, and then start developing against Azure Cosmos DB.</span></span> 

## <a name="create-a-console-app"></a><span data-ttu-id="09a27-103">Criar uma aplicação de consola</span><span class="sxs-lookup"><span data-stu-id="09a27-103">Create a console app</span></span>

1. <span data-ttu-id="09a27-104">Abra o Visual Studio Code e, em seguida, selecione **Ficheiro** > **Abrir Pasta**.</span><span class="sxs-lookup"><span data-stu-id="09a27-104">Open Visual Studio Code, and then select **File** > **Open Folder**.</span></span>

2. <span data-ttu-id="09a27-105">Crie uma nova pasta chamada **learning-module** onde quer que esteja seu novo projeto em C# e em seguida clique em **Selecionar Pasta**.</span><span class="sxs-lookup"><span data-stu-id="09a27-105">Create a new folder named **learning-module** where you want your new C# project to be, and then click **Select Folder**.</span></span>

2. <span data-ttu-id="09a27-106">Abra o terminal integrado do Visual Studio Code ao selecionar **Ver** > **Terminal Integrado** no menu principal.</span><span class="sxs-lookup"><span data-stu-id="09a27-106">Open the integrated terminal from Visual Studio Code by selecting **View** > **Integrated Terminal** from the main menu.</span></span>

3. <span data-ttu-id="09a27-107">Na janela do terminal, escreva **dotnet new console**.</span><span class="sxs-lookup"><span data-stu-id="09a27-107">In the terminal window, type **dotnet new console**.</span></span>

    <span data-ttu-id="09a27-108">Este comando cria um ficheiro **Program.cs** na sua pasta com um simples programa "Olá, mundo!" já escrito, juntamente com um ficheiro de projeto C# chamado **learning-module.csproj**.</span><span class="sxs-lookup"><span data-stu-id="09a27-108">This command creates a **Program.cs** file in your folder with a simple "Hello World" program already written, along with a C# project file named **learning-module.csproj**.</span></span>

4. <span data-ttu-id="09a27-109">Na janela de terminal, escreva o seguinte comando para executar o programa "Olá, mundo!".</span><span class="sxs-lookup"><span data-stu-id="09a27-109">In the terminal window, type the following command to run the "Hello World" program.</span></span> 

    ```
    dotnet run
    ```

    <span data-ttu-id="09a27-110">A janela de terminal exibe "Olá, mundo!"</span><span class="sxs-lookup"><span data-stu-id="09a27-110">The terminal window displays "Hello world!"</span></span> <span data-ttu-id="09a27-111">como saída.</span><span class="sxs-lookup"><span data-stu-id="09a27-111">as output.</span></span>

## <a name="connect-the-app-to-azure-cosmos-db"></a><span data-ttu-id="09a27-112">Ligar a aplicação ao Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="09a27-112">Connect the app to Azure Cosmos DB</span></span>

1. <span data-ttu-id="09a27-113">Inicie sessão no Azure ao clicar em **Ver** > **Paleta de Comandos** e escrever **Azure: Iniciar Sessão**.</span><span class="sxs-lookup"><span data-stu-id="09a27-113">Sign in to Azure by clicking **View** > **Command Palette** and typing **Azure: Sign In**.</span></span>

    <span data-ttu-id="09a27-114">Siga as instruções para copiar e colar o código fornecido no seu browser, que o autentica na sua sessão do Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="09a27-114">Follow the prompts to copy and paste the code provided in the web browser, which authenticates your Visual Studio Code session.</span></span>

2. <span data-ttu-id="09a27-115">Clique no ![ícone do Explorer](../media/2-setup/visual-studio-code-explorer-icon.png), ícone **Explorer** no menu da esquerda e, em seguida, aumente o **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="09a27-115">Click the ![Explorer icon](../media/2-setup/visual-studio-code-explorer-icon.png) **Explorer** icon on the left menu, and then expand **Azure Cosmos DB**.</span></span>

3. <span data-ttu-id="09a27-116">Aumentar a sua subscrição do Azure > conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="09a27-116">Expand your Azure subscription > Azure Cosmos DB account.</span></span> <span data-ttu-id="09a27-117">Se tiver criado a base de dados de **Produtos** e a coleção **Vestuário** nos módulos anteriores, a extensão mostra-os.</span><span class="sxs-lookup"><span data-stu-id="09a27-117">If you created the **Products** database and **Clothing** collection in the previous modules, the extension displays them.</span></span>

   ![Extensão do Azure Cosmos DB para o Visual Studio Code](../media/2-setup/azure-cosmos-db-vs-code-extension.png) 

4. <span data-ttu-id="09a27-119">Agora vamos criar uma nova base de dados e coleção para os seus clientes.</span><span class="sxs-lookup"><span data-stu-id="09a27-119">Now let's create a new database and collection for your customers.</span></span>

    <span data-ttu-id="09a27-120">Na janela do Explorador, clique com o botão direito na sua conta e então em **Criar Base de Dados**.</span><span class="sxs-lookup"><span data-stu-id="09a27-120">In the Explorer window, right-click your account, and then click **Create Database**.</span></span> 
    
    <span data-ttu-id="09a27-121">Na caixa de texto na parte superior do ecrã, escreva **Utilizadores** para o nome de base de dados > **Introduzir** > **WebCustomers** para o nome da coleção >  **Introduzir** > **userId** para a chave de partição > **Introduzir** > **1000** para a capacidade de taxa de transferência inicial > **Introduzir**.</span><span class="sxs-lookup"><span data-stu-id="09a27-121">In the text box at the top of the screen, type **Users** for the database name > **Enter** > **WebCustomers** for the collection name > **Enter** > **userId** for the partition key > **Enter** > **1000** for the initial throughput capacity > **Enter**.</span></span>

    <span data-ttu-id="09a27-122">![Extensão do Azure Cosmos DB para o Visual Studio Code](../media/2-setup/vs-code-azure-cosmos-db-extension.gif) <!--Retake on fresh machine without the other subscriptions showing--></span><span class="sxs-lookup"><span data-stu-id="09a27-122">![Azure Cosmos DB Visual Studio Code extension](../media/2-setup/vs-code-azure-cosmos-db-extension.gif) <!--Retake on fresh machine without the other subscriptions showing--></span></span>

    <span data-ttu-id="09a27-123">A nova base de dados de Utilizadores e coleção WebCustomers são exibidas na janela do Explorador.</span><span class="sxs-lookup"><span data-stu-id="09a27-123">The new Users database and WebCustomers collection are displayed in the Explorer window.</span></span>

5. <span data-ttu-id="09a27-124">No terminal integrado, tem de executar cada um dos seguintes comandos numa nova linha de comandos para instalar os pacotes de NuGet necessários.</span><span class="sxs-lookup"><span data-stu-id="09a27-124">In the integrated terminal, run each of the following commands at a new prompt to install the required NuGet packages.</span></span>

    ```
    dotnet add package System.Net.Http
    dotnet add package Microsoft.Azure.DocumentDB.Core
    dotnet add package Newtonsoft.Json
    dotnet add package System.Threading.Tasks
    dotnet add package System.Linq
    dotnet add package Bogus
    dotnet restore
    ```

6. <span data-ttu-id="09a27-125">Na parte superior do painel do Explorador, clique em **Program.cs** para abrir o ficheiro.</span><span class="sxs-lookup"><span data-stu-id="09a27-125">At the top of the Explorer pane, click **Program.cs** to open the file.</span></span>

7. <span data-ttu-id="09a27-126">Adicione as seguintes instruções using após `using System;`.</span><span class="sxs-lookup"><span data-stu-id="09a27-126">Add the following using statements after `using System;`.</span></span>

    ```csharp
    using System.Linq;
    using System.Threading.Tasks;
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;
    ```

8. <span data-ttu-id="09a27-127">Adicione as duas constantes seguintes e a sua variável de *cliente* à classe Program:</span><span class="sxs-lookup"><span data-stu-id="09a27-127">Add the following two constants and your *client* variable to the Program class:</span></span>

    ```csharp
    public class Program
    {
        // ADD THIS PART TO YOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;
    ```

    <!--TODO: Use more secure method-->

9. <span data-ttu-id="09a27-128">Copie a sua cadeia de ligação da extensão do Azure Cosmos DB ao clicar com o botão direito na conta do learning-module e clicar **Copiar Cadeia de Ligação**.</span><span class="sxs-lookup"><span data-stu-id="09a27-128">Copy your connection string from the Azure Cosmos DB extension by right-clicking the learning-module account, and clicking **Copy Connection String**.</span></span>

    ![Extensão do Azure Cosmos DB para o Visual Studio Code](../media/2-setup/vs-code-copy-connection-string.gif) 

10. <span data-ttu-id="09a27-130">Cole a cadeia de ligação num ficheiro de texto e, em seguida, copie a parte de **AccountEndpoint** do ficheiro de texto para o **EndpointUrl** no Program.cs.</span><span class="sxs-lookup"><span data-stu-id="09a27-130">Paste the connection string into a text file, and then copy the **AccountEndpoint** portion from the text file into the **EndpointUrl** in Program.cs.</span></span>

    <span data-ttu-id="09a27-131">O AccountEndpoint deverá ser semelhante ao seguinte código:</span><span class="sxs-lookup"><span data-stu-id="09a27-131">The AccountEndpoint should look like the following code:</span></span>

    ```csharp
    private const string EndpointUrl = "https://<account name>.documents.azure.com:443/;
    ```

12. <span data-ttu-id="09a27-132">Agora copie o valor **AccountKey** do valor de texto para o valor de **PrimaryKey** em Program.cs.</span><span class="sxs-lookup"><span data-stu-id="09a27-132">Now copy the **AccountKey** value from the text value into the **PrimaryKey** value in Program.cs.</span></span>

12. <span data-ttu-id="09a27-133">No terminal integrado, escreva o comando seguinte para executar o programa para garantir que executa.</span><span class="sxs-lookup"><span data-stu-id="09a27-133">In the integrated terminal, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

13. <span data-ttu-id="09a27-134">Adicione uma nova tarefa assíncrona para criar um novo cliente e verifique se a base de dados de Utilizadores existe ao adicionar o seguinte método após o método principal.</span><span class="sxs-lookup"><span data-stu-id="09a27-134">Add a new asynchronous task to create a new client, and check whether the Users database exists by adding the following method after the main method.</span></span>
    
    ```csharp
    private async Task BasicOperations()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "Users" });

        await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("Users"), new DocumentCollection { Id = "WebCustomers" });
    }
    ```

14. <span data-ttu-id="09a27-135">No terminal integrado, escreva novamente o seguinte comando para executar o programa para garantir que executa.</span><span class="sxs-lookup"><span data-stu-id="09a27-135">In the integrated terminal, again, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

15. <span data-ttu-id="09a27-136">Copie e cole o código seguinte no método **Main**, a substituir a linha atual `Console.WriteLine("Hello World!");`.</span><span class="sxs-lookup"><span data-stu-id="09a27-136">Copy and paste the following code into the **Main** method, overwriting the current `Console.WriteLine("Hello World!");` line.</span></span>

    ```csharp
    try
            {
                    Program p = new Program();
                    p.BasicOperations().Wait();
            }
            catch (DocumentClientException de)
            {
                    Exception baseException = de.GetBaseException();
                    Console.WriteLine("{0} error occurred: {1}, Message: {2}", de.StatusCode, de.Message, baseException.Message);
            }
            catch (Exception e)
            {
                    Exception baseException = e.GetBaseException();
                    Console.WriteLine("Error: {0}, Message: {1}", e.Message, baseException.Message);
            }
            finally
            {
                    Console.WriteLine("End of demo, press any key to exit.");
                    Console.ReadKey();
            }
    ```

16. <span data-ttu-id="09a27-137">No terminal integrado, escreva novamente o seguinte comando para executar o programa para garantir que executa.</span><span class="sxs-lookup"><span data-stu-id="09a27-137">In the integrated terminal, again, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

    <span data-ttu-id="09a27-138">A consola apresenta o seguinte resultado.</span><span class="sxs-lookup"><span data-stu-id="09a27-138">The console displays the following output.</span></span>
    
    ```
    Database and collection validation complete
    End of demo, press any key to exit.
    ```

## <a name="summary"></a><span data-ttu-id="09a27-139">Resumo</span><span class="sxs-lookup"><span data-stu-id="09a27-139">Summary</span></span>

<span data-ttu-id="09a27-140">Neste módulo, vai configurar a base para a sua aplicação Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="09a27-140">In this module, you set up the groundwork for your Azure Cosmos DB application.</span></span> <span data-ttu-id="09a27-141">Configurou o seu ambiente de desenvolvimento no Visual Studio Code, criou um simples projeto HelloWorld, ligou o projeto ao ponto final Azure Cosmos DB e certificou-se de que a sua base de dados e coleção existem.</span><span class="sxs-lookup"><span data-stu-id="09a27-141">You set up your development environment in Visual Studio Code, created a simple HelloWorld project, connected the project to the Azure Cosmos DB endpoint, and ensured your database and collection exist.</span></span>