A sua empresa decidiu gerir os dados de vídeo das suas câmaras de trânsito no Azure com VMs. Para poder executar os vários codecs, precisamos primeiro de criar as VMs. Também precisamos de ligar e interagir com essas VMs. Nesta unidade, vai aprender como criar uma VM com o portal do Azure. Vai configurar a VM para o RDP, selecionar uma imagem de VM e escolher a opção de armazenamento adequada.

## <a name="introduction-to-windows-virtual-machines-in-azure"></a>Introdução às máquinas de virtuais do Windows no Azure

As VMs do Azure estão num recurso de computação na cloud dimensionável sob pedido. São semelhantes às máquinas virtual alojadas no Windows Hyper-V. Elas incluem um processador, memória, armazenamento e recursos de rede. Pode iniciar e parar máquinas virtuais à vontade como no Hyper-V e geri-las a partir do portal ou com a CLI do Azure. Também pode utilizar um cliente de RDP para ligar diretamente à interface de utilizador (IU) de ambiente de trabalho do Windows e utilizar a VM como se estivesse a iniciar sessão num computador Windows local.

## <a name="create-resources-for-a-windows-vm"></a>Criar recursos para um VM do Windows

Ao criar uma VM do Windows no Azure, também está a criar recursos para alojar a VM. Como em outros serviços do Azure, precisa de um **Grupo de Recursos**. É uma prática comum incluir outros serviços relacionados com a VM no mesmo grupo de recursos, incluindo:

* A máquina virtual
* Armazenamento
* Redes virtuais 
* Interfaces de rede
* Subrede
* Endereço IP público

Quando cria uma nova VM, pode utilizar um grupo de recursos existente ou criar um novo.

## <a name="choose-the-vm-image"></a>Selecione a imagem de VM

Selecionar a imagem é uma das primeiras e mais importantes decisões que vai tomar ao criar uma VM. Uma imagem é um modelo utilizado para criar uma VM. Estes modelos incluem um sistema operativo e, muitas vezes, outro software, como ferramentas de desenvolvimento ou ambientes de alojamento da Web.

Tudo o que um computador pode ter instalado pode ser incluído numa imagem e isso é poderoso. Pode criar uma VM a partir de uma imagem pré-configurada exatamente para as tarefas de que precisa, como alojar uma aplicação Asp.Net Core.

Pode opcionalmente criar e carregar as suas próprias imagens, mas isso está fora do âmbito deste módulo.

> [!Note] 
> Pode reparar numa funcionalidade chamada "Máquina Virtual (clássico)." Esta é uma funcionalidade de legado que é suportada por clientes que já criaram instâncias. Para novas cargas de trabalho, vai querer a funcionalidade de "Máquina Virtual do Azure" ou, abreviadamente, "Máquinas Virtuais".

## <a name="sizing-your-vm"></a>Dimensionar a sua VM

Tal como uma máquina física tem uma determinada quantidade de memória e potência de CPU, uma máquina virtual também. O Azure oferece uma variedade de VMs de diferentes tamanhos em diferentes pontos de preço. Estas VM começam com um desenvolvimento ao nível de entrada da Série A e testam imagens por toda a Série D para computação de efeitos gerais. Incluem a série H para necessidades computacionais de desempenho elevado e a série N para as funções otimizadas para a unidade de processador gráfico (GPU).

Como vai ver mais tarde no módulo, podemos alterar o tamanho de uma VM após ter sido criado, mas isso requer desligá-la, o que pode resultar num tempo de inatividade para as nossas cargas de trabalho.

## <a name="choosing-storage-options"></a>Escolher opções de armazenamento

A opção seguinte ao especificar uma VM é a tecnologia de unidades de disco rígido. As opções um disco rígido (HDD) mais tradicional ou uma unidade de estado sólido (SSD) mais moderna. O armazenamento SSD custa mais para utilizar, mas dá um melhor desempenho, sobretudo em ambientes que suportam níveis elevados de transferência de dados ou E/S frequente.

> [!Note] 
> As Aplicações nas Máquinas Virtuais do Azure também se podem ligar a outras formas de persistência no Azure como o Azure Cosmos DB e armazenamento de Blobs do Azure.
