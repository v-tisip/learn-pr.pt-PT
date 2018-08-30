<span data-ttu-id="7861c-101">Com frequência, vários documentos na base de dados têm de ser atualizados ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="7861c-101">Multiple documents in your database frequently need to be updated at the same time.</span></span> <span data-ttu-id="7861c-102">Esta unidade aborda como criar, registar e executar procedimentos armazenados a partir da aplicação de consola .NET.</span><span class="sxs-lookup"><span data-stu-id="7861c-102">This unit discusses how to create, register, and run stored procedures from your .NET console application.</span></span>

## <a name="create-a-stored-procedure-in-your-app"></a><span data-ttu-id="7861c-103">Criar um procedimento armazenado na aplicação</span><span class="sxs-lookup"><span data-stu-id="7861c-103">Create a stored procedure in your app</span></span>

<span data-ttu-id="7861c-104">Neste procedimento armazenado, o OrderId, que contém uma lista de todos os artigos na encomenda, é utilizado para calcular o total da encomenda.</span><span class="sxs-lookup"><span data-stu-id="7861c-104">In this stored procedure, the OrderId, which contains a list of all the items in the order, is used to calculate an order total.</span></span> <span data-ttu-id="7861c-105">O total é calculado pela soma dos artigos na encomenda, menos qualquer dividendo (crédito) que o cliente tenha e toma em consideração qualquer código de cupão.</span><span class="sxs-lookup"><span data-stu-id="7861c-105">The order total is calculated from the sum of the items in the order, less any dividend (credit) the customer has, and takes any coupon codes into account.</span></span>

1. <span data-ttu-id="7861c-106">Copie o seguinte código e cole-o no fim do ficheiro Program.cs.</span><span class="sxs-lookup"><span data-stu-id="7861c-106">Copy the following code and paste it into the end of the Program.cs file.</span></span>

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

2. <span data-ttu-id="7861c-107">Agora, copie o seguinte código e cole-o no fim do método **BasicOperations**.</span><span class="sxs-lookup"><span data-stu-id="7861c-107">Now copy the following code and paste it into the end of the **BasicOperations** method.</span></span>

    ```
    await this.UpdateOrderTotal("Users", "WebCustomers", "5-6235");
    ```

3. <span data-ttu-id="7861c-108">Guarde o ficheiro Program.cs e, no terminal integrado, execute o comando seguinte.</span><span class="sxs-lookup"><span data-stu-id="7861c-108">Save the Program.cs file and then, in the integrated terminal, run the following command.</span></span>

    ```
    dotnet run
    ```

    <span data-ttu-id="7861c-109">A consola apresenta o resultado seguinte.</span><span class="sxs-lookup"><span data-stu-id="7861c-109">The console displays the following output.</span></span>

    ```
    Order total is 90.85.
    Press any key to continue ...
    ```

## <a name="clean-up"></a><span data-ttu-id="7861c-110">Limpeza</span><span class="sxs-lookup"><span data-stu-id="7861c-110">Clean up</span></span>

<span data-ttu-id="7861c-111">Se planear continuar a trabalhar nos módulos neste percurso de aprendizagem, ignore o processo de limpeza; caso contrário, utilize os seguintes passos para eliminar os recursos para evitar incorrer em custos de utilização do serviço.</span><span class="sxs-lookup"><span data-stu-id="7861c-111">If you plan to continue working on the modules in this learning path, skip the clean-up process, or else use the following steps to delete your resources to avoid incurring charges for use of the service.</span></span>

1. <span data-ttu-id="7861c-112">No portal do Azure, selecione **Grupos de recursos** à esquerda e, em seguida, selecione o grupo de recursos que criou.</span><span class="sxs-lookup"><span data-stu-id="7861c-112">In the Azure portal, select **Resource groups** on the far left, and then select the resource group you created.</span></span>  

    <span data-ttu-id="7861c-113">Se o menu à esquerda estiver fechado, clique no</span><span class="sxs-lookup"><span data-stu-id="7861c-113">If the left menu is collapsed, click</span></span> ![botão Expandir](../media/5-javascript-programming/expand.png) <span data-ttu-id="7861c-115">para expandi-lo.</span><span class="sxs-lookup"><span data-stu-id="7861c-115">to expand it.</span></span>

   ![Métricas no portal do Azure](../media/5-javascript-programming/delete-resources-select.png)

2. <span data-ttu-id="7861c-117">Na nova janela, selecione o grupo de recursos e, em seguida, clique em **Eliminar grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="7861c-117">In the new window select the resource group, and then click **Delete resource group**.</span></span>

   ![Métricas no portal do Azure](../media/5-javascript-programming/delete-resources.png)

3. <span data-ttu-id="7861c-119">Na nova janela, escreva o nome do grupo de recursos a eliminar e, em seguida, clique em **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="7861c-119">In the new window, type the name of the resource group to delete, and then click **Delete**.</span></span>

## <a name="summary"></a><span data-ttu-id="7861c-120">Resumo</span><span class="sxs-lookup"><span data-stu-id="7861c-120">Summary</span></span>

<span data-ttu-id="7861c-121">Neste módulo, criou uma aplicação de consola .NET Core que cria, atualiza e elimina os registos dos utilizadores, consulta os utilizadores com o SQL e o LINQ e executa um procedimento armazenado para criar o total das encomendas que considera os dividendos e os cupões dos utilizadores.</span><span class="sxs-lookup"><span data-stu-id="7861c-121">In this module you've created a .NET Core console application that creates, updates, and deletes user records, queries the users by using SQL and LINQ, and runs a stored procedure to create an order total that takes the users dividends and coupons into account.</span></span>