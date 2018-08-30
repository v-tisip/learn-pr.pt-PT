<!--TODO: Explain how to do ExecuteNext (pages closer to SDK imp) vs ToList (continuation token)--> Agora que criou documentos na aplicação, vamos consultá-los. O Azure Cosmos DB utiliza consultas SQL e consultas LINQ. Abordamos as consultas SQL e como executá-las no portal no módulo **Adicionar dados e consultar dados na base de dados**. 

Portanto, esta unidade concentra-se em executar consultas SQL e consultas LINQ a partir da aplicação.

Vamos utilizar os documentos de utilizador que criou para a aplicação de retalhista online para testar estas consultas.

## <a name="linq-query-basics"></a>Noções básicas da consultas LINQ

O LINQ é um modelo de programação do .NET que expressa os cálculos como consultas em fluxos de objetos. Pode criar um objeto **IQueryable** para consultar diretamente o Azure Cosmos DB, o que converte a consulta LINQ numa consulta do Cosmos DB. A consulta é, em seguida, passada para o servidor do Azure Cosmos DB para obter um conjunto de resultados no formato JSON. Os resultados devolvidos terão a serialização anulada num fluxo de objetos do .NET no lado do cliente. Muitos programadores preferem consultas LINQ, dado que fornecem um modelo de programação consistente da forma como trabalham com objetos no código da aplicação e de como expressam a lógica de consulta em execução na base de dados.

A tabela seguinte mostra como as consultas LINQ são convertidas em SQL.

| Expressão LINQ | Conversão SQL |
|---|---|
| `input.Select(family => family.parents[0].familyName);`| `SELECT VALUE f.parents[0].familyName FROM Families f` |
|`input.Select(family => family.children[0].grade + c); // c is an int variable` | `SELECT VALUE f.children[0].grade + c FROM Families f` |
|`input.Select(family => new { name = family.children[0].familyName, grade = family.children[0].grade + 3});`| `SELECT VALUE {"name":f.children[0].familyName, "grade": f.children[0].grade + 3 } FROM Families f`|
|`input.Where(family=> family.parents[0].familyName == "Smith");`|`SELECT * FROM Families f WHERE f.parents[0].familyName = "Smith"`|

## <a name="run-sql-and-linq-queries"></a>Executar consultas SQL e LINQ

1. O exemplo a seguir mostra como uma consulta pode ser realizada no SQL, no LINQ ou no LINQ lambda a partir do código .NET. Copie o código e adicione-o após o método **DeleteUserDocument**.

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

2. Copie e cole o código seguinte no método **BasicOperations**, antes da linha `await this.DeleteUserDocument("Users", "WebCustomers", "1");`.

    ```csharp
    this.ExecuteSimpleQuery("Users", "WebCustomers");
    ```

3. Guarde o ficheiro Program.cs e, no terminal integrado, execute o comando seguinte.
    
    ```
    dotnet run
    ```

    A consola apresenta o resultado seguinte.

    ```
    Running LINQ query...
    Running direct SQL query...
    Press any key to continue ...
    ```

    Parabéns! Obteve com êxito o seu conjunto de utilizadores no Azure Cosmos DB ao utilizar consultas SQL e LINQ.

## <a name="summary"></a>Resumo

Nessa unidade, ficou a conhecer as consultas LINQ e, em seguida, adicionou uma consulta LINQ e do SQL à aplicação para obter registos de utilizador.