O Azure PowerShell permite-lhe escrever comandos e executá-los imediatamente. Isto é conhecido como **modo interativo**.

Lembre-se de que o objetivo geral no exemplo de Gestão das Relações com os Clientes (CRM) consiste em criar três ambientes de teste que contêm as VMs. Irá utilizar grupos de recursos para garantir que as VMs são organizadas em ambientes separados: um para testes de unidade, um para testes de integração e um para testes de aceitação. Precisa apenas de criar os grupos de recursos, o que significa que o modo interativo do PowerShell é uma boa opção.

Esta secção mostra alguns exemplos de utilização do PowerShell interativamente para iniciar sessão na sua subscrição do Azure e criar grupos de recursos.

## <a name="what-are-powershell-cmdlets"></a>O que são cmdlets do PowerShell?
Um comando do PowerShell é chamado um **cmdlet** (pronunciado "command-let"). Um cmdlet é um comando que manipula uma única funcionalidade. O termo **cmdlet** significa "pequeno comando". Por convenção, os autores de cmdlet são incentivados a manterem os cmdlets simples e com uma única finalidade.

O produto base do PowerShell é enviado com cmdlets que funcionam com funcionalidades como sessões e tarefas em segundo plano. Adicione módulos à instalação do PowerShell para obter os cmdlets que manipulam outras funcionalidades. Por exemplo, existem módulos de terceiros para trabalhar com o ftp, administrar o sistema operativo, aceder ao sistema de ficheiros e assim por diante.

Os cmdlets seguem uma convenção de nomenclatura de verbo-substantivo; Por exemplo, **Get-Process**, **Format-Table**, e **Start-Service**. Também existe uma convenção para escolha do verbo: "get" para obter dados, "set" para inserir ou atualizar dados, "format" para formatar dados, "out" para direcionar a saída a um destino e assim por diante.

Incentivamos os autores do cmdlet a incluírem um ficheiro de ajuda para cada cmdlet. O cmdlet **Get-Help** apresenta o ficheiro de ajuda para qualquer cmdlet:

```powershell
Get-Help <cmdlet-name> -detailed
```

## <a name="what-is-azurerm"></a>O que é o AzureRM?
O **AzureRM** é o nome formal para o módulo do Azure PowerShell que contém cmdlets para trabalhar com funcionalidades do Azure (o **RM** no nome do significa **Gestor de Recursos**). Ele contém centenas de cmdlets que lhe permitem controlar quase todos os aspetos de cada recurso do Azure. Pode trabalhar com grupos de recursos, armazenamento, máquinas virtuais, Azure Active Directory, contentores, aprendizagem automática e assim por diante.

## <a name="how-to-create-a-resource-group"></a>Como criar um grupo de recursos
Em seguida, vamos criar um grupo de recursos com uma instalação local do Azure PowerShell. 

Existem quatro passos: 
1. Importe os cmdlets do Azure.
1. Ligue à sua subscrição do Azure.
1. Crie o grupo de recursos.
1. Certifique-se de que a criação foi concluída com êxito (ver abaixo).

![Passos para criar um recurso no Azure com o Azure PowerShell](../media-drafts/5-create-resource-overview.png)

Cada passo corresponde a um cmdlet diferente.

### <a name="import"></a>Importar
No arranque, o PowerShell carrega apenas os cmdlets de núcleo por predefinição. O que significa que os cmdlets que precisa para trabalhar com o Azure não serão carregados. A forma mais fiável de carregar os cmdlets que precisa é importá-los manualmente no início da sua sessão do PowerShell.

Utilize o cmdlet **Import-Module** para carregar módulos. Este cmdlet tem vários parâmetros para lidar com uma variedade de situações. Por exemplo, pode carregar vários módulos, uma versão do módulo específico, parte de um módulo e assim por diante. Para carregar um módulo completo, a sintaxe é simplesmente:

```powershell
Import-Module <module-name>
```

> [!TIP]
> Se trabalha com o Azure PowerShell com frequência, existem duas formas para automatizar o processo de carregamento de módulo. Pode adicionar uma entrada ao seu perfil do PowerShell para importar o módulo do Azure no arranque ou utilizar as versões mais recentes do PowerShell, o que carrega automaticamente o módulo de contenção ao utilizar um cmdlet.

### <a name="connect"></a>Ligar
Assim que estiver a trabalhar com uma instalação local do Azure PowerShell, terá de autenticar antes de poder executar comandos do Azure. O cmdlet **Connect-AzureRmAccount** pede as credenciais do Azure e, em seguida, liga-se à sua subscrição do Azure. Ele tem muitos parâmetros opcionais, mas se precisar apenas de uma linha de comandos interativa, não são precisos parâmetros:

```powershell
Connect-AzureRmAccount
```

### <a name="create"></a>Criar
O cmdlet **New-AzureRmResourceGroup** cria um grupo de recursos. Tem de especificar um nome e localização. O nome tem de ser exclusivo na sua subscrição. A localização determina onde os metadados para o grupo de recursos serão armazenados (podem ser importantes para si por motivos de conformidade). Utilize cadeias de carateres como "E.U.A. Oeste", "Europa do Norte" ou "	Oeste da Índia" para especificar a localização. Tal como acontece com a maioria dos cmdlets do Azure, o **New-AzureRmResourceGroup** tem muitos parâmetros opcionais; no entanto, a sintaxe de núcleo é:

```powershell
New-AzureRmResourceGroup -Name <name> -Location <location>
```

### <a name="verify"></a>Verificar
O **Get-AzureRmResource** lista os seus recursos do Azure. Isto é útil aqui para verificar se a criação do grupo de recursos foi concluída com êxito.

```powershell
Get-AzureRmResource
```

Para obter uma vista mais concisa, pode enviar a saída do **Get-AzureRmResource** para o cmdlet **Format-Table** com um pipe "|".

```powershell
Get-AzureRmResource | Format-Table
```

## <a name="summary"></a>Resumo
O modo interativo do PowerShell é adequado para tarefas pontuais. No nosso exemplo, vamos utilizar o mesmo grupo de recursos para o tempo de vida do projeto, o que significa que é razoável criá-lo de forma interativa. O modo interativo é, muitas vezes, mais rápido e fácil para esta tarefa do que escrever um script e executá-lo exatamente uma vez.