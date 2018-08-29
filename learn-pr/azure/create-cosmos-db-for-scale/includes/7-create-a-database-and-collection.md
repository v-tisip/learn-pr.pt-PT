Agora que já sabe como as unidades de pedido são utilizadas para determinar o débito da base de dados e como a chave de partição cria a estratégia de dimensionamento para a sua base de dados, está pronto para criar a sua base de dados e coleção.

## <a name="creating-your-database-and-collection"></a>Criar uma base de dados e coleção

1. No portal do Azure, clique em **Explorador de Dados** > **Nova Coleção**.
    
    A área **Adicionar Coleção** é apresentada na extremidade direita. Poderá ter de se deslocar para a direita para a conseguir ver.

    ![O painel Data Explorer no portal do Azure, Adicionar Coleção](../media/5-create-a-database-and-collection/azure-cosmosdb-data-explorer.png)

2. Na página **Adicionar coleção**, introduza as definições para a nova coleção.

    Definição|Valor sugerido|Descrição
    ---|---|---
    Id da base de dados|Utilizadores|Denomine a nova base de dados como *Utilizadores*. Os nomes das bases de dados devem conter de 1 a 255 carateres e não podem conter /, \\, #, ?, ou um espaço à direita.
    ID da coleção|WebCustomers|Denomine a nova coleção como *WebCustomers*. Os IDs das coleções têm os mesmos requisitos em termos de carateres do que os nomes das bases de dados.
    Capacidade de armazenamento| Ilimitado |Utilize o valor predefinido de **Ilimitado**. Este valor corresponde à capacidade de armazenamento da base de dados e permite que esta aumente conforme necessário.
    Chave de partição|/UserId|UserID é uma chave de partição adequada a um contexto de retalho online, dado que muitas consultas se baseiam no ID de cliente.
    Débito|1000 RU|Altere o débito para 1000 unidades de pedido por segundo (RU/s). 1000 é o valor de RU/s mínimo que pode definir para ativar o dimensionamento automático.
    
    Por enquanto, não marque a opção Aprovisionar débito da base de dados e não adicione nenhuma chave única à coleção. 
    
3. Clique em **OK**.

    O Data Explorer mostra a base de dados e a coleção novas.

    ![O Data Explorer do portal do Azure a mostrar a base de dados e a coleção novas](../media/5-create-a-database-and-collection/azure-cosmos-db-new-collection.png)

## <a name="summary"></a>Resumo

Nesta unidade, recorreu aos seus conhecimentos sobre as chaves de partição e unidades de pedido para criar uma base de dados e uma coleção com definições de débito e dimensionamento adequadas às suas necessidades empresariais.