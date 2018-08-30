Neste exercício, vai instalar o **Azure PowerShell** no computador local. Escolha a seção apropriada para o sistema operativo.

## <a name="linux-and-mac"></a>Linux e Mac
No Linux e no macOS, o primeiro passo é instalar o **PowerShell Core**.

### <a name="linux"></a>Linux
Conforme mencionado na última unidade, instalar o PowerShell para Linux implicará utilizar um gestor de pacotes. Vamos utilizar o **Ubuntu 18.04** neste exemplo, mas temos [instruções detalhadas para outras versões e distribuições na nossa documentação](https://docs.microsoft.com/powershell/scripting/setup/installing-powershell-core-on-linux).

Aqui, vai instalar o PowerShell Core no Ubuntu Linux com o Advanced Packaging Tool (**apt**) e a linha de comandos do Bash. 

1. Importe a chave de encriptação do repositório Ubuntu da Microsoft. Este procedimento permitirá que o gestor de pacotes verifique se o pacote do PowerShell Core que instala é da Microsoft.

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```
1. Registe o **repositório Microsoft Ubuntu** para que o Gestor de pacotes possa localizar o pacote do PowerShell Core.

    ```bash
    sudo curl -o /etc/apt/sources.list.d/microsoft.list https://packages.microsoft.com/config/ubuntu/18.04/prod.list
    ```

1. Atualize a lista de pacotes.

    ```bash
    sudo apt-get update
    ```

1. Instale o PowerShell Core.

    ```bash
    sudo apt-get install -y powershell
    ```

1. Inicie o PowerShell para verificar se foi instalado com êxito.

    ```bash
    pwsh
    ```

### <a name="macos"></a>macOS
Em seguida, instale o **PowerShell Core** no macOS, com o gestor de pacotes Homebrew.

> [!IMPORTANT]
> Se o comando **brew** não estiver disponível, poderá ter de instalar o gestor de pacotes Homebrew. Para obter os detalhes, veja o [site do Homebrew](https://brew.sh/).

1. Instale o Homebrew-Cask, para obter mais pacotes, incluindo o pacote do PowerShell Core:

    ```bash
    brew tap caskroom/cask
    ```
1. Instale o PowerShell Core:

    ```bash
    brew cask install powershell
    ```

1. Inicie o PowerShell para verificar se foi instalado com êxito:

    ```bash
    pwsh
    ```

## <a name="install-azure-powershell"></a>Instalar o Azure PowerShell
Depois de instalar a produto **PowerShell** base, instale o **Azure PowerShell** para adicionar os comandos específicos do Azure.

### <a name="windows"></a>Windows
Instale o Azure PowerShell no Windows com o comando `Install-Module` do PowerShell.

> [!IMPORTANT]
> Precisa do PowerShell versão 5.0 ou superior para instalar o Azure PowerShell. Para verificar a versão do PowerShell, utilize o comando seguinte: 
>
> `$PSVersionTable.PSVersion` 
>
>Se o número da versão for inferior a 5.0, siga as instruções para [atualizar o PowerShell existente no Windows](https://docs.microsoft.com/powershell/scripting/setup/installing-windows-powershell?view=powershell-6#upgrading-existing-windows-powershell).

1. Abra o menu **Iniciar** e escreva **Windows PowerShell**.
2. Clique com o botão direito do rato no ícone **Windows PowerShell** e selecione **Executar como administrador**.
3. Na caixa de diálogo **Controlo de Conta de Utilizador**, selecione **Sim**.
4. Digite o comando seguinte e, em seguida, prima Enter:

    ```powershell
    Install-Module -Name AzureRM
    ```
5. Quando lhe for perguntado se confia nos módulos do PSGallery, responda **Sim** ou **Sim para Todos**.

> [!NOTE]
> Se obtiver uma mensagem de erro a indicar que já está instalada uma versão do módulo do Powershell do Azure, poderá atualizar para a versão _mais recente_ ao emitir o comando:
> 
> `Update-Module -Name AzureRM`
> 
> Tal como no comando `Install-Module`, responda **Sim** ou **Sim para Todos** quando lhe for perguntado se confia no módulo.

### <a name="linux-or-macos"></a>Linux ou macOS
Utilizamos o mesmo processo básico para instalar o Azure PowerShell no Linux ou no macOS. O procedimento é o mesmo para ambos os sistemas operativos. A diferença está na obtenção de uma sessão elevada do PowerShell Core.

1. Num terminal, escreva o comando seguinte para iniciar o PowerShell Core com privilégios elevados.

    ```bash
    sudo pwsh
    ```

1. Execute o seguinte comando na linha de comandos do Azure PowerShell para instalar o Azure PowerShell.

    ```powershell
    Install-Module AzureRM.NetCore
    ```

1. Quando lhe for perguntado se confia nos módulos do **PSGallery**, responda **Sim** ou **Sim para Todos**.

## <a name="summary"></a>Resumo
Acabou de configurar os computadores locais para administrar os recursos do Azure com o Azure PowerShell. Agora, pode utilizar o Azure PowerShell localmente para introduzir comandos ou executar scripts. O Azure PowerShell vai encaminhar os comandos para os datacenters do Azure, onde serão executados no contexto da sua subscrição do Azure.