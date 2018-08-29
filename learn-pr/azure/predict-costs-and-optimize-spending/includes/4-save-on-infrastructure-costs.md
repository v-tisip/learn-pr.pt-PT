Vimos como criar estimativas de custo para ambientes que gostaria de criar, percorremos algumas ferramentas para obter detalhes sobre onde estamos a gastar dinheiro e previmos despesas futuras. O nosso próximo desafio é ver como pode reduzir os custos de infraestrutura.

## <a name="use-reserved-instances"></a>Utilizar instâncias reservadas

Se tiver cargas de trabalho de VM que são estáticas e previsíveis por natureza, especialmente as que são executadas 24x7x365, através de instâncias reservadas é uma forma fantástica de poupar potencialmente até 70 por cento, dependendo do tamanho da VM.

![Poupanças de instância reservada](../images/savings-coins.png)

As instâncias reservadas são compradas em prazos de um ou três anos, com pagamento exigido para o prazo total antecipado. Após a compra, a Microsoft corresponde a reserva com as instâncias em execução e diminui as horas da sua reserva. As reservas podem ser compradas através do portal do Azure. E como as instâncias reservadas são um desconto de computação, estão disponíveis para VMs do Linux e Windows.

## <a name="right-size-underutilized-virtual-machines"></a>Dimensionamento correto de máquinas virtuais subutilizadas

Lembre-se da nossa discussão anterior de que o Azure Cost Management e o Assistente do Azure podem recomendar o dimensionamento correto ou o encerramento das VMs. Dimensionar corretamente uma máquina virtual é o processo de redimensioná-la para um tamanho adequado. Vamos imaginar que tem um servidor em execução como um controlador de domínio que está dimensionado como uma **Standard_D4sv3**, mas a VM encontra-se 90 por cento inativa na maior parte do tempo. Ao redimensionar esta VM para uma **Standard_D2s_v3**, reduz o custo de computação em 50 por cento. Os custos são lineares e duplos para cada tamanho maior na mesma série. Neste caso, até pode beneficiar da alteração da série de instância para ir para uma série de VM mais barata.

![Redimensionar VM](../images/vm-resize.png)

Demasiadas máquinas virtuais grandes são uma despesa desnecessária comum no Azure e algo que pode ser facilmente resolvido. Pode alterar o tamanho de uma VM no portal do Azure, no Azure PowerShell ou na CLI do Azure.

> [!NOTE]
> Redimensionar uma VM exige que tenha de ser parada, redimensionada e, em seguida, reiniciada. Esta ação pode demorar alguns minutos, dependendo da importância da alteração de tamanho. Planeie uma falha ou mude o tráfego para outra instância enquanto executa esta tarefa.

## <a name="deallocate-virtual-machines-in-off-hours"></a>Desaloque máquinas virtuais em horários sem atividade

Se tiver cargas de trabalho de máquina virtual que só são utilizadas durante determinados períodos de tempo, mas estiver a executá-las a tempo inteiro todos os dias, está a perder dinheiro. Estas VMs são excelentes candidatas para serem encerradas quando não estiverem em utilização e iniciarem a cópia de segurança com base numa agenda, economizando os custos de computação, enquanto a VM é desalocada.

Esta abordagem é uma excelente estratégia para ambientes de desenvolvimento. Muitas vezes, o desenvolvimento pode ocorrer apenas durante o horário comercial, dando-lhe flexibilidade para desalocar estes sistemas nas horas sem atividade e impedir que os custos de computação acumulem. O Azure tem agora uma [solução de automatização](https://docs.microsoft.com/azure/automation/automation-solution-vm-management) totalmente disponível para tirar partido do seu ambiente.

Também pode utilizar a funcionalidade de encerramento automático numa máquina virtual para agendar encerramentos automatizados.

![Encerramento automatizado](../images/vm-auto-shutdown.png)

## <a name="delete-unused-virtual-machines"></a>Eliminar máquinas virtuais não utilizadas 

 Este conselho pode parecer óbvio, mas se não estiver a utilizar um serviço, deve encerrá-lo. Não é raro encontrar sistemas que não produzem ou sistemas de prova de conceito deixados em torno de um projeto que já não é preciso. Reveja regularmente o seu ambiente e trabalhe para identificar estes sistemas. Encerrar estes sistemas pode oferecer um benefício multifacetado ao fazer com que economize não só em custos de infraestrutura, mas também potencialmente em licenciamento e operações.

## <a name="migrate-to-paas-or-saas-services"></a>Migrar para os serviços PaaS ou SaaS 

Por último, uma vez que move cargas de trabalho para a cloud, uma evolução natural é começar com os serviços de infraestrutura como serviço (IaaS) e, em seguida, movê-los para a plataforma como serviço (PaaS) conforme apropriado, num processo iterativo.

Os serviços de PaaS oferecem, normalmente, poupanças substanciais nos custos de recursos e operacionais. O desafio é que dependendo do tipo de serviço, serão precisos diferentes níveis de esforço para mover para estes serviços, de uma perspetiva de tempo e recursos. Poderá mover facilmente uma base de dados do SQL Server para a Base de Dados SQL do Azure, mas poderá exigir um esforço substancialmente maior para mover a sua aplicação de várias camadas para um contentor ou arquitetura sem servidor. É uma boa prática avaliar continuamente a arquitetura das suas aplicações para determinar se existem ganhos de eficiência através dos serviços de PaaS.  

O Azure facilita o teste destes serviços com pouco risco, ao oferecer a possibilidade de experimentar novos padrões de arquitetura relativamente simples. Dito isto, é normalmente uma jornada mais longa e poderá não ser de ajuda imediata, se estiver à procura de ganhos rápidos de uma perspetiva de economia de custos. O Centro de Arquitetura do Azure é um ótimo lugar para ganhar ideias para transformar a sua aplicação, bem como as melhores práticas numa vasta gama de arquiteturas e serviços do Azure. 