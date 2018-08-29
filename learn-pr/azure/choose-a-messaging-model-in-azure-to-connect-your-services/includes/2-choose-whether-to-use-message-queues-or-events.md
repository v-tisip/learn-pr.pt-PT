Suponha que está a planear a arquitetura de uma aplicação distribuída de partilha de música. Deve certificar-se de que a aplicação é tão fiável e escalável quanto possível e de que pretende utilizar tecnologias do Azure para criar uma infraestrutura de comunicação robusta.

Antes de escolher a tecnologia certa do Azure, tem de compreender todas as comunicações individuais que os componentes da aplicação trocam. Para todas as comunicações, pode escolher uma tecnologia diferente do Azure.

A primeira coisa a entender sobre uma comunicação é se envia mensagens ou eventos. Algumas tecnologias do Azure visam eventos e outras visam mensagens, pelo que esta é uma escolha fundamental.

## <a name="what-is-a-message"></a>O que é uma mensagem?

Na terminologia de aplicações distribuídas, as **mensagens** têm as seguintes características:

- Uma mensagem contém dados não processados, produzidos por um componente, que será consumida por outro componente.
- Uma mensagem contém os dados em si, não apenas uma referência a esses dados.
- O componente de envio espera que o conteúdo da mensagem seja processado de uma determinada forma pelo componente de destino. A integridade do sistema global pode depender do remetente e do receptor ao fazer uma tarefa específica.

Por exemplo, suponha que um utilizador carrega uma música nova ao utilizar a aplicação móvel de partilha de música. A aplicação móvel tem de enviar essa música para a API Web que é executada no Azure. O próprio ficheiro de suporte de dados de música tem de ser enviado, e não apenas um alerta que indica que foi adicionada uma nova música. A aplicação móvel espera que a API Web armazene a nova música na base de dados e disponibilize-a a outros utilizadores. Este é um exemplo de uma mensagem.

## <a name="what-is-an-event"></a>O que é um evento?

Os **eventos** são mais leves do que as mensagens e são geralmente utilizados para comunicações de difusão. Os componentes que enviam o evento são conhecidos como **publicadores** e os recetores são conhecidos como **subscritores**.

Com os eventos, os componentes de receção geralmente decidem em que comunicações estão interessados e "inscrevem-se" neles. A subscrição é, normalmente, gerida por um intermediário, como o Azure Event Grid ou o Hub de Eventos do Azure. Quando os publicadores enviam um evento, o intermediário irá encaminhar esse evento aos subscritores interessados. Isto é conhecido como uma "arquitetura de publicação-subscrição", não é a única forma de lidar com eventos, mas é a mais comum.

Os eventos têm as seguintes características:

- Um evento é uma notificação simples que indica que algo aconteceu.
- O evento pode ser enviado para vários recetores ou para nenhum.
- Os eventos destinam-se, muitas vezes, a "fan-out" (distribuição) ou têm um grande número de subscritores para cada publicador.
- O publicador do evento não tem qualquer expectativa sobre a ação de um componente de receção.
- Alguns eventos são unidades discretas e não relacionadas com outros eventos. 
- Alguns eventos fazem parte de uma série ordenada e relacionada.  

Por exemplo, suponha que o carregamento de ficheiros de música foi concluído e foi adicionada a música nova à base de dados. Para informar os utilizadores sobre o novo ficheiro, a API Web deve informar os utilizadores de aplicações móveis e de front-end da Web sobre o novo ficheiro. Os utilizadores podem optar se querem ouvir a música nova, pelo que a notificação inicial não inclui o ficheiro de música, mas apenas notifica os utilizadores de que a música existe. O remetente não tem uma expectativa específica de que os recetores de eventos farão nada específico em resposta à receção deste evento.

Este é um exemplo de um evento discreto.

## <a name="how-to-choose-messages-or-events"></a>Como escolher mensagens ou eventos

Uma aplicação única é mais propensa a utilizar eventos para determinados fins e mensagens para outros. Antes de escolher, tem de analisar a sua arquitetura de aplicação e todos os seus casos de utilização para identificar todos os fins diferentes que os seus componentes têm para comunicar entre si. 

Os eventos têm maior probabilidade de serem utilizados para difusões e costumam ser efémeros, o que significa que uma comunicação pode não ser processada por qualquer recetor se nenhum estiver atualmente inscrito. As mensagens têm maior probabilidade de serem utilizadas quando a aplicação distribuída exige uma garantia de que a comunicação será processada.

Para todas as comunicações, considere a pergunta: o componente de envio espera que a comunicação seja processada de uma determinada forma pelo componente de destino?

Se a resposta for sim, opte por utilizar uma mensagem. Se a resposta for não, poderá utilizar eventos.

## <a name="summary"></a>Resumo

Os componentes de uma aplicação distribuída comunicam entre si para muitas finalidades diferentes. Para cada um destes fins, tem de escolher se pretende utilizar os eventos ou mensagens de forma a que possa escolher uma tecnologia do Azure que foi concebida para esse fim. 

Depois de ter compreendido por que os componentes comunicam e por que utilizam mensagens ou eventos, pode avançar para a escolha de filas de Armazenamento do Azure, Hubs de Eventos, Event Grids ou Service Bus para trocar as informações.