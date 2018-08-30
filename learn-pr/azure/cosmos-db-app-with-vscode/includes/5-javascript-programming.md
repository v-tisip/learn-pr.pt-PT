Com frequência, vários documentos na base de dados têm de ser atualizados ao mesmo tempo. Esta unidade aborda como criar, registar e executar procedimentos armazenados a partir da aplicação de consola .NET.

## <a name="create-a-stored-procedure-in-your-app"></a>Criar um procedimento armazenado na aplicação

Neste procedimento armazenado, o OrderId, que contém uma lista de todos os artigos na encomenda, é utilizado para calcular o total da encomenda. O total é calculado pela soma dos artigos na encomenda, menos qualquer dividendo (crédito) que o cliente tenha e toma em consideração qualquer código de cupão.

1. Copie o seguinte código e cole-o no fim do ficheiro Program.cs.

    <!--TODO: Update sproc to take order total and check for available dividend, and use of summer coupon code, and provide updated total-->
    ```csharp
    private async Task UpdateOrderTotal(string databaseName, string collectionName, Order orderId)
    {
    var markAntiquesSproc = new StoredProcedure
    {
        Id = "ValidateDocumentAge",
        Body = @"
                function(docToCreate, antiqueYear) {
                    var collection = getContext().getCollection();    
                    var response = getContext().getResponse();    
    
                    if(docToCreate.Year != undefined && docToCreate.Year < antiqueYear){
                        docToCreate.antique = true;
                    }
    
                    collection.createDocument(collection.getSelfLink(), docToCreate, {}, 
                        function(err, docCreated, options) { 
                            if(err) throw new Error('Error while creating document: ' + err.message);                              
                            if(options.maxCollectionSizeInMb == 0) throw 'max collection size not found'; 
                            response.setBody(docCreated);
                    });
             }"
    };
    // register stored procedure
    StoredProcedure createdStoredProcedure = await client.CreateStoredProcedureAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), markAntiquesSproc);
    dynamic document = new Document() { Id = "Borges_112" };
    document.Title = "Aleph";
    document.Year = 1949;
    
    // execute stored procedure
    Document createdDocument = await client.ExecuteStoredProcedureAsync<Document>(UriFactory.CreateStoredProcedureUri("db", "coll", "ValidateDocumentAge"), document, 1920);
    }
    ```

2. Agora, copie o seguinte código e cole-o no fim do método **BasicOperations**.

    ```
    await this.UpdateOrderTotal("Users", "WebCustomers", "5-6235");
    ```

3. Guarde o ficheiro Program.cs e, no terminal integrado, execute o comando seguinte.

    ```
    dotnet run
    ```

    A consola apresenta o resultado seguinte.

    ```
    Order total is 90.85.
    Press any key to continue ...
    ```

## <a name="clean-up"></a>Limpeza

Se planear continuar a trabalhar nos módulos neste percurso de aprendizagem, ignore o processo de limpeza; caso contrário, utilize os seguintes passos para eliminar os recursos para evitar incorrer em custos de utilização do serviço.

1. No portal do Azure, selecione **Grupos de recursos** à esquerda e, em seguida, selecione o grupo de recursos que criou.  

    Se o menu à esquerda estiver fechado, clique no ![botão Expandir](../media/5-javascript-programming/expand.png) para expandi-lo.

   ![Métricas no portal do Azure](../media/5-javascript-programming/delete-resources-select.png)

2. Na nova janela, selecione o grupo de recursos e, em seguida, clique em **Eliminar grupo de recursos**.

   ![Métricas no portal do Azure](../media/5-javascript-programming/delete-resources.png)

3. Na nova janela, escreva o nome do grupo de recursos a eliminar e, em seguida, clique em **Eliminar**.

## <a name="summary"></a>Resumo

Neste módulo, criou uma aplicação de consola .NET Core que cria, atualiza e elimina os registos dos utilizadores, consulta os utilizadores com o SQL e o LINQ e executa um procedimento armazenado para criar o total das encomendas que considera os dividendos e os cupões dos utilizadores.