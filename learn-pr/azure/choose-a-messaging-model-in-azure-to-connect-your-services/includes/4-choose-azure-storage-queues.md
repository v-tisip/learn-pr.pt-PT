Imagine que está a planear a arquitetura da sua aplicação de partilha de música. Deve optar por uma forma que garanta que o carregamento de ficheiros de música é feito da aplicação móvel para a API Web de forma viável.

Depois de ter compreendido que esta comunicação deve ser uma mensagem, tem de escolher entre as filas de Armazenamento do Azure e o Azure Service Bus, podendo ambos podem ser utilizados para armazenar as filas de mensagens enquanto aguardam processamento.

## <a name="delivery-guarantees"></a>Garantias de entrega

Normalmente, os sistemas de colocação em fila garantem a entrega de cada mensagem na fila para um componente de destino. Contudo, estas garantias podem assumir diferentes abordagens:

- **Entrega No-Mínimo-Uma-Vez.** Nesta abordagem, é garantido que cada mensagem é entregue a, pelo menos, um dos componentes que obtém as mensagens da fila. No entanto, note que em determinadas circunstâncias é possível que a mesma mensagem seja entregue mais de uma vez. Por exemplo, se existirem duas instâncias de uma aplicação Web a obter mensagens de uma fila, normalmente cada mensagem vai para apenas uma das duas instâncias. Contudo, se uma instância demorar muito tempo a processar a mensagem e o tempo limite expirar, a mensagem pode ser enviada para a outra instância também. O código da aplicação Web deve ser concebido com essa possibilidade em mente.
- **Entrega No-Máximo-Uma-Vez.** Nesta abordagem, não é garantido que cada mensagem seja entregue e há uma pequena hipótese que nem chegue ao destino. Contudo, não há qualquer hipótese de que a mensagem seja enviada duas vezes, tal como acontece com a entrega No-Máximo-Uma-Vez.
- **Primeiro a Entrar, Primeiro a Sair (FIFO).** Na maioria dos sistema de mensagens, as mensagens deixam, normalmente, a fila pela mesma ordem em que foram adicionados, mas deve considerar se esta ordem é garantida. Se a sua aplicação distribuída necessitar que as mensagens sejam processadas exatamente pela ordem correta, tem de escolher um sistema de fila que inclua uma garantia de FIFO.

## <a name="transactions"></a>Transações

Alguns grupos de mensagens intimamente relacionados podem provocar problemas quando a entrega falha para uma mensagem no grupo.

Por exemplo, considere uma aplicação de comércio eletrónico. Quando o utilizador clica no botão "Comprar", é enviada uma mensagem com os detalhes do pedido, juntamente com uma mensagem com os detalhes do cartão de crédito. Se a mensagem do cartão de crédito não for entregue, o pedido pode ser expedida sem pagamento.

Pode evitar este tipo de problemas, agrupando as duas mensagens numa transação. O sucesso ou fracasso das transações é medido enquanto unidade única. Se a entrega da mensagem de detalhes do cartão de crédito falhar, o mesmo acontecerá à mensagem de detalhes do pedido.

## <a name="when-to-use-storage-queues"></a>Quando utilizar filas de armazenamento

As filas são utilizadas para mensagens, mas não eventos.

As Contas de Armazenamento do Azure incluem filas que podem ser utilizadas por aplicações distribuídas como localizações de armazenamento temporário simples para as mensagens. Um componente de origem pode adicionar uma mensagem à fila. Os componentes de destino obtêm a mensagem no início da fila para processamento. Estas filas aumentam a fiabilidade de troca de mensagens, porque, em momentos de procura elevada, as mensagens podem simplesmente aguardar até que um componente de destino esteja pronto para as processar.

As filas são também fornecidas como parte das Mensagens do Azure Service Bus. Se decidiu utilizar uma fila no Azure para uma comunicação específica, tem de optar por utilizar uma fila de Armazenamento ou uma fila do Service Bus.

Para tomar essa decisão, considere as seguintes perguntas:

- Necessita de uma garantia de entrega No-Máximo-Uma-Vez?
- Necessita de uma garantia de FIFO?
- Necessita de agrupar mensagens em transações?
- Necessita de armazenar mensagens com mais de 64 KB?

Se a resposta a alguma dessas perguntas for positiva, tem de optar por utilizar uma fila do Service Bus.

Deve ainda considerar as seguintes questões:

- Necessita de registos do lado do servidor de todas as mensagens que passam pela fila?
- Espera que a fila ultrapasse os 80 GB?

Se a resposta a alguma dessas perguntas for positiva, tem de optar por uma fila do Service Bus.

## <a name="summary"></a>Resumo

Uma fila é uma localização de armazenamento temporário simples para as mensagens enviadas entre os componentes de uma aplicação distribuída. Utilize uma fila para organizar as mensagens e processar facilmente aumentos inesperados da procura.

Utilize as filas de Armazenamento do Azure se procura um sistema de fila simples e fácil de codificar. Para necessidades mais avançadas, utilize filas do Service Bus do Azure.