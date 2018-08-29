Muitas aplicações utilizam eventos para notificar os componentes distribuídos sobre algum acontecimento ou objeto alterado. Pode utilizar o Event Grid para facilitar a distribuição desses eventos pelo Azure.

Suponha que tem uma aplicação de partilha de música com uma API Web executada no Azure. Quando um novo ficheiro de som é carregado por um utilizador, tem de notificar todas as aplicações móveis instaladas nos dispositivos dos utilizadores em todo o mundo.

Pode utilizar subscrições do Azure Event Grid para alcançar esta fiabilidade rapidamente.

## <a name="what-is-event-grid"></a>O que é o Event Grid?

O Azure Event Grid é um serviço que distribui eventos a partir de origens, como contas de Armazenamento de Blobs do Azure ou Serviços de Multimédia, para os subscritores, como as Funções do Azure ou para Web Hooks.

Uma origem de evento é qualquer componente que pode gerar um evento. Por exemplo, um utilizador pode adicionar um novo ficheiro de multimédia para uma conta de Armazenamento de Blobs. Isto gera um evento que o Event Grid pode distribuir.

Um subscritor de eventos é qualquer componente que pode receber eventos do Event Grid. Por exemplo, uma Função do Azure pode executar o código que responde no novo ficheiro de multimédia na conta de Armazenamento de Blobs.

O Event grid facilita a ligação de origens para vários subscritores.

![Origens e subscritores do Event grid](../images/6-event-grid.png)

## <a name="event-sources"></a>Origens de Eventos

Os eventos podem ser gerados pelos seguintes tipos de recursos do Azure:

- **Subscrições e Grupos de Recursos do Azure.** As subscrições e grupos de recursos geram eventos relacionados com operações de gestão no Azure. Por exemplo, quando um utilizador cria uma Máquina Virtual (VM), esta origem gera um evento.
- **Contas de Armazenamento.** As contas de armazenamento podem gerar eventos quando os utilizadores adicionam blobs, ficheiros, entradas da tabela ou mensagens de fila. Pode utilizar contas do blob e contas de fins gerais como origens de eventos.
- **Serviços de Multimédia.** Os Serviços de Multimédia alojam suporte de dados de vídeo e áudio e oferecem funcionalidades de gestão avançada para ficheiros de multimédia. Os Serviços de Multimédia podem gerar eventos quando uma tarefa de codificação é iniciada ou concluída num ficheiro de vídeo.
- **Hub IoT.** O hub da Internet das coisas (IoT) do Azure comunica com, e recolhe, telemetria de dispositivos IoT. Pode gerar eventos sempre que receber essas comunicações.
- **Eventos Personalizados.** Os eventos personalizados podem ser gerados através da API REST ou com o SDK do Azure em Java, GO, .NET, Node, Python e Ruby. Por exemplo, pode criar um evento personalizado numa função de trabalho de Aplicação Web do Azure quando esta seleciona uma mensagem de uma fila de armazenamento.

Esta integração ampla com origens de diversos eventos no Azure garante que o Event Grid pode distribuir eventos relacionados com quase qualquer recurso do Azure.

## <a name="topics"></a>Tópicos

No Azure Event Grid, um tópico é uma coleção de eventos relacionados. Quando publica eventos de uma origem, decide se esses eventos precisam apenas de um único tópico ou são divididos em vários tópicos. Os componentes que recebem e lidam com os eventos subscrevem tópicos para determinar os eventos que irão receber.

## <a name="subscriptions"></a>Subscrições

Os processadores de eventos utilizam subscrições para comunicar ao Event Grid os eventos que pretendem receber num tópico. A subscrição também corrige o ponto final – esta é a localização para onde o Event Grid envia notificações de eventos. Uma subscrição também pode filtrar eventos por tipo ou por assunto, para garantir que um processador de eventos recebe apenas eventos relevantes.

## <a name="event-handlers"></a>Processadores de Eventos

Os seguintes tipos de objeto no Azure podem receber e lidar com eventos do Event Grid:

- **Funções do Azure.** Uma Função do Azure consiste em código personalizado que é executado no Azure sem servidor virtual do anfitrião ou contentor. Utilize uma Função do Azure como um processador de eventos quando pretende criar um código para uma resposta personalizada para o evento.
- **WebHooks.** Um WebHook é a API Web que implementa uma arquitetura push.
- **Logic Apps.** Uma Aplicação Lógica do Azure aloja um processo comercial como um fluxo de trabalho.
- **Microsoft Flow.** O Flow também aloja fluxos de trabalho, mas é mais fácil de a equipa não técnica utilizar.

## <a name="how-to-choose"></a>Como escolher

Utilize o Event Grid quando precisar destas funcionalidades:

- **Simplicidade.** É muito simples ligar origens aos subscritores no Event Grid.
- **Filtros avançados.** As subscrições têm um controlo apertado sobre os eventos que recebem de um tópico.
- **Número de pontos finais.** Pode subscrever um número ilimitado de pontos finais para os mesmos eventos e tópicos.
- **Fiabilidade** O Event Grid repete a entrega de eventos até 24 horas para cada subscrição.
- **Pagamento por evento** Pague apenas o número de eventos que transmite.

## <a name="summary"></a>Resumo

O Event Grid é um sistema de distribuição de eventos simples, mas versátil. Utilize-o para publicar eventos para subscritores, que irão receber esses eventos de forma fiável e rápida.