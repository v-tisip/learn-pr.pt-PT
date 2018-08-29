Agora que já conhece os serviços de computação disponíveis do Azure, vamos analisar um a um para o ajudar a decidir quando deve utilizar cada serviço.

## <a name="azure-virtual-machines"></a>Máquinas virtuais do Azure

Quando for preciso o controlo total do sistema operativo e do ambiente, as máquinas virtuais são a melhor opção. Pode personalizar todo o software em execução na VM, como um computador físico. Isto é ideal ao executar software personalizado ou configurações de alojamento personalizadas.

As VMs também são uma excelente opção quando mudar de um servidor físico para a cloud. Pode criar uma imagem do servidor físico com frequência e alojá-lo numa máquina virtual. Isto dá-lhe a liberdade total para escolher os sistemas operativos e os ambientes de execução da aplicação, o que significa que pode desenvolver em quase qualquer linguagem que utilize as ferramentas à sua preferência.

No entanto, irá precisar de manter a máquina virtual. Ou seja, atualizar o sistema operativo e o software em que é executado. 

Também exige mais consideração ao dimensionar. Pode aumentar verticalmente a máquina virtual, o que significa que pode adicionar mais recursos de computação e memória. Mas se precisar de executar várias instâncias em paralelo, poderá ter de adicionar serviços adicionais, como balanceadores de carga.

Imagine que está a executar um site que aloja um site de retalho. Se duplicar a VM, irá precisar de um serviço adicional para encaminhar os pedidos entre várias instâncias da VM do site.

Também existem serviços de máquina de virtual avançados disponíveis no Azure:

* Para executar consistentemente instâncias disponíveis da mesma aplicação ou conjuntos de aplicações em VMs configuradas de forma semelhante, utilize a opção **Conjuntos de Dimensionamento de Máquina Virtual**. Gera, automaticamente, milhares de VMs idênticas carregadas com a sua aplicação em minutos, para que os utilizadores nunca tenham de esperar. E, dado que não tem de aprovisionar previamente as máquinas virtuais, utiliza apenas os recursos de computação que a sua aplicação precisa em qualquer altura.

* Poderão existir situações em que precisa de poder de computação em bruto ou poder de computação de nível de supercomputador. A opção do **Batch** oferece gestão de computação e agendamento de tarefas de escala da cloud com a capacidade de dimensionar para dezenas, centenas ou milhares de VMs. Também pode especificar VMs com funcionalidades de supercomputador.

## <a name="azure-containers"></a>Contentores do Azure

Os contentores são uma excelente opção se pretender executar várias instâncias de uma aplicação numa única máquina virtual. O orquestrador de contentores pode iniciar, parar e aumentar horizontalmente instâncias da aplicação conforme preciso.

No entanto, os contentores servem frequentemente para criar soluções com uma arquitetura de microsserviços. Os contentores servem, muitas vezes, para dividir soluções em partes mais pequenas. Por exemplo, pode dividir um site num contentor que aloja o seu front-end, outro que aloja o back-end e um terceiro para o armazenamento. Isto permite-lhe separar partes da sua aplicação em secções lógicas que podem ser mantidas, dimensionadas ou atualizadas de forma independente.

Imagine que o back-end do seu site atingiu a capacidade máxima, mas o front-end e o armazenamento não estão a ser muito utilizados. Pode dimensionar o back-end separadamente para melhorar o desempenho. Ou pode optar por utilizar um serviço de armazenamento diferente. Ou pode substituir o contentor de armazenamento sem afetar o resto da aplicação.

 Se a sua equipa está familiarizada com a utilização da orquestração de contentores do Kubernetes, considere a opção **Azure Kubernetes Service (AKS)**. Ela simplifica e automatiza a gestão, a implementação e as operações de orquestração do Kubernetes.

## <a name="azure-functions"></a>Funções do Azure

As funções do Azure são ideais quando está preocupado apenas com o código que executa o seu serviço e não a plataforma subjacente ou a infraestrutura. São frequentemente utilizadas quando precisa de realizar ações em resposta a um evento, muitas vezes por um pedido do REST, temporizador ou mensagem de outro serviço do Azure, e quando esse trabalho pode ser concluído rapidamente, em segundos ou menos.

As funções do Azure dimensionam automaticamente, pelo que são uma excelente opção quando o pedido é variável, e o utilizador é cobrado apenas quando uma função é acionada. Por exemplo, pode receber mensagens de uma solução de IoT que serve para monitorizar uma frota de veículos de entregas. Provavelmente vai receber mais dados durante o horário comercial.

As funções do Azure não têm um estado; comportam-se como se fossem reiniciadas sempre que respondem a um evento. Isto é ideal para processar os dados de entrada. E se o estado é obrigatório, podem ligar-se a um serviço de armazenamento do Azure.
