<span data-ttu-id="edc45-101"><!--TODO: Explain how to do ExecuteNext (pages closer to SDK imp) vs ToList (continuation token)--> Agora que criou documentos na aplicação, vamos consultá-los.</span><span class="sxs-lookup"><span data-stu-id="edc45-101"><!--TODO: Explain how to do ExecuteNext (pages closer to SDK imp) vs ToList (continuation token)--> Now that you've created documents in your application, let's query them from your application.</span></span> <span data-ttu-id="edc45-102">O Azure Cosmos DB utiliza consultas SQL e consultas LINQ.</span><span class="sxs-lookup"><span data-stu-id="edc45-102">Azure Cosmos DB uses SQL queries and LINQ queries.</span></span> <span data-ttu-id="edc45-103">Abordamos as consultas SQL e como executá-las no portal no módulo **Adicionar dados e consultar dados na base de dados**.</span><span class="sxs-lookup"><span data-stu-id="edc45-103">SQL queries and how to run them in the portal is discussed in the **Add data and query data in your database** module.</span></span> 

<span data-ttu-id="edc45-104">Portanto, esta unidade concentra-se em executar consultas SQL e consultas LINQ a partir da aplicação.</span><span class="sxs-lookup"><span data-stu-id="edc45-104">So this unit focuses on running SQL queries and LINQ queries from your application.</span></span>

<span data-ttu-id="edc45-105">Vamos utilizar os documentos de utilizador que criou para a aplicação de retalhista online para testar estas consultas.</span><span class="sxs-lookup"><span data-stu-id="edc45-105">We'll use the user documents you've created for your online retailer application to test these queries.</span></span>

## <a name="linq-query-basics"></a><span data-ttu-id="edc45-106">Noções básicas da consultas LINQ</span><span class="sxs-lookup"><span data-stu-id="edc45-106">LINQ query basics</span></span>

<span data-ttu-id="edc45-107">O LINQ é um modelo de programação do .NET que expressa os cálculos como consultas em fluxos de objetos.</span><span class="sxs-lookup"><span data-stu-id="edc45-107">LINQ is a .NET programming model that expresses computations as queries on streams of objects.</span></span> <span data-ttu-id="edc45-108">Pode criar um objeto **IQueryable** para consultar diretamente o Azure Cosmos DB, o que converte a consulta LINQ numa consulta do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="edc45-108">You can create an **IQueryable** object that directly queries Azure Cosmos DB, which translates the LINQ query into a Cosmos DB query.</span></span> <span data-ttu-id="edc45-109">A consulta é, em seguida, passada para o servidor do Azure Cosmos DB para obter um conjunto de resultados no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="edc45-109">The query is then passed to the Azure Cosmos DB server to retrieve a set of results in JSON format.</span></span> <span data-ttu-id="edc45-110">Os resultados devolvidos terão a serialização anulada num fluxo de objetos do .NET no lado do cliente.</span><span class="sxs-lookup"><span data-stu-id="edc45-110">The returned results are deserialized into a stream of .NET objects on the client side.</span></span> <span data-ttu-id="edc45-111">Muitos programadores preferem consultas LINQ, dado que fornecem um modelo de programação consistente da forma como trabalham com objetos no código da aplicação e de como expressam a lógica de consulta em execução na base de dados.</span><span class="sxs-lookup"><span data-stu-id="edc45-111">Many developers prefer LINQ queries, as they provide a single consistent programming model across how they work with objects in application code and how they express query logic running in the database.</span></span>

<span data-ttu-id="edc45-112">A tabela seguinte mostra como as consultas LINQ são convertidas em SQL.</span><span class="sxs-lookup"><span data-stu-id="edc45-112">The following table shows how LINQ queries are translated into SQL.</span></span>

| <span data-ttu-id="edc45-113">Expressão LINQ</span><span class="sxs-lookup"><span data-stu-id="edc45-113">LINQ expression</span></span> | <span data-ttu-id="edc45-114">Conversão SQL</span><span class="sxs-lookup"><span data-stu-id="edc45-114">SQL translation</span></span> |
|---|---|
| `input.Select(family => family.parents[0].familyName);`| `SELECT VALUE f.parents[0].familyName FROM Families f` |
|`input.Select(family => family.children[0].grade + c); // c is an int variable` | `SELECT VALUE f.children[0].grade + c FROM Families f` |
|`input.Select(family => new { name = family.children[0].familyName, grade = family.children[0].grade + 3});`| `SELECT VALUE {"name":f.children[0].familyName, "grade": f.children[0].grade + 3 } FROM Families f`|
|`input.Where(family=> family.parents[0].familyName == "Smith");`|`SELECT * FROM Families f WHERE f.parents[0].familyName = "Smith"`|

## <a name="run-sql-and-linq-queries"></a><span data-ttu-id="edc45-115">Executar consultas SQL e LINQ</span><span class="sxs-lookup"><span data-stu-id="edc45-115">Run SQL and LINQ queries</span></span>

1. <span data-ttu-id="edc45-116">O exemplo a seguir mostra como uma consulta pode ser realizada no SQL, no LINQ ou no LINQ lambda a partir do código .NET.</span><span class="sxs-lookup"><span data-stu-id="edc45-116">The following sample shows how a query could be performed in SQL, LINQ, or LINQ lambda from your .NET code.</span></span> <span data-ttu-id="edc45-117">Copie o código e adicione-o após o método **DeleteUserDocument**.</span><span class="sxs-lookup"><span data-stu-id="edc45-117">Copy the code and add it after your **DeleteUserDocument** method.</span></span>

    ```csharp
    private void ExecuteSimpleQuery(string databaseName, string collectionName)
    {
        // Set some common query options
        FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1 };
    
            // Here we find the Andersen family via its LastName
            IQueryable<USer> userQuery = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                    .Where(u => u.LastName == "Sun");
    
            // The query is executed synchronously here, but can also be executed asynchronously via the IDocumentQuery<T> interface
            Console.WriteLine("Running LINQ query...");
            foreach (User user in userQuery)
            {
                Console.WriteLine("\tRead {0}", user);
            }
    
            // Now execute the same query via direct SQL
            IQueryable<User> userQueryInSql = this.client.CreateDocumentQuery<User>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                    "SELECT * FROM User WHERE User.LastName = 'Sun'",
                    queryOptions);
    
            Console.WriteLine("Running direct SQL query...");
            foreach (User user in userQueryInSql)
            {
                    Console.WriteLine("\tRead {0}", user);
            }
    
            Console.WriteLine("Press any key to continue ...");
            Console.ReadKey();
    }
    ```

2. <span data-ttu-id="edc45-118">Copie e cole o código seguinte no método **BasicOperations**, antes da linha `await this.DeleteUserDocument("Users", "WebCustomers", "1");`.</span><span class="sxs-lookup"><span data-stu-id="edc45-118">Copy and paste the following code to your **BasicOperations** method, before the `await this.DeleteUserDocument("Users", "WebCustomers", "1");` line.</span></span>

    ```csharp
    this.ExecuteSimpleQuery("Users", "WebCustomers");
    ```

3. <span data-ttu-id="edc45-119">Guarde o ficheiro Program.cs e, no terminal integrado, execute o comando seguinte.</span><span class="sxs-lookup"><span data-stu-id="edc45-119">Save the Program.cs file and then, in the integrated terminal, run the following command.</span></span>
    
    ```
    dotnet run
    ```

    <span data-ttu-id="edc45-120">A consola apresenta o resultado seguinte.</span><span class="sxs-lookup"><span data-stu-id="edc45-120">The console displays the following output.</span></span>

    ```
    Running LINQ query...
    Running direct SQL query...
    Press any key to continue ...
    ```

    <span data-ttu-id="edc45-121">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="edc45-121">Congratulations!</span></span> <span data-ttu-id="edc45-122">Obteve com êxito o seu conjunto de utilizadores no Azure Cosmos DB ao utilizar consultas SQL e LINQ.</span><span class="sxs-lookup"><span data-stu-id="edc45-122">You have successfully your Azure Cosmos DB collection of users by using SQL and LINQ queries.</span></span>

## <a name="summary"></a><span data-ttu-id="edc45-123">Resumo</span><span class="sxs-lookup"><span data-stu-id="edc45-123">Summary</span></span>

<span data-ttu-id="edc45-124">Nessa unidade, ficou a conhecer as consultas LINQ e, em seguida, adicionou uma consulta LINQ e do SQL à aplicação para obter registos de utilizador.</span><span class="sxs-lookup"><span data-stu-id="edc45-124">In this unit you learned about LINQ queries, and then added a LINQ and SQL query to your application to retrieve user records.</span></span>