<!--TODO: explain Etag in knowledge needed-->
<!--TODO: Update to weave in the online retailer story-->


<span data-ttu-id="135b7-101">Os dados são armazenados em documentos JSON no Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="135b7-101">Data is stored in JSON documents in Azure Cosmos DB.</span></span> <span data-ttu-id="135b7-102">Os [documentos](https://docs.microsoft.com/azure/cosmos-db/sql-api-resources#documents) podem ser criados, obtidos, substituídos ou eliminados no portal, conforme mostrado no módulo anterior, ou através de programação, conforme descrito neste módulo.</span><span class="sxs-lookup"><span data-stu-id="135b7-102">[Documents](https://docs.microsoft.com/azure/cosmos-db/sql-api-resources#documents) can be created, retrieved, replaced, or deleted in the portal, as shown in the previous module, or programmatically, as described in this module.</span></span> <span data-ttu-id="135b7-103">O Azure Cosmos DB disponibiliza SDKs no lado do cliente para .NET, .NET Core, Java, Node.js e Python, cada um deles suporta estas operações.</span><span class="sxs-lookup"><span data-stu-id="135b7-103">Azure Cosmos DB provides client-side SDKs for .NET, .NET Core, Java, Node.js, and Python, each of which supports these operations.</span></span> <span data-ttu-id="135b7-104">Neste módulo vamos utilizar o SDK .NET Core para executar operações CRUD (criar, obter, atualizar e eliminar).</span><span class="sxs-lookup"><span data-stu-id="135b7-104">In this module we'll be using the .NET Core SDK to perform CRUD (create, retrieve, update, and delete) operations.</span></span> 

<span data-ttu-id="135b7-105">As principais operações dos documentos do Azure Cosmos DB fazem parte da classe [DocumentClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet):</span><span class="sxs-lookup"><span data-stu-id="135b7-105">The main operations for Azure Cosmos DB documents are part of the [DocumentClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) class:</span></span>
* [<span data-ttu-id="135b7-106">CreateDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="135b7-106">CreateDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentasync?view=azure-dotnet)
* [<span data-ttu-id="135b7-107">ReadDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="135b7-107">ReadDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentasync?view=azure-dotnet)
* [<span data-ttu-id="135b7-108">ReplaceDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="135b7-108">ReplaceDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.replacedocumentasync?view=azure-dotnet)
* <span data-ttu-id="135b7-109">[UpsertDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.upsertdocumentasync?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="135b7-109">[UpsertDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.upsertdocumentasync?view=azure-dotnet).</span></span> <span data-ttu-id="135b7-110">O modo Upsert realiza uma operação de criação ou substituição, dependendo se o documento já existe.</span><span class="sxs-lookup"><span data-stu-id="135b7-110">Upsert performs a create or replace operation depending on whether the document already exists.</span></span>
* [<span data-ttu-id="135b7-111">DeleteDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="135b7-111">DeleteDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.deletedocumentasync?view=azure-dotnet)

<span data-ttu-id="135b7-112">Para efetuar qualquer uma destas operações, terá de criar uma classe que represente o objeto armazenado na base de dados.</span><span class="sxs-lookup"><span data-stu-id="135b7-112">To perform any of these operations, you need to create a class that represents the object stored in the database.</span></span> <span data-ttu-id="135b7-113">Uma vez que estamos a trabalhar com uma base de dados de utilizadores, deverá criar uma classe **Utilizador** para armazenar os dados primários como os nomes e UserId deles (o que é necessário, já que essa é a chave de partição que permite o dimensionamento horizontal) e subclasses para preferências de envio e histórico de pedidos.</span><span class="sxs-lookup"><span data-stu-id="135b7-113">Because we're working with a database of users, you'll want to create a **User** class to store primary data such as their name and UserId (which is required, as that's the partition key to enable horizontal scaling) and subclasses for shipping preferences and order history.</span></span>

<span data-ttu-id="135b7-114">Depois de ter essas classes criadas para representar os utilizadores, vai criar novos documentos de utilizador para cada instância e, em seguida, realizar algumas operações CRUD simples nos documentos.</span><span class="sxs-lookup"><span data-stu-id="135b7-114">Once you have those classes created to represent your users, you'll create new user documents for each instance, and then we'll perform some simple CRUD operations on the documents.</span></span>

## <a name="create-documents"></a><span data-ttu-id="135b7-115">Criar documentos</span><span class="sxs-lookup"><span data-stu-id="135b7-115">Create documents</span></span>

1. <span data-ttu-id="135b7-116">Primeiro, crie uma classe **Utilizador** que represente os objetos a armazenar no Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="135b7-116">First, create a **User** class that represents the objects to store in Azure Cosmos DB.</span></span> <span data-ttu-id="135b7-117">Também vamos criar as subclasses **OrderHistory** e **ShippingPreference** que são utilizadas dentro da classe **Utilizador**.</span><span class="sxs-lookup"><span data-stu-id="135b7-117">We will also create **OrderHistory** and **ShippingPreference** subclasses that are used within **User**.</span></span> <span data-ttu-id="135b7-118">Tenha em atenção que os documentos têm de ter um **Id** propriedade serializado como **id** no JSON.</span><span class="sxs-lookup"><span data-stu-id="135b7-118">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> 

    <span data-ttu-id="135b7-119">Para criar essas classes, copie e cole as classes **Utilizador**, **OrderHistory**, **ShippingPreference** seguintes por baixo do método **BasicOperations**.</span><span class="sxs-lookup"><span data-stu-id="135b7-119">To create these classes, copy and paste the following **User**, **OrderHistory**, **ShippingPreference** classes underneath the **BasicOperations** method.</span></span>

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

2. <span data-ttu-id="135b7-120">No terminal integrado, escreva o comando seguinte para executar o programa com êxito.</span><span class="sxs-lookup"><span data-stu-id="135b7-120">In the integrated terminal, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

3. <span data-ttu-id="135b7-121">Agora, copie e cole a tarefa **CreateUserDocumentIfNotExists** na classe **ShippingPreference**.</span><span class="sxs-lookup"><span data-stu-id="135b7-121">Now copy and paste the **CreateUserDocumentIfNotExists** task under the **ShippingPreference** class.</span></span>

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

4. <span data-ttu-id="135b7-122">Em seguida, adicione o seguinte ao método **BasicOperations**.</span><span class="sxs-lookup"><span data-stu-id="135b7-122">Then add the following to the **BasicOperations** method.</span></span>

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

5. <span data-ttu-id="135b7-123">No terminal integrado, escreva de novo o comando seguinte para executar o programa com êxito.</span><span class="sxs-lookup"><span data-stu-id="135b7-123">In the integrated terminal, again, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

    <span data-ttu-id="135b7-124">O terminal apresenta a saída seguinte, que indica que ambos os registos de utilizador foram criados com êxito.</span><span class="sxs-lookup"><span data-stu-id="135b7-124">The terminal displays the following output, indicating that both user records were successfully created.</span></span> 

    ```
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

## <a name="read-documents"></a><span data-ttu-id="135b7-125">Ler documentos</span><span class="sxs-lookup"><span data-stu-id="135b7-125">Read documents</span></span>

1. <span data-ttu-id="135b7-126">Para ler os documentos da base de dados, copie o código a seguir e coloque-o no final do ficheiro Program.cs.</span><span class="sxs-lookup"><span data-stu-id="135b7-126">To read documents from the database, copy in the following code and place it at the end of the Program.cs file.</span></span>

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

2.  <span data-ttu-id="135b7-127">Copie e cole o código seguinte no final do método **BasicOperations**, depois da linha `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);`.</span><span class="sxs-lookup"><span data-stu-id="135b7-127">Copy and paste the following code to the end of the **BasicOperations** method, after the `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);` line.</span></span>

    ```csharp
    await this.ReadUserDocument("Users", "WebCustomers", yanhe);
    ```

4. <span data-ttu-id="135b7-128">Guarde o ficheiro Program.cs e, no terminal integrado, execute o comando seguinte.</span><span class="sxs-lookup"><span data-stu-id="135b7-128">Save the Program.cs file and then, in the integrated terminal, run the following command.</span></span>

    ```
    dotnet run
    ```
    <span data-ttu-id="135b7-129">O terminal apresenta o resultado seguinte, no qual a saída “Foi encontrado o utilizador 1” indica que o documento foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="135b7-129">The terminal displays the following output, where the output "Found user 1" indicates the document was found.</span></span>

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

## <a name="replace-documents"></a><span data-ttu-id="135b7-130">Substituir documentos</span><span class="sxs-lookup"><span data-stu-id="135b7-130">Replace documents</span></span>
<span data-ttu-id="135b7-131">O Azure Cosmos DB suporta a substituição de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="135b7-131">Azure Cosmos DB supports replacing JSON documents.</span></span> <span data-ttu-id="135b7-132">Neste caso, vamos atualizar um registo de utilizador para considerar uma alteração nos apelidos.</span><span class="sxs-lookup"><span data-stu-id="135b7-132">In this case, we'll update a user record to account for a change to their last name.</span></span>

1. <span data-ttu-id="135b7-133">Copie e cole o método **ReplaceFamilyDocument** por baixo do método **CreateUserDocumentIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="135b7-133">Copy and paste the **ReplaceFamilyDocument** method underneath your **CreateUserDocumentIfNotExists** method.</span></span>

    ```csharp
    private async Task ReplaceUserDocument(string databaseName, string collectionName, string LastName, User updatedUser)
    {
        await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, LastName), updatedUser);
        this.WriteToConsoleAndPromptToContinue("Replaced last name for {0}", LastName);
    }
    ```

2. <span data-ttu-id="135b7-134">Copie e cole o código seguinte no final do método **BasicOperations**, depois da linha `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);`.</span><span class="sxs-lookup"><span data-stu-id="135b7-134">Copy and paste the following code to the end of the **BasicOperations** method, after the `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);` line.</span></span>

    ```csharp
    yanhe.LastName = "Suh";
    await this.ReplaceUserDocument("Users", "WebCustomers", yanhe.LastName, yanhe);
    ```
    <!--TODO: need to fix this as it's giving an error-->

4. <span data-ttu-id="135b7-135">Guarde o ficheiro Program.cs e, no terminal integrado, execute o comando seguinte.</span><span class="sxs-lookup"><span data-stu-id="135b7-135">Save the Program.cs file and then, in the integrated terminal, run the following command.</span></span>

    ```
    dotnet run
    ```
    <span data-ttu-id="135b7-136">O terminal apresenta o resultado seguinte, no qual a saída “Substituído apelido para Suh” indica que o documento foi substituído.</span><span class="sxs-lookup"><span data-stu-id="135b7-136">The terminal displays the following output, where the output "Replaced last name for Suh" indicates the document was replaced.</span></span>

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

## <a name="delete-documents"></a><span data-ttu-id="135b7-137">Eliminar documentos</span><span class="sxs-lookup"><span data-stu-id="135b7-137">Delete documents</span></span>

1. <span data-ttu-id="135b7-138">Copie e cole o método **DeleteUserDocument** por baixo do método **ReplaceUserDocument**.</span><span class="sxs-lookup"><span data-stu-id="135b7-138">Copy and paste the **DeleteUserDocument** method underneath your **ReplaceUserDocument** method.</span></span>
    
    ```csharp
    private async Task DeleteUserDocument(string databaseName, string collectionName, string documentName)
    {
        await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName), new RequestOptions { PartitionKey = new PartitionKey("User.UserId") });
        Console.WriteLine("Deleted User {0}", documentName);
    }
    ```

2. <span data-ttu-id="135b7-139">Copie e cole o código seguinte no método **BasicOperations**, por baixo da segunda execução de consulta.</span><span class="sxs-lookup"><span data-stu-id="135b7-139">Copy and paste the following code to your **BasicOperations** method underneath the second query execution.</span></span>

    ```csharp
    await this.DeleteUserDocument("Users", "WebCustomers", "1");
    ```

3. <span data-ttu-id="135b7-140">Guarde o ficheiro Program.cs e, no terminal integrado, execute o comando seguinte.</span><span class="sxs-lookup"><span data-stu-id="135b7-140">Save the Program.cs file and then, in the integrated terminal, run the following command.</span></span>

    ```
    dotnet run
    ```

    <span data-ttu-id="135b7-141">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="135b7-141">Congratulations!</span></span> <span data-ttu-id="135b7-142">Eliminou documentos do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="135b7-142">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <a name="summary"></a><span data-ttu-id="135b7-143">Resumo</span><span class="sxs-lookup"><span data-stu-id="135b7-143">Summary</span></span>

<span data-ttu-id="135b7-144">Nessa unidade, criou, substituiu e eliminou documentos na base de dados do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="135b7-144">In this unit you created, replaced, and deleted documents in your Azure Cosmos DB database.</span></span>