A sua equipa de pesquisa tem de executar o processamento de dados, que é intensivo em termos de computação, e não tem o equipamento para o fazer. A equipa optou por utilizar o Azure para fazer a análise dos dados.

## <a name="what-is-azure-compute"></a>O que é a computação do Azure?
A computação do Azure é um serviço de recursos de computação a pedido para executar aplicações baseadas na cloud. Este serviço oferece recursos de computação, como processadores de vários núcleos e supercomputadores através de máquinas virtuais e contentores. Também oferece computação sem servidor para permitir a execução de aplicações sem configuração de infraestrutura ou configuração. Os recursos estão disponíveis a pedido e, normalmente, podem ser criados em minutos ou até mesmo segundos. Paga apenas pelos recursos que utiliza e o tempo em que os utiliza.

Existem três técnicas comuns para executar a computação no Azure:
1. Máquinas virtuais
1. Contentores
1. Computação sem servidor

## <a name="what-are-virtual-machines"></a>O que são máquinas virtuais?

Uma **máquina virtual (VM)** é uma emulação de software de um computador físico. As VMs incluem um processador virtual, memória, armazenamento e recursos de rede. Alojam um sistema operativo e pode instalar e executar software como se estivesse num computador físico. E, ao utilizar um cliente de ambiente de trabalho remoto, pode utilizar e controlar a máquina virtual como se estivesse sentado à frente de um terminal físico.

### <a name="virtual-machines-in-azure"></a>Máquinas virtuais no Azure

As máquinas virtuais podem ser criadas e alojadas no Azure. Normalmente, as novas máquinas virtuais podem ser criadas e aprovisionadas em minutos ao selecionar uma imagem de máquina virtual pré-configurada.

A seleção de uma imagem é uma das decisões mais importantes que precisará de tomar ao criar uma VM. Uma imagem é um modelo utilizado para criar uma máquina virtual. Estes modelos já incluem um sistema operativo (SO) e, muitas vezes, outro software, como ferramentas de desenvolvimento ou ambientes de alojamento na Web.

## <a name="what-are-containers"></a>O que são contentores?

Os contentores são um ambiente de virtualização, mas, ao contrário de uma máquina virtual, não incluem nenhum sistema operativo. Em vez disso, referenciam o sistema operativo do ambiente anfitrião que executa o contentor. Por exemplo, se estiverem em execução cinco contentores num servidor com um kernel Linux específico, os cinco contentores estarão em execução nesse mesmo kernel. 

Normalmente, os contentores contêm uma aplicação escrita por si e incluirão quaisquer bibliotecas exigidas para que a sua aplicação seja executada no kernel do ambiente do anfitrião. 

Os contentores devem ser leves e foram concebidos para serem criados, aumentados horizontalmente e parados dinamicamente, e exigem mudança de ambiente e procura.

Uma vantagem de utilizar contentores é a capacidade de executar várias aplicações isoladas numa máquina virtual. Uma vez que os contentores propriamente ditos estão protegidos e isolados, não precisa necessariamente de separar as VMs de cargas de trabalho separadas.

O Azure suporta contentores de Docker e várias formas de gerir esses contentores. Os contentores podem ser geridos manualmente ou com os serviços do Azure, como o Azure Kubernetes Service.

### <a name="what-is-serverless-computing"></a>O que é a computação sem servidor?

A computação sem servidor é um ambiente de execução alojado na cloud que executa o seu código, mas elimina totalmente o ambiente de alojamento subjacente. Deverá criar uma instância do serviço e adicionar o código; não é necessária nenhuma configuração da infraestrutura nem manutenção (aliás, nem sequer é permitida).

Deverá configurar as aplicações sem servidor para responder a eventos, o que poderá ser um ponto final de REST, um temporizador ou uma mensagem recebida de outro serviço do Azure. A aplicação sem servidor é executada apenas quando é acionada por um evento. 

A infraestrutura não é da sua responsabilidade. O dimensionamento e o desempenho são processados automaticamente, e são faturados apenas os recursos exatos que utiliza. Nem sequer é preciso reservar a capacidade.

O Azure tem duas implementações de computação sem servidor: as **Funções do Azure**, que podem executar o código em praticamente qualquer linguagem moderna, e o **Azure Logic Apps**, que lhe permite executar lógica acionada pelos serviços do Azure sem ter de escrever código.
