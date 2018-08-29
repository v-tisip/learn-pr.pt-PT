Imagine um cenário em que um cabeleireiro movimentado tem um problema recorrente: os clientes falham frequentemente as marcações. As marcações são blocos de tempo reservados. Se um cliente falha uma marcação, o cabeleireiro perde dinheiro. Para corrigir este problema, o cabeleireiro recorre a si, um programador de software. Para melhorar o problema, opta por enviar mensagens de texto de lembrete. Todas as manhãs, envia uma mensagem de texto a cada cliente com uma marcação nesse dia.

Como programador do Azure, decide resolver este problema através de uma função do Azure. Já sabe como implementar a lógica para enviar uma mensagem de texto. Agora, tem de saber como enviar a mensagem numa hora específica. Felizmente, as Funções do Azure suportam uma funcionalidade denominada _acionadores_. Os acionadores são utilizados para determinar a forma como é executada uma função do Azure.

## <a name="learning-objectives"></a>Objetivos de aprendizagem
> [!div class="checklist"]
> * Determinar o acionador mais adequado para as suas necessidades empresariais.
> * Criar um acionador de temporizador para invocar uma função com base numa agenda consistente.
> * Criar um acionador HTTP para invocar uma função quando é recebido um pedido HTTP.
> * Criar um acionador de blobs para invocar uma função quando é criado ou atualizado um blob no Armazenamento do Azure.
