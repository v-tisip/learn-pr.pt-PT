Neste módulo, vai criar uma simples aplicação de consola ao utilizar o terminal integrado, instalar pacotes NuGet e utilizar a extensão do Azure Cosmos DB para ver as bases de dados e coleções criadas no módulo anterior. Vai obter a sua cadeia de ligação do Azure Cosmos DB a partir da extensão e então começar a programar em relação ao Azure Cosmos DB. 

## <a name="create-a-console-app"></a>Criar uma aplicação de consola

1. Abra o Visual Studio Code e, em seguida, selecione **Ficheiro** > **Abrir Pasta**.

2. Crie uma nova pasta chamada **learning-module** onde quer que esteja seu novo projeto em C# e em seguida clique em **Selecionar Pasta**.

2. Abra o terminal integrado do Visual Studio Code ao selecionar **Ver** > **Terminal Integrado** no menu principal.

3. Na janela do terminal, escreva **dotnet new console**.

    Este comando cria um ficheiro **Program.cs** na sua pasta com um simples programa "Olá, mundo!" já escrito, juntamente com um ficheiro de projeto C# chamado **learning-module.csproj**.

4. Na janela de terminal, escreva o seguinte comando para executar o programa "Olá, mundo!". 

    ```
    dotnet run
    ```

    A janela de terminal exibe "Olá, mundo!" como saída.

## <a name="connect-the-app-to-azure-cosmos-db"></a>Ligar a aplicação ao Azure Cosmos DB

1. Inicie sessão no Azure ao clicar em **Ver** > **Paleta de Comandos** e escrever **Azure: Iniciar Sessão**.

    Siga as instruções para copiar e colar o código fornecido no seu browser, que o autentica na sua sessão do Visual Studio Code.

2. Clique no ![ícone do Explorer](../media/2-setup/visual-studio-code-explorer-icon.png), ícone **Explorer** no menu da esquerda e, em seguida, aumente o **Azure Cosmos DB**.

3. Aumentar a sua subscrição do Azure > conta do Azure Cosmos DB. Se tiver criado a base de dados de **Produtos** e a coleção **Vestuário** nos módulos anteriores, a extensão mostra-os.

   ![Extensão do Azure Cosmos DB para o Visual Studio Code](../media/2-setup/azure-cosmos-db-vs-code-extension.png) 

4. Agora vamos criar uma nova base de dados e coleção para os seus clientes.

    Na janela do Explorador, clique com o botão direito na sua conta e então em **Criar Base de Dados**. 
    
    Na caixa de texto na parte superior do ecrã, escreva **Utilizadores** para o nome de base de dados > **Introduzir** > **WebCustomers** para o nome da coleção >  **Introduzir** > **userId** para a chave de partição > **Introduzir** > **1000** para a capacidade de taxa de transferência inicial > **Introduzir**.

    ![Extensão do Azure Cosmos DB para o Visual Studio Code](../media/2-setup/vs-code-azure-cosmos-db-extension.gif) <!--Retake on fresh machine without the other subscriptions showing-->

    A nova base de dados de Utilizadores e coleção WebCustomers são exibidas na janela do Explorador.

5. No terminal integrado, tem de executar cada um dos seguintes comandos numa nova linha de comandos para instalar os pacotes de NuGet necessários.

    ```
    dotnet add package System.Net.Http
    dotnet add package Microsoft.Azure.DocumentDB.Core
    dotnet add package Newtonsoft.Json
    dotnet add package System.Threading.Tasks
    dotnet add package System.Linq
    dotnet add package Bogus
    dotnet restore
    ```

6. Na parte superior do painel do Explorador, clique em **Program.cs** para abrir o ficheiro.

7. Adicione as seguintes instruções using após `using System;`.

    ```csharp
    using System.Linq;
    using System.Threading.Tasks;
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;
    ```

8. Adicione as duas constantes seguintes e a sua variável de *cliente* à classe Program:

    ```csharp
    public class Program
    {
        // ADD THIS PART TO YOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;
    ```

    <!--TODO: Use more secure method-->

9. Copie a sua cadeia de ligação da extensão do Azure Cosmos DB ao clicar com o botão direito na conta do learning-module e clicar **Copiar Cadeia de Ligação**.

    ![Extensão do Azure Cosmos DB para o Visual Studio Code](../media/2-setup/vs-code-copy-connection-string.gif) 

10. Cole a cadeia de ligação num ficheiro de texto e, em seguida, copie a parte de **AccountEndpoint** do ficheiro de texto para o **EndpointUrl** no Program.cs.

    O AccountEndpoint deverá ser semelhante ao seguinte código:

    ```csharp
    private const string EndpointUrl = "https://<account name>.documents.azure.com:443/;
    ```

12. Agora copie o valor **AccountKey** do valor de texto para o valor de **PrimaryKey** em Program.cs.

12. No terminal integrado, escreva o comando seguinte para executar o programa para garantir que executa.

    ```csharp
    dotnet run
    ```

13. Adicione uma nova tarefa assíncrona para criar um novo cliente e verifique se a base de dados de Utilizadores existe ao adicionar o seguinte método após o método principal.
    
    ```csharp
    private async Task BasicOperations()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "Users" });

        await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("Users"), new DocumentCollection { Id = "WebCustomers" });
    }
    ```

14. No terminal integrado, escreva novamente o seguinte comando para executar o programa para garantir que executa.

    ```csharp
    dotnet run
    ```

15. Copie e cole o código seguinte no método **Main**, a substituir a linha atual `Console.WriteLine("Hello World!");`.

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

16. No terminal integrado, escreva novamente o seguinte comando para executar o programa para garantir que executa.

    ```csharp
    dotnet run
    ```

    A consola apresenta o seguinte resultado.
    
    ```
    Database and collection validation complete
    End of demo, press any key to exit.
    ```

## <a name="summary"></a>Resumo

Neste módulo, vai configurar a base para a sua aplicação Azure Cosmos DB. Configurou o seu ambiente de desenvolvimento no Visual Studio Code, criou um simples projeto HelloWorld, ligou o projeto ao ponto final Azure Cosmos DB e certificou-se de que a sua base de dados e coleção existem.