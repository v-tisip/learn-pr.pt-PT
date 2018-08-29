A criação de scripts de administração é uma forma poderosa de otimizar o seu fluxo de trabalho. Pode automatizar tarefas comuns repetitivas e, após a verificação de um script, este será executado de forma consistente, o que permite reduzir a ocorrência de erros.

Suponha que trabalha numa empresa que utiliza Máquinas Virtuais do Azure (VMs) para testar o seu software de Gestão da Relação com o Cliente (CRM). As VMs são criadas a partir de imagens que incluem um serviço Web de front-end que implementa a lógica de negócio e uma base de dados SQL.

Tem executado vários testes numa única VM, mas reparou que as alterações na base de dados e ficheiros de configuração podem gerar resultados inconsistentes. Num caso, um erro criou um registo de chamada telefónica sem cliente correspondente na base de dados. O registo órfão originou a falha dos testes de integração subsequentes, mesmo depois de o erro ser corrigido. Planeia resolver este problema com uma nova implementação de VM para cada ciclo de testes. Quer automatizar a configuração da criação da VM, uma vez que será executada várias vezes por semana. 

Aqui, verá como gerir recursos do Azure com o Azure PowerShell. Vai utilizar o Azure PowerShell interativamente para tarefas pontuais e escrever scripts para automatizar as tarefas repetidas. 

## <a name="learning-objectives"></a>Objetivos de aprendizagem
> [!div class="checklist"]
> * Decidir se o Azure PowerShell é a ferramenta certa para as suas tarefas de administração do Azure
> * Instalar o Azure PowerShell no Linux, macOS e Windows
> * Ligar a uma subscrição do Azure com o Azure PowerShell
> * Criar recursos do Azure com o Azure PowerShell

## <a name="prerequisites"></a>Pré-requisitos
- Experiência com uma interface de linha de comandos, como o PowerShell ou Bash
- Conhecimento dos conceitos básicos do Azure, como grupos de recursos e Máquinas Virtuais
- Experiência na administração de recursos do Azure com o Portal do Azure
