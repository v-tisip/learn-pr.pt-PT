A sua empresa escolheu o Azure Cosmos DB para satisfazer as exigências dos seus clientes e da base de produtos em expansão. A sua tarefa é criar a base de dados.

O primeiro passo é criar uma conta do Azure Cosmos DB. 

## <a name="what-is-an-azure-cosmos-db-account"></a>O que é uma conta do Azure Cosmos DB?

A conta do Azure Cosmos DB é um recurso do Azure que atua como uma entidade organizacional para as suas bases de dados. Liga a sua utilização à subscrição do Azure para efeitos de faturação.

Cada conta do Azure Cosmos DB está associada a um dos vários modelos de dados suportados pelo Azure Cosmos DB e pode criar o número de contas que precisar. 

A API SQL é o modelo de dados preferencial se estiver a criar uma nova aplicação. Se estiver a trabalhar com gráficos ou tabelas, ou a migrar os dados do MongoDB ou do Cassandra para o Azure, crie contas adicionais e selecione os modelos de dados relevantes.

Quando criar uma conta, escolha um ID significativo para si; é desta forma que identifica a sua conta. Além disso, crie a conta na região do Azure mais próxima dos seus utilizadores para minimizar a latência entre o datacenter e os seus utilizadores.

Opcionalmente, pode configurar redes virtuais e a redundância geográfica durante a criação da conta, mas este procedimento também pode ser efetuado mais tarde. Neste módulo, não vamos ativar essas definições.

## <a name="creating-an-azure-cosmos-db-account-in-the-portal"></a>Criar uma conta do Azure Cosmos DB no portal

<!--TODO: Update portal link with one that routes to free Learning acct-->
1. Inicie sessão no [portal do Azure](https://portal.azure.com/).
2. Clique em **Criar um recurso** > **Bases de dados** > **Azure Cosmos DB**.
   
   ![O painel da base de dados do portal do Azure](../media/1-introduction/create-nosql-db-databases-json-tutorial-1.png)

3. Na página **Nova conta**, introduza as definições para a nova conta do Azure Cosmos DB.
 
    Definição|Valor|Descrição
    ---|---|---
    ID|*Introduzir um nome exclusivo*|Introduza um nome exclusivo para identificar esta conta do Azure Cosmos DB. Uma vez que *documents.azure.com* é anexado ao ID que indicar para criar o seu URI, utilize um ID exclusivo, mas identificável.<br><br>O ID pode conter apenas minúsculas, números, o caráter hífen (-) e tem de ter entre 3 e 50 carateres.
    API|SQL|A API determina o tipo de conta a criar. O Azure Cosmos DB fornece cinco APIs que se adequam às necessidades da sua aplicação: SQL (base de dados de documentos), Gremlin (base de dados de gráficos), MongoDB (base de dados de documentos), Tabela do Azure e Cassandra, em que cada um necessita atualmente de uma conta separada. <br><br>Selecione **SQL** porque neste está a criar uma base de dados de documentos consultável com a sintaxe SQL e acessível com a API SQL.|
    Subscrição|*A sua subscrição*|Selecione a subscrição do Azure que pretende utilizar para esta conta do Azure Cosmos DB. 
    Grupo de Recursos|Criar novo<br><br>*Em seguida, introduza o mesmo nome exclusivo, conforme indicado no ID acima*|Selecione **Criar Novo** e, em seguida, introduza um novo nome de grupo de recursos para a sua conta. Para simplicidade, pode utilizar o mesmo nome do ID. 
    Localização|*Selecione a região mais próxima dos seus utilizadores*|Selecione a localização geográfica na qual vai alojar a sua conta do Azure Cosmos DB. Utilize a localização mais próxima dos seus utilizadores para lhes dar o acesso mais rápido aos dados.
    Ativar redundância geográfica| Deixar em branco | Esta definição cria uma versão replicada da base de dados numa segunda região (emparelhada). Deixe em branco por agora, uma vez que a base de dados pode ser replicada mais tarde. 
    Redes virtuais|Desativado|Deixe as redes virtuais desativadas por agora. Podem ser ativadas posteriormente. 

4. Clique em **Criar**.

    ![A página da nova conta do Azure Cosmos DB](../media/1-introduction/azure-cosmos-db-create-new-account.png)

5. A criação da conta demora alguns minutos. Aguarde que o portal apresente a notificação de que a implementação foi concluída com êxito e clique na notificação. 

    ![Alerta de notificação](../media/1-introduction/azure-cosmos-db-notification.png)

6. Na janela de notificação, clique em **Ir para recurso**.

    ![Ir para recurso](../media/1-introduction/azure-cosmos-db-go-to-resource.png)

    O portal apresenta a página **Parabéns! A sua conta do Azure Cosmos DB foi criada**.

    ![O painel de Notificações de portal do Azure](../media/1-introduction/azure-cosmos-db-account-created.png)

## <a name="summary"></a>Resumo

Criou uma conta do Azure Cosmos DB, que é o primeiro passo para criar uma base de dados do Azure Cosmos DB. Selecionou as definições apropriadas para os tipos de dados e definiu a localização da conta para minimizar a latência para os seus utilizadores.
