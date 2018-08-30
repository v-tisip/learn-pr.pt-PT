Jaime gere um conjunto de máquinas virtuais do Azure em execução na nossa infraestrutura da Web empresarial, que inclui vários sites e servidores de bases de dados em execução em várias plataformas. 

Apesar de o portal do Azure ser fácil de utilizar, Jaime descobriu que navegar nos diferentes painéis faz com que algumas das tarefas demorem mais tempo. 

Ao analisar as alternativas, ele descobre a ferramenta CLI do Azure.

Ao trabalhar com a CLI do Azure, Jaime pode escrever scripts para verificar o estado dos servidores, implementar uma nova configuração, abrir uma porta ou ligar-se a uma máquina virtual para alterar uma configuração.

Talvez seja como o Jaime e esteja à procura de uma ferramenta que o ajude a automatizar as tarefas no seu ambiente na cloud. Vamos mostrar-lhe como utilizar a CLI do Azure para criar e gerir máquinas virtuais alojadas no Azure. 

## <a name="azure-cli"></a>CLI do Azure

A CLI do Azure é a ferramenta de linha de comandos das várias plataformas da Microsoft para a gestão dos recursos do Azure. Está disponível para macOS, Linux e Windows, ou no browser através do [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview).

> [!IMPORTANT]
> Existem duas versões da ferramenta CLI do Azure disponíveis atualmente: a CLI 1.0 do Azure e a CLI 2.0 do Azure. Vamos utilizar a CLI 2.0 do Azure, que é a versão mais recente e é a recomendada, a menos que esteja a executar scripts herdados escritos para a 1.0. A CLI 1.0 do Azure é iniciada com o comando `azure` e a CLI 2.0 do Azure é iniciada com o comando `az`. 

A CLI do Azure pode ajudá-lo a gerir recursos do Azure como máquinas virtuais e discos, na linha de comandos ou em scripts. Vamos começar e ver o que ela pode fazer.

## <a name="learning-objectives"></a>Objetivos de Aprendizagem
> [!div class="checklist"]
> * Criar uma máquina virtual do Azure com a CLI
> * Redimensionar VMs com a CLI
> * Gerir e consultar uma VM na linha de comandos
> * Instalar software numa VM