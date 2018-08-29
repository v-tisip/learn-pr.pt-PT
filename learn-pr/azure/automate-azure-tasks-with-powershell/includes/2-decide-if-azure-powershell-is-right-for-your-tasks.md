Suponha que tem de escolher uma ferramenta para administrar os recursos do Azure utilizados para testar o seu sistema de Gestão da Relação com o Cliente (CRM). As principais operações que tem de fazer são: criar grupos de recursos e aprovisionar Máquinas Virtuais (VMs).

Quer algo que seja mais fácil para os administradores aprenderem, mas poderoso o suficiente para automatizar a instalação e a configuração de várias máquinas virtuais (VMs) ou criar um script de um ambiente de aplicação completo. Existem várias ferramentas disponíveis. Tem de encontrar a melhor para as suas pessoas e as suas tarefas.

## <a name="what-tools-are-available"></a>Que ferramentas estão disponíveis?
O Azure fornece três ferramentas de administração: 

1. O Portal do Azure 
2. A CLI do Azure
3. Azure PowerShell

Todas oferecem aproximadamente a mesma quantidade de controlo; qualquer tarefa que pode fazer com uma das ferramentas, provavelmente pode fazer com as outras duas. As três destinam-se a várias plataformas, em execução no Windows, macOS e Linux. Diferem em sintaxe, requisitos de configuração e se suportam automatização.

Aqui, vamos descrever cada uma das três opções e fornecer algumas orientações sobre como decidir de entre elas. 

## <a name="what-is-the-azure-portal"></a>O que é o portal do Azure?
O portal do Azure é um site que permite criar, configurar e alterar os recursos na sua subscrição do Azure. O portal é uma Interface de Utilizador Gráfica (GUI) que simplifica a localização do recurso de que precisa e a execução de todas as alterações necessárias. Também o orienta por tarefas administrativas complexas ao fornecer assistentes e sugestões.

O portal não fornece nenhuma forma de automatizar tarefas repetitivas. Por exemplo, para configurar 15 VMs, seria necessário criá-las uma a uma através do assistente de cada VM. Este processo pode ser demorado e propenso a erros para tarefas complexas. 

## <a name="what-is-the-azure-cli"></a>O que é a CLI do Azure?
A CLI do Azure é um programa de linha de comandos para várias plataformas para ligar ao Azure e executar comandos administrativos nos recursos do Azure. Por exemplo, para criar uma VM, teria de utilizar um comando semelhante ao seguinte:

```bash
az vm create \
  --resource-group CrmTestingResourceGroup \
  --name CrmUnitTests \
  --image UbuntuLTS
  ...
```

A CLI do Azure está disponível de duas formas: dentro de um navegador, através do Azure Cloud Shell, ou numa instalação local no Linux, Mac ou Windows. Em ambos os casos, pode ser utilizada interativamente ou em scripts. Para uma utilização interativa, primeiro tem de iniciar uma shell, como `cmd.exe` no Windows ou Bash no Linux ou macOS e, em seguida, emitir o comando na linha de comandos da shell. Para automatizar tarefas repetitivas, tem de montar os comandos num script da shell através da sintaxe de script da shell escolhida e, em seguida, executar o script.

## <a name="what-is-azure-powershell"></a>O que é o Azure PowerShell?
O Azure PowerShell é um módulo que adiciona ao Windows PowerShell ou ao PowerShell Core para lhe permitir ligar à sua subscrição do Azure e gerir os recursos. O Azure PowerShell requer o PowerShell para funcionar. O PowerShell fornece serviços como a janela da shell, análise de comandos, entre outros. O Azure PowerShell adiciona comandos específicos do Azure.

Por exemplo, o Azure PowerShell fornece o comando **New-AzureRmVM** que cria uma Máquina Virtual dentro da sua subscrição do Azure. Para utilizá-la, teria de iniciar a aplicação PowerShell e, em seguida, emitir um comando semelhante ao seguinte:

```powershell
New-AzureRmVm `
    -ResourceGroupName "CrmTestingResourceGroup" `
    -Name "CrmUnitTests" `
    -Image "UbuntuLTS"
    ...
```

O Azure PowerShell está disponível de duas formas: dentro de um navegador, através do Azure Cloud Shell, ou numa instalação local no Linux, Mac ou Windows. Em ambos os casos, tem dois modos à sua escolha. Pode utilizá-lo no modo interativo, em que emite manualmente um comando de cada vez, ou no modo de scripts, em que executa um script composto por vários comandos.

## <a name="how-to-choose-an-administrative-tool"></a>Como escolher uma ferramenta administrativa
Existe uma paridade aproximada entre o portal, a CLI do Azure e o Azure PowerShell relativamente aos objetos do Azure que podem administrar e as configurações que podem criar. Destinam-se também a várias plataformas. Isto significa que vai considerar normalmente vários outros fatores quando fizer a sua escolha:

- **Automatização**: precisa de automatizar um conjunto de tarefas repetitivas ou complexas? O Azure PowerShell e a CLI do Azure suportam isto, enquanto que o portal não.

- **Curva de aprendizagem**: precisa de concluir uma tarefa rapidamente sem aprender novos comandos ou sintaxe? O portal do Azure não requer que aprenda sintaxe ou memorize comandos. No Azure PowerShell e na CLI do Azure, tem de conhecer a sintaxe detalhada de cada comando que utilizar.

- **Conjunto de competências da equipa**: a sua equipa já tem experiência? Por exemplo, a sua equipa pode ter utilizado o PowerShell para administrar o Windows. Se assim for, ficará rapidamente à vontade para utilizar o Azure PowerShell.

## <a name="example"></a>Exemplo
Lembre-se de que está a escolher uma ferramenta administrativa para criar os ambientes de teste para a sua aplicação de CRM. Os administradores têm de efetuar duas tarefas do Azure específicas:

1. Criar um grupo de recursos para cada categoria de testes (unidade, integração e aceitação).
2. Criar várias VMs em cada grupo de recursos antes de cada fase de testes.

Para criar os grupos de recursos, o portal do Azure é uma opção razoável. Tratam-se de tarefas pontuais, pelo que não são necessários scripts para efetuá-las.

Encontrar a melhor ferramenta para criar as VMs é uma decisão mais desafiadora. Tem de criar várias e tem de o fazer repetidamente, talvez várias vezes por semana. Isto significa que precisa de automatização, pelo que o portal do Azure não é uma boa opção. Neste caso, o Azure PowerShell ou a CLI do Azure vão satisfazer as suas necessidades. Se os membros da sua equipa têm algum conhecimento do PowerShell, o Azure PowerShell será provavelmente a melhor opção. O Azure PowerShell está disponível nos sistemas operativos utilizados pela sua equipa de administração, suporta automatização e deve ser rápido de aprender pela sua equipa.

## <a name="summary"></a>Resumo
A primeira experiência da maioria dos administradores com o Azure é no Portal. É uma ótima opção para começar, uma vez que fornece uma interface gráfica simples e bem estruturada, mas tem opções limitadas para automatização. Quando precisar de automatização, o Azure dá-lhe duas opções: o Azure PowerShell para administradores com experiência com o PowerShell e a CLI do Azure para todos os outros.

Na prática, as empresas têm normalmente uma mistura de tarefas pontuais e repetitivas. Isto significa que é comum utilizar o Portal e uma solução de scripts. No nosso exemplo de CRM, é adequado criar os grupos de recursos através do Portal e automatizar a criação de VMs com o PowerShell.

O resto deste módulo concentra-se na instalação e utilização do Azure PowerShell.