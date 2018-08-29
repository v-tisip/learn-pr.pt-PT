Suponha que escolheu o Azure PowerShell como solução de automatização. Os administradores preferem executar os scripts localmente em vez de no Azure Cloud Shell. A equipa utiliza máquinas com Linux, macOS e Windows. Tem de colocar o Azure PowerShell a funcionar em todos os dispositivos. 

## <a name="what-must-be-installed"></a>O que deve ser instalado?
Vamos percorrer as instruções de instalação reais na unidade seguinte, mas vamos examinar os dois componentes que constituem o Azure PowerShell.

- **Produto PowerShell base** Tem duas variantes: o PowerShell no Windows e o PowerShell Core no macOS e Linux.
- **Módulo do Azure PowerShell** Este modulo adicional tem de estar instalado para adicionar os comandos específicos do Azure ao PowerShell.

> [!NOTE]
> O PowerShell está incluído no Windows (mas pode ter uma atualização disponível). Terá de instalar o PowerShell Core no Linux e macOS.

Depois de instalar o produto base, adicione o módulo do Azure PowerShell à sua instalação.

## <a name="how-to-install-powershell-core"></a>Como instalar o PowerShell Core
No Linux e no macOS, utilize um gestor de pacotes para instalar o PowerShell Core. O gestor de pacotes recomendado é diferente consoante o SO e a distribuição.

> [!NOTE]
> O PowerShell Core está disponível no repositório da Microsoft, pelo que primeiro tem de adicionar esse repositório ao gestor de pacotes.

### <a name="linux"></a>Linux
No Linux, o gestor de pacotes será alterado consoante a distribuição Linux que escolher.

| Distribuição(ões)  | Gestor de pacotes |
|------------------|-----------------|
| Ubuntu, Debian   | `apt-get`       |
| Red Hat, CentOS  | `yum`           |
| OpenSUSE         | `zypper`        |
| Fedora           | `dnf`           |

### <a name="mac"></a>Mac
No macOS, utilizará `Homebrew` para instalar o PowerShell Core.

## <a name="how-to-install-azure-powershell"></a>Como instalar o Azure PowerShell
Assim que tiver o PowerShell instalado, o método de instalação preferencial para o módulo do Azure PowerShell é utilizar o comando `Install-Module` a partir do PowerShell. Precisará de privilégios elevados para instalar os módulos.

- No Windows, tem de executar o PowerShell como administrador
- No Linux e macOS, utilizará o comando `sudo` para obter privilégios elevados

## <a name="summary"></a>Resumo
O PowerShell está incorporado no Windows, mas tem de instalar o módulo do Azure PowerShell. No Linux e macOS, tem de instalar o PowerShell Core e o módulo do Azure PowerShell. Na secção seguinte, vai percorrer os passos de instalação detalhados para algumas plataformas comuns.