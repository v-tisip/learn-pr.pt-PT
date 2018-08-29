Há determinadas aplicações que produzem um grande número de eventos a partir de um número semelhante de origens. Ouvimos, recorrentemente, o termo "Macrodados" aplicado a estas situações, que exigem uma infraestrutura exclusiva para processamento.

Imagine que trabalha para a Contoso Aircraft Engines. Os motores que o seu empregador fabrica têm centenas de sensores. Para que uma aeronave possa voar todas as manhãs, primeiro, os respetivos motores são ligados a um conjunto de teste e postos à prova. Além disso, os dados de voo em cache são transmitidos quando a aeronave está ligada aos equipamentos de terra.

Pretende utilizar o histórico dos dados do sensor para detetar padrões na leituras do sensor que indiquem a possibilidade eminente de falhas do motor. Pretende que as leituras do sensor em tempo real sejam comparadas com estes padrões de falha. Em seguida, pode avisar os utilizadores em tempo real, caso um motor apresente leituras preocupantes.

## <a name="what-is-azure-event-hubs"></a>O que são Hubs de Eventos do Azure?

Um Hub de Eventos do Azure é um intermediário para o padrão de comunicação publicar-subscrever, mas, ao contrário do Event Grid, está otimizado para um débito extremamente alto, um elevado número de publicadores, segurança e resiliência.

Ao passo que o Event Grid se adapta de forma mais ou menos perfeita ao padrão publicar-subscrever, em que simplesmente gere subscrições e encaminha comunicações para os subscritores, o Hub de Eventos executa alguns serviços adicionais que, em certa medida, fazem com que se assemelhe mais a um serviço de barramento ou a uma fila de mensagens do que um simples emissor de eventos.

#### <a name="partitions"></a>Partições ####
À medida que o Hub de Eventos recebe comunicações, vai dividi-las em partições. As partições são memórias intermédias nas quais são guardadas as comunicações. Por causa das memórias intermédias, os eventos não são completamente efémeros e um evento não é perdido, só porque um subscritor está ocupado ou offline. O subscritor pode sempre utilizar a memória intermédia para "recuperar o atraso". Por predefinição, os eventos permanecem na memória intermédia durante 24 horas e, em seguida, expirarem automaticamente.

As memórias intermédias são chamadas de partições, porque os dados estão divididos entre elas. Cada Hub de Eventos tem, pelo menos, duas partições e cada partição tem um conjunto de subscritores separado.

#### <a name="capture"></a>Captura ####
O Hub de Eventos pode enviar todos os seus eventos imediatamente para o Azure Data Lake ou Armazenamento de Blobs para uma persistência permanente de baixo custo.

#### <a name="authentication"></a>Autenticação ####
Todos os editores são autenticados e é-lhes emitido um token. Tal significa que o Hub de Eventos pode aceitar eventos a partir de dispositivos externos e aplicações móveis sem se preocupar com a possibilidade de dados fraudulentos poderem arruinar a nossa análise. 

## <a name="using-azure-event-hub"></a>Utilizar o Hub de Eventos do Azure

Os Hubs de Eventos têm suporte para pipelining da transmissão de eventos para outros serviços do Azure. Utilizá-lo com o Stream Analytics, por exemplo, permite uma análise complexa dos dados em tempo real com capacidade para correlacionar vários eventos e procurar padrões. Neste caso, o Stream Analytics seria considerado um subscritor.

Para os nossos motores das aeronaves, iremos definir a nossa arquitetura para que os Hubs de Eventos autentiquem as comunicações dos nossos motores. Em seguida, vamos utilizar a Captura para guardar todos os dados para o Azure Data Lake e, mais tarde, podemos usar todos esses dados para reparametrizar e melhorar os nossos modelos de aprendizagem automática. Por fim, as nossas transmissões de eventos serão detetados por subscritores do Azure Stream Analytics. O Stream Analytics vai utilizar o nosso modelo de aprendizagem automática para procurar padrões nos dados do sensor que possam indicar problemas.

Uma vez que temos várias partições, e que cada motor envia todos os seus dados para apenas uma partição, cada instância do nosso subscritor do Stream Analytics só precisa lidar com um subconjunto dos nossos dados gerais, em vez de filtrar e a correlacionar todos eles.

## <a name="choose-event-grid-or-event-hub"></a>Optar pelo Event Grid ou Hub de Eventos

Ambos suportam a semântica *Pelo Menos Uma Vez*.

Se precisar de uma infraestrutura de publicação-subscrição de eventos simples com publicadores fidedignos (por exemplo, o seu próprio servidor Web), deve escolher o Azure Event Grid.

### <a name="consider-event-hub-if"></a>Considere o Hub de Eventos se:
* precisar de autenticar um grande número de publicadores;
* precisar de guardar uma transmissão de eventos para o Azure Data Lake ou Armazenamento de Blobs;
* precisar de agregação ou análise na sua transmissão de eventos
* precisar de mensagens fiáveis ou resiliência. 