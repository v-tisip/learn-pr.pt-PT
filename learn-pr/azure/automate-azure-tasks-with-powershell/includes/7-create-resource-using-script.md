As tarefas repetitivas ou complexas, muitas vezes, consomem muito tempo administrativo. As organizações preferem automatizar estas tarefas para reduzir os custos e evitar erros.

Isto é importante no exemplo da empresa de Gestão das Relações com os Clientes (CRM). Na CRM pode testar o seu software em várias Máquinas Virtuais do Linux (VMs) que tem de eliminar e recriar continuamente. Deve utilizar um script do PowerShell para automatizar a criação das VMs.

Para além do funcionamento essencial de criação de uma VM, tem alguns requisitos adicionais para o seu script. 
- Irá criar várias VMs, pelo que deve colocar a criação dentro de um ciclo
- Tem de criar VMs em três grupos de recursos diferentes, para que o nome do grupo de recursos seja passado para o script como um parâmetro

Nesta secção, verá como escrever e executar um script do Azure PowerShell que cumpre estes requisitos.

## <a name="what-is-a-powershell-script"></a>O que é um script do PowerShell?
Um script do PowerShell é um ficheiro de texto que contém comandos e construções de controlo. Os comandos são invocações de cmdlets. As construções de controlo são funcionalidades de programação como ciclos, variáveis, parâmetros, comentários, etc., disponibilizados pelo PowerShell.

Os ficheiros de script do PowerShell têm uma extensão de ficheiro **.ps1**. Pode criar e guardar estes ficheiros com qualquer editor de texto. 

> [!TIP]
> Se estiver a escrever scripts do PowerShell no Windows, pode utilizar o Windows PowerShell Integrated Scripting Environment (ISE). Este editor oferece funcionalidades como a sintaxe colorida e uma lista dos cmdlets disponíveis.
>
>![A ISE do Windows PowerShell](../media-drafts/7-windows-powershell-ise-screenshot.png)

Assim que gravar o script, execute-o a partir da linha de comandos do PowerShell ao passar o nome do ficheiro precedido por um ponto e uma barra invertida:

```powershell
.\myScript.ps1
```

## <a name="powershell-techniques"></a>Técnicas do PowerShell
O PowerShell tem muitas funcionalidades encontradas em linguagens de programação típicas. Pode definir variáveis, utilizar ramos e ciclos, capturar parâmetros da linha de comandos, escrever funções, adicionar comentários e assim por diante. Iremos precisar de três funcionalidades para o nosso script: variáveis, ciclos e parâmetros.

### <a name="variables"></a>Variáveis
O PowerShell suporta variáveis. Utilize **$** para declarar uma variável e **=** para atribuir um valor. Por exemplo:

```powershell
$loc = "East US"
$iterations = 3
```

As variáveis podem conter objetos. Por exemplo, a seguinte definição define a variável **adminCredential** para o objeto devolvido pelo cmdlet **Get-Credential**.

```powershell
$adminCredential = Get-Credential
```

Para obter o valor armazenado numa variável, utilize o prefixo **$** e o respetivo nome, conforme mostrado abaixo: 

```powershell
$loc = "East US"
New-AzureRmResourceGroup -Name "MyResourceGroup" -Location $loc
```

### <a name="loops"></a>Ciclos
O PowerShell tem vários ciclos: **For**, **Do...While**, **For...Each** e assim por diante. O ciclo **For** é a melhor correspondência para as nossas necessidades porque iremos executar um cmdlet um número fixo de vezes.

A sintaxe de núcleo é mostrada abaixo; o exemplo é executado durante duas iterações e imprime sempre o valor de **i**. Os operadores de comparação são escritos **-lt** para "menos de", **-le** para "menos de ou igual a", **eq** para "igual", **ne** para "não igual a", etc.

```powershell
For ($i = 1; $i -lt 3; $i++)
{
    $i
}
```

### <a name="parameters"></a>Parâmetros
Quando executa um script, pode passar argumentos na linha de comandos. Pode indicar nomes para cada parâmetro para ajudar o script a extrair os valores. Por exemplo:

```powershell
.\setupEnvironment.ps1 -size 5 -location "East US"
```

No script, capture os valores em variáveis. Neste exemplo, os parâmetros são correspondidos por nome:

```powershell
param([string]$location, [int]$size)
```

Pode omitir os nomes da linha de comandos. Por exemplo:

```powershell
.\setupEnvironment.ps1 5 "East US"
```

No script, o utilizador depende da posição para a correspondência quando os parâmetros não têm nome:

```powershell
param([int]$size, [string]$location)
```

## <a name="how-to-create-a-linux-virtual-machine"></a>Como criar uma Máquina Virtual do Linux
O Azure PowerShell disponibiliza o cmdlet **New-AzureRmVm** para criar uma Máquina Virtual. O cmdlet tem vários parâmetros para permitir lidar com o grande número de definições de configuração de VM. A maioria dos parâmetros tem valores predefinidos razoáveis, portanto, precisamos apenas de especificar cinco coisas:
- **ResourceGroupName**: O grupo de recursos no qual a nova VM será colocada.
- **VM Name (Nome da VM)**: O nome da VM no Azure.
- **Localização**: A localização geográfica onde a VM será aprovisionada.
- **Credencial**: Um objeto que contém o nome de utilizador e a palavra-passe para a conta de administrador da VM. Iremos utilizar o cmdlet **Get-Credential** para pedir um nome de utilizador e palavra-passe. O **Get-Credential** inclui o nome de utilizador e a palavra-passe num objeto de credencial, que devolve como resultado.
- **Imagem**: identidade do sistema operativo a utilizar para a VM. Nós iremos utilizar "UbuntuLTS".

A sintaxe do cmdlet é mostrada abaixo:

```powershell
   New-AzureRmVm 
       -ResourceGroupName <resource group name> 
       -Name <machine name> 
       -Credential <credentials object> 
       -Location <location> 
       -Image <image name>
```

## <a name="summary"></a>Resumo
A combinação do PowerShell e do Azure PowerShell oferece-lhe todas as ferramentas que precisa para automatizar o Azure. No nosso exemplo do CRM, poderemos criar várias VMs do Linux com um parâmetro para manter o script genérico e um ciclo para evitar o código repetido. O que significa que uma operação anteriormente complexa agora pode ser executada num único passo.