Imagine que trabalha numa empresa que faz o processamento de dados das câmeras de tráfego. Os fluxos de vídeo são analisados, categorizados e processados para identificar rostos e matrículas em alturas específicas. Estas informações são, em seguida, carregadas para o Azure Data Lake e é gerado um índice pesquisável.

Estes fluxos de vídeo utilizam uma variedade de diferentes codecs e resoluções. Terá de executar vários pacotes de software proprietário com base no Windows para realizar o processamento inicial e codificá-los num formato de vídeo comum. Uma vez que são lançados novos formatos regularmente, é vantajoso realizar o processamento de vídeo em máquinas virtuais (VMs). Os pacotes proprietários podem ser, em seguida, adicionados e atualizados sem interromper todo o sistema.

Para administrar o software de codificação nas máquinas virtuais do Windows, terá de se ligar à interface de utilizador.

Neste módulo, vai aprender a criar uma máquina virtual do Windows e a ligar-se com o protocolo RDP (Remote Desktop).

## <a name="learning-objectives"></a>Objetivos de aprendizagem
> [!div class="checklist"]
> * Criar uma máquina virtual do Windows com o portal do Azure.
> * Conhecer as opções que estão disponíveis para as máquinas virtuais no Azure.
> * Ligar-se a uma máquina virtual do Windows em execução através da Ligação ao Ambiente de Trabalho Remoto do Windows.

## <a name="prerequisites"></a>Pré-requisitos

- Conhecimento do ambiente dos Serviços Cloud do Azure.
- Estar familiarizado com as máquinas virtuais.
