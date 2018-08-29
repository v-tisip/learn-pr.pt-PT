Em seguida iremos analisar os dados em toda a nossa base de dados. Isto é importante para se certificar de que podemos trabalhar com um volume de transações para as nossas necessidades de negócio. Os requisitos de débito nem sempre são consistentes. Por exemplo, pode criar um site de compras que precisa de ser dimensionado durante as vendas ou os feriados. Vamos começar a estimar os requisitos de débito da base de dados.

## <a name="what-is-database-throughput"></a>O que é o débito da base de dados? 

O débito da base de dados é o número de leituras e gravações que a sua base de dados pode realizar num segundo. 

Para dimensionar o débito estrategicamente, precisa de estimar as necessidades do débito ao estimar o número de leituras e gravações que terá de suportar em alturas diferentes e para tamanhos de documento diferentes. Se calcular corretamente, irá manter os seus utilizadores satisfeitos nos picos de procura. Se estimar incorretamente, os seus pedidos podem ficar com a taxa limitada e as operações terão de aguardar e tentar novamente, provavelmente causando uma alta latência e clientes insatisfeitos.

## <a name="what-is-a-request-unit"></a>O que é uma unidade de pedido?

O Azure Cosmos DB mede o débito através de algo chamado de **unidade de pedido (RU)**. A utilização da unidade de pedido é medida por segundo, pelo que a unidade de medida é **unidades de pedido por segundo (RU/s)**. Tem de reservar o número de RU/s que pretende que o Azure Cosmos DB aprovisione antecipadamente, para que possa manipular a carga que estimou e aumentar ou reduzir verticalmente a sua RU/s em qualquer altura, para satisfazer o pedido atual.

## <a name="request-unit-basics"></a>Noções básicas da unidade de pedido

Uma unidade de pedido único, 1 RU, é igual ao custo aproximado da execução de um pedido GET único num documento de 1 KB com o ID de documento. Executar um GET com o ID de documento é um meio eficiente para recuperar um documento e, portanto, o custo é pequeno. Criar, substituir ou eliminar o mesmo item exige processamento adicional pelo serviço e, portanto, exige mais unidades de pedido.

O número de unidades de pedido utilizadas para uma operação é diferente consoante o tamanho do documento, o número de propriedades do documento, a operação a realizar e alguns conceitos complexos adicionais, como a consistência e a política de indexação.

A tabela seguinte mostra o número de unidades de pedido que são precisas para itens de três tamanhos diferentes (1 KB, 4 KB e 64 KB) e em dois níveis de desempenho diferentes (500 leituras/segundo + 100 gravações/segundo e 500 leituras/segundo + 500 gravações/segundo). Neste exemplo, a consistência de dados está definida como **Sessão** e a política de indexação está definida como **Nenhuma**.

| Tamanho do item | Leituras/segundo | Gravações/segundo | Unidades de pedidos
| --- | --- | --- | --- |
| 1 KB | 500 | 100 | (500 * 1) + (100 * 5) = 1.000 RU/s
| 1 KB | 500 | 500 | (500 * 1) + (500 * 5) = 3.000 RU/s
| 4 KB | 500 | 100 | (500 * 1,3) + (100 * 7) = 1.350 RU/s
| 4 KB | 500 | 500 | (500 * 1,3) + (500 * 7) = 4.150 RU/s
| 64 KB | 500 | 100 | (500 * 10) + (100 * 48) = 9.800 RU/s
| 64 KB | 500 | 500 | (500 * 10) + (500 * 48) = 29.000 RU/s
 
Como pode ver, quanto maior for o item, mais leituras e gravações são precisas, mais unidades de pedido tem de reservar. Se tiver de calcular as necessidades de débito de uma aplicação, o [Planeador de Capacidade](https://www.documentdb.com/capacityplanner) do Azure Cosmos DB é uma ferramenta online que lhe permite carregar um documento JSON de exemplo e definir o número de operações que tem de concluir por segundo. Em seguida, apresenta um total estimado para reservar.

## <a name="exceeding-throughput-limits"></a>A exceder os limites de débito

Se não reservar unidades de pedido suficientes e estiver a tentar ler ou gravar mais dados do que o débito aprovisionado permite, o seu pedido terá a taxa limitada. Quando um pedido tem a taxa limitada, este tem de ser repetido novamente após um intervalo especificado. Se utilizar o SDK .NET, o pedido será repetido automaticamente após aguardar a quantidade de tempo especificada no cabeçalho repetir-após.

## <a name="creating-an-account-built-to-scale"></a>Criar uma conta criada para dimensionamento

Pode alterar o número de unidades de pedido aprovisionadas numa base de dados em qualquer altura. Por isso, durante períodos de volume pesados, pode aumentar verticalmente para acomodar essa procura elevada e, em seguida, reduzir o débito aprovisionado durante os horários fora de pico para reduzir os custos.

Quando cria uma conta, pode aprovisionar um mínimo de 400 RU/s ou um máximo de 250.000 RU/s no portal. Se precisar de mais débito, preencha um pedido no portal do Azure. É recomendado definir o débito inicial para 1000 RU/s para quase todas as contas, uma vez que é o valor mínimo no qual a sua base de dados será dimensionada automaticamente se precisar de mais de 10 GB de armazenamento. Se definir a taxa de débito inicial para qualquer valor inferior a 1000 RU/s, a base de dados não conseguirá dimensionar para mais de 10 GB, a menos que reaprovisione a base de dados e indique uma chave de partição. As chaves de partição ativam uma pesquisa rápida de dados no Azure Cosmos DB para dimensionar automaticamente a base de dados quando é preciso. As chaves de partição são abordadas na unidade seguinte.

## <a name="summary"></a>Resumo

Agora, já sabe como estimar e avaliar o débito para uma Azure Cosmos DB com unidades de pedido. As unidades de pedido podem ser modificadas em qualquer altura e defini-las para 1000 RU/s ao criar uma conta ajuda a garantir que a sua base de dados está pronta para ser dimensionada mais tarde.