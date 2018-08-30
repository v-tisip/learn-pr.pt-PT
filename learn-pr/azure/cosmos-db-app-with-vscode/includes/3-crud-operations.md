<!--TODO: explain Etag in knowledge needed-->
<!--TODO: Update to weave in the online retailer story-->


Os dados são armazenados em documentos JSON no Azure Cosmos DB. Os [documentos](https://docs.microsoft.com/azure/cosmos-db/sql-api-resources#documents) podem ser criados, obtidos, substituídos ou eliminados no portal, conforme mostrado no módulo anterior, ou através de programação, conforme descrito neste módulo. O Azure Cosmos DB disponibiliza SDKs no lado do cliente para .NET, .NET Core, Java, Node.js e Python, cada um deles suporta estas operações. Neste módulo vamos utilizar o SDK .NET Core para executar operações CRUD (criar, obter, atualizar e eliminar). 

As principais operações dos documentos do Azure Cosmos DB fazem parte da classe [DocumentClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet):
* [CreateDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentasync?view=azure-dotnet)
* [ReadDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentasync?view=azure-dotnet)
* [ReplaceDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.replacedocumentasync?view=azure-dotnet)
* [UpsertDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.upsertdocumentasync?view=azure-dotnet). O modo Upsert realiza uma operação de criação ou substituição, dependendo se o documento já existe.
* [DeleteDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.deletedocumentasync?view=azure-dotnet)

Para efetuar qualquer uma destas operações, terá de criar uma classe que represente o objeto armazenado na base de dados. Uma vez que estamos a trabalhar com uma base de dados de utilizadores, deverá criar uma classe **Utilizador** para armazenar os dados primários como os nomes e UserId deles (o que é necessário, já que essa é a chave de partição que permite o dimensionamento horizontal) e subclasses para preferências de envio e histórico de pedidos.

Depois de ter essas classes criadas para representar os utilizadores, vai criar novos documentos de utilizador para cada instância e, em seguida, realizar algumas operações CRUD simples nos documentos.

## <a name="create-documents"></a>Criar documentos

1. Primeiro, crie uma classe **Utilizador** que represente os objetos a armazenar no Azure Cosmos DB. Também vamos criar as subclasses **OrderHistory** e **ShippingPreference** que são utilizadas dentro da classe **Utilizador**. Tenha em atenção que os documentos têm de ter um **Id** propriedade serializado como **id** no JSON. 

    Para criar essas classes, copie e cole as classes **Utilizador**, **OrderHistory**, **ShippingPreference** seguintes por baixo do método **BasicOperations**.

    <!--TODO: specify JSON for all of these? -->
    ```csharp
    public class User
    {
            [JsonProperty("id")]
            public string Id { get; set; }
            [JsonProperty("userId")]
            public string UserId { get; set; }
            [JsonProperty("lastName")]
            public string LastName { get; set; }
            [JsonProperty("firstName")]
            public string FirstName { get; set; }
            [JsonProperty("email")]
            public string Email { get; set; }
            [JsonProperty("dividend")]
            public string Dividend { get; set; }
            public OrderHistory[] OrderHistory { get; set; }
            public ShippingPreference[] ShippingPreference { get; set; }
            public CouponsUsed[] Coupons { get; set; }
            public override string ToString()
            {
            return JsonConvert.SerializeObject(this);
            }
    }
    
    public class OrderHistory
    {
            public string OrderId { get; set; }
            public string DateShipped { get; set; }
            public string Total { get; set; }
    }
    
    public class ShippingPreference
    {
            public int Priority { get; set; }
            public string AddressLine1 { get; set; }
            public string AddressLine2 { get; set; }
            public string City { get; set; }
            public string State { get; set; }
            public string ZipCode { get; set; }
            public string Country { get; set; }
    }
    
    public class CouponsUsed
    {
            public string CouponCode { get; set; }
    
    }
    
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key to continue ...");
            Console.ReadKey();
    }
    ```

2. No terminal integrado, escreva o comando seguinte para executar o programa com êxito.

    ```csharp
    dotnet run
    ```

3. Agora, copie e cole a tarefa **CreateUserDocumentIfNotExists** na classe **ShippingPreference**.

    ```csharp
    private async Task CreateUserDocumentIfNotExists(string databaseName, string collectionName, User user)
    {
            try
            {
            await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, user.Id), new RequestOptions { PartitionKey = new PartitionKey("user.userId") });
            this.WriteToConsoleAndPromptToContinue("Found {0}", user.Id);
            }
            catch (DocumentClientException de)
            {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                    await this.client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), user);
                    this.WriteToConsoleAndPromptToContinue("Created User {0}", user.Id);
            }
            else
            {
                    throw;
            }
            }
    }
    ```

4. Em seguida, adicione o seguinte ao método **BasicOperations**.

    ```csharp
     User yanhe = new User
                {
                    Id = "1",
                    UserId = "yanhe",
                    LastName = "He",
                    FirstName = "Yan",
                    Email = "yanhe@todo.com",
                    OrderHistory = new OrderHistory[]
            {
                new OrderHistory {
                    OrderId = "1000",
                    DateShipped = "08/17/2018",
                    Total = "52.49"
                }
            },
                    ShippingPreference = new ShippingPreference[]
            {
                    new ShippingPreference {
                            Priority = 1,
                            AddressLine1 = "90 W 8th St",
                            City = "New York",
                            State = "NY",
                            ZipCode = "10001",
                            Country = "USA"
                    }
            },
                };
    
                await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", yanhe);
    
                User nelapin = new User
                {
                    Id = "2",
                    UserId = "nelapin",
                    LastName = "Pindakova",
                    FirstName = "Nela",
                    Email = "nelapin@todo.com",
                    Dividend = "8.50",
                    OrderHistory = new OrderHistory[]
            {
                new OrderHistory {
                    OrderId = "1001",
                    DateShipped = "08/17/2018",
                    Total = "105.89"
                }
            },
                    ShippingPreference = new ShippingPreference[]
            {
                    new ShippingPreference {
                            Priority = 1,
                            AddressLine1 = "505 NW 5th St",
                            City = "New York",
                            State = "NY",
                            ZipCode = "10001",
                            Country = "USA"
                    },
                    new ShippingPreference {
                            Priority = 2,
                            AddressLine1 = "505 NW 5th St",
                            City = "New York",
                            State = "NY",
                            ZipCode = "10001",
                            Country = "USA"
                    }
            },
                    Coupons = new CouponsUsed[]
             {
                 new CouponsUsed{
                     CouponCode = "Fall2018"
                 }
             }
                };
    
                await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);
    ```

5. No terminal integrado, escreva de novo o comando seguinte para executar o programa com êxito.

    ```csharp
    dotnet run
    ```

    O terminal apresenta a saída seguinte, que indica que ambos os registos de utilizador foram criados com êxito. 

    ```
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

## <a name="read-documents"></a>Ler documentos

1. Para ler os documentos da base de dados, copie o código a seguir e coloque-o no final do ficheiro Program.cs.

    ```csharp
    private async Task ReadUserDocument(string databaseName, string collectionName, User user)
    {
            try
            {
            await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, user.Id), new RequestOptions { PartitionKey = new PartitionKey("user.userId") });
            this.WriteToConsoleAndPromptToContinue("Found user {0}", user.Id);
            }
            catch (DocumentClientException de)
            {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                this.WriteToConsoleAndPromptToContinue("User {0} not found", user.Id);
            }
            else
            {
                throw;
            }
            }
    }
    ```

2.  Copie e cole o código seguinte no final do método **BasicOperations**, depois da linha `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);`.

    ```csharp
    await this.ReadUserDocument("Users", "WebCustomers", yanhe);
    ```

4. Guarde o ficheiro Program.cs e, no terminal integrado, execute o comando seguinte.

    ```
    dotnet run
    ```
    O terminal apresenta o resultado seguinte, no qual a saída “Foi encontrado o utilizador 1” indica que o documento foi encontrado.

    ```
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    Found user 1
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

## <a name="replace-documents"></a>Substituir documentos
O Azure Cosmos DB suporta a substituição de documentos JSON. Neste caso, vamos atualizar um registo de utilizador para considerar uma alteração nos apelidos.

1. Copie e cole o método **ReplaceFamilyDocument** por baixo do método **CreateUserDocumentIfNotExists**.

    ```csharp
    private async Task ReplaceUserDocument(string databaseName, string collectionName, string LastName, User updatedUser)
    {
        await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, LastName), updatedUser);
        this.WriteToConsoleAndPromptToContinue("Replaced last name for {0}", LastName);
    }
    ```

2. Copie e cole o código seguinte no final do método **BasicOperations**, depois da linha `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);`.

    ```csharp
    yanhe.LastName = "Suh";
    await this.ReplaceUserDocument("Users", "WebCustomers", yanhe.LastName, yanhe);
    ```
    <!--TODO: need to fix this as it's giving an error-->

4. Guarde o ficheiro Program.cs e, no terminal integrado, execute o comando seguinte.

    ```
    dotnet run
    ```
    O terminal apresenta o resultado seguinte, no qual a saída “Substituído apelido para Suh” indica que o documento foi substituído.

    ```
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    Found user 1
    Press any key to continue ...
    Replaced last name for Suh 
    End of demo, press any key to exit.
    ```

## <a name="delete-documents"></a>Eliminar documentos

1. Copie e cole o método **DeleteUserDocument** por baixo do método **ReplaceUserDocument**.
    
    ```csharp
    private async Task DeleteUserDocument(string databaseName, string collectionName, string documentName)
    {
        await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName), new RequestOptions { PartitionKey = new PartitionKey("User.UserId") });
        Console.WriteLine("Deleted User {0}", documentName);
    }
    ```

2. Copie e cole o código seguinte no método **BasicOperations**, por baixo da segunda execução de consulta.

    ```csharp
    await this.DeleteUserDocument("Users", "WebCustomers", "1");
    ```

3. Guarde o ficheiro Program.cs e, no terminal integrado, execute o comando seguinte.

    ```
    dotnet run
    ```

    Parabéns! Eliminou documentos do Azure Cosmos DB com êxito.

## <a name="summary"></a>Resumo

Nessa unidade, criou, substituiu e eliminou documentos na base de dados do Azure Cosmos DB.