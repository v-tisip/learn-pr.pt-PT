
Neste exercício, vai instalar a CLI do Azure no computador local e, em seguida, executar um comando simples para verificar a instalação. 

## <a name="installing-the-azure-cli"></a>Instalar a CLI do Azure
O método utilizado para instalar a CLI do Azure depende do sistema operativo do computador. Escolha os passos para o seu sistema operativo.

### <a name="linux"></a>Linux
Aqui, vai instalar a CLI do Azure no Ubuntu Linux com o Advanced Packaging Tool (**apt**) e a linha de comandos do Bash.

> [!NOTE]
> Os comandos listados abaixo referem-se à versão 18.04 do Ubuntu. Se estiver a utilizar uma versão diferente do Ubuntu, terá de adicionar um repositório diferente. Para obter os detalhes, veja [Instalar a CLI 2.0 do Azure com apt](https://docs.microsoft.com/cli/azure/install-azure-cli-apt).

1. Modifique a lista de origens para que o repositório da Microsoft seja registado e o gestor de pacotes possa localizar o pacote da CLI do Azure.

    ```bash
    AZ_REPO=$(lsb_release -cs)
    echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | \
    sudo tee /etc/apt/sources.list.d/azure-cli.list
    ```
1. Importe a chave de encriptação do repositório Ubuntu da Microsoft. Este procedimento permitirá que o gestor de pacotes verifique se o pacote da CLI do Azure que instala é da Microsoft.

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```
1. Instale a CLI do Azure.

    ```bash
    sudo apt-get install apt-transport-https
    sudo apt-get update && sudo apt-get install azure-cli
    ```

### <a name="macos"></a>macOS
Aqui, vai instalar a CLI do Azure no macOS, com o gestor de pacotes Homebrew.

> [!IMPORTANT]
> Se o comando **brew** não estiver disponível, poderá ter de instalar o gestor de pacotes Homebrew. Para obter os detalhes, veja o [site do Homebrew](https://brew.sh/).

1. Atualize o repositório brew para se certificar de que obtém o pacote mais recente da CLI do Azure.

    ```bash
    brew update
    ```
1. Instale a CLI do Azure.

    ```bash
    brew install azure-cli
    ```

### <a name="windows"></a>Windows
Aqui, vai instalar a CLI do Azure no Windows com o instalador MSI.

1. Aceda a [https://aka.ms/installazurecliwindows](https://aka.ms/installazurecliwindows) e, na caixa de diálogo de segurança do browser, clique em **Executar**.
1. No instalador, aceite os termos de licenciamento e clique em **Instalar**.
1. Na caixa de diálogo **Controlo de Conta de Utilizador**, selecione **Sim**.

## <a name="running-the-azure-cli"></a>Executar a CLI do Azure
Execute a CLI do Azure ao abrir uma shell do Bash (Linux e macOS) ou a partir da linha de comandos ou do PowerShell (Windows).

1. Inicie a CLI do Azure e verifique a instalação ao executar a verificação da versão.

    ```bash
    az --version
    ```

> [!NOTE]
> No Windows, executar a CLI do Azure a partir do PowerShell tem algumas vantagens em relação a executar a CLI do Azure a partir da linha de comandos; por exemplo, o PowerShell fornece funcionalidades de conclusão de separadores adicionais em comparação com aquelas disponíveis na linha de comandos. 

## <a name="summary"></a>Resumo
Acabou de configurar os computadores locais para administrar os recursos do Azure com a CLI do Azure. Agora, pode utilizar a CLI do Azure localmente para introduzir comandos ou executar scripts. O Azure PowerShell encaminhará os comandos para os datacenters do Azure, onde serão executados no contexto da sua subscrição do Azure.
