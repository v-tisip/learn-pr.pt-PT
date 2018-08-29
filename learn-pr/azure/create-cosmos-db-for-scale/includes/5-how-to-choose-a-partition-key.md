O revendedor online para quem trabalha, tem planos para expandir o negócio para uma nova área geográfica, num futuro próximo. Esta jogada vai aumentar a sua base de clientes e o seu volume de transações. Tem de garantir que a sua base de dados está equipada para suportar esta expansão, quando ela acontecer.

Ter uma estratégia de partição garante que no momento em que a sua base de dados precisar de crescer, poderá fazê-lo de forma fácil, continuando a executar consultas e transações de forma eficiente.

## <a name="what-is-a-partition-strategy"></a>O que é uma estratégia de partição?

Se continuar a adicionar novos dados a um único servidor ou uma única partição, vai, invariavelmente, deixar de ter espaço. Para estar preparado, terá de adotar uma estratégia de partição para **aumentar horizontalmente** em vez de verticalmente. O dimensionamento horizontal permite-lhe adicionar mais partições à sua base de dados, à medida que a sua aplicação precisa delas.

A estratégia de partição e dimensionamento horizontal no Azure Cosmos DB é orientada pela chave de partição, que é um valor definido quando cria uma coleção. Uma vez definida a chave de partição, esta não pode ser alterada sem recriar a coleção, por isso, a seleção da chave de partição correta é uma decisão importante a tomar no início do seu processo de desenvolvimento.  

Nesta unidade, vaia prender a escolher a chave de partição que melhor se adapta ao seu cenário e vai tirar partido do dimensionamento automático do Azure Cosmos DB.

## <a name="partition-key-basics"></a>Noções básicas da chave de partição

Uma chave de partição representa um valor na sua base de dados que é consultado com frequência. Assim, no caso de um retalhista online, usar o valor UserID ou ProductID como a chave de partição é uma boa opção. UserID é uma boa opção, porque a sua aplicação está constantemente a recolher informações sobre definições de personalização, carrinho de compras, histórico de pedidos e informações de perfil, entre muitas outras, para o utilizador. ProductID também é uma boa opção, porque a sua aplicação tem de consultar níveis de inventário, custos de envio, opções de cor, localizações de armazém e muito mais.

Uma chave de partição deve ter como objetivo distribuir operações por toda a base de dados. Deve distribuir os pedidos para evitar ter partições demasiado ativas. Uma partição demasiado ativa significa que há uma partição que recebe muitos mais pedidos que as restantes partições, o que pode provocar um estrangulamento de débito. Por exemplo, para a sua aplicação de comércio eletrónico, a hora atual seria uma má escolha para chave de partição, uma vez que todos os dados de entrada iriam para uma única chave de partição. UserID ou ProductID seriam uma melhor escolha, uma vez que é provável que todos os utilizadores do seu site adicionem e atualizem o respetivo carrinho de compras ou informações de perfil com a mesma frequência, o que distribui as leituras e escritas por todas as partições de utilizador. Da mesma forma, seria provável que as atualizações para os dados do produto fossem também distribuídas de forma bastante uniforme, fazendo do ProductID uma boa escolha para chave de partição.

Cada chave de partição tem uma capacidade de armazenamento máxima de 10 GB, que corresponde ao tamanho de uma partição física do Azure Cosmos DB. Se o seu único registo de UserID ou ProductID for superior a 10 GB, pondere a utilização de uma chave composta, para que cada registo seja menor. Um exemplo de chave composta seria UserID-date, o que seria qualquer coisa como NomeCliente 08072018. Esta abordagem de chave composta iria permitir-lhe criar uma nova partição, para cada dia que um utilizador visitasse o site.

## <a name="best-practices"></a>Melhores práticas

Se está a tentar determinar qual a melhor chave de partição para si e a solução não é óbvia, aqui ficam algumas dicas a ter em conta.

* Não tenha medo de ter demasiadas chaves de partição. Quantas mais chaves de partição tiver, mais dimensionamento tem.

* Para determinar a melhor chave de partição para uma carga de trabalho de leitura intensiva, analise as primeiras três a cinco consultas que tenciona utilizar. O valor mais frequentemente incluído na cláusula ONDE é um bom candidato para a chave de partição.

* Para cargas de trabalho de escrita intensiva, terá de compreender as necessidades de transação da sua carga de trabalho, porque a chave de partição é o âmbito das transações de vários documentos.
