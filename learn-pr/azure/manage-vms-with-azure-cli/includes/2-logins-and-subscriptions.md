Antes de começar, vamos rever a sintaxe da ferramenta CLI do Azure. Se tiver concluído o módulo **Controlar os serviços do Azure com a CLI do Azure**, sabe que os comandos da CLI do Azure assumem a forma de:

```azurecli
az [command] [subcommand] [--parameter --parameter]
```

O `[command]` identifica a área específica do Azure que pretende controlar. Por exemplo, pode gerir as informações da subscrição com o comando `account` ou as bases de dados SQL com o comando `sql`. O `[subcommand]` e `[--parameters]` dependem do comando com que está a trabalhar. 

Pode ver uma lista de comandos, subcomandos e parâmetros ao escrever um comando parcial. Por exemplo, se escrever `az` na linha de comandos, será apresentado o ecrã de ajuda de nível superior. Se escrever `az vm`, serão apresentados todos os subcomandos das máquinas virtuais. Esta abordagem pode ser uma excelente forma de explorar a ferramenta CLI do Azure.

> [!NOTE]
> Vamos utilizar o Azure Cloud Shell para trabalhar com a CLI do Azure. Se preferir trabalhar no computador local, todos os comandos abordados podem ser executados na linha de comandos ao [instalar a CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).

## <a name="log-in-to-azure"></a>Iniciar sessão no Azure

A primeira coisa a fazer ao trabalhar com a CLI do Azure é iniciar sessão na sua conta do Azure. Para isso, utilize o comando `login`. Se estiver a utilizar o Cloud Shell, será apresentado um botão para iniciar sessão no Azure.

```azurecli
az login
```

Este comando iniciará uma janela do browser, onde poderá selecionar a conta da Microsoft que quer utilizar.

## <a name="working-with-subscriptions"></a>Trabalhar com subscrições

Neste módulo, vamos trabalhar numa subscrição temporária criada como experiência. Mas, numa situação normal, utilizará uma subscrição da sua própria conta. Se tiver mais de uma subscrição, poderá obter uma lista das subscrições claramente formatada através da instrução `az account list --output table`.

```
Name                                  CloudName    SubscriptionId                        State    IsDefault
------------------------------------  -----------  ------------------------------------  -------  -----------
Contoso Legacy Resources              AzureCloud   abc13b0c-d2c4-64b2-9ac5-2f4cb819b752  Enabled  True
Visual Studio Enterprise              AzureCloud   233aebce-23c2-4572-c056-c029449e93ed  Enabled  False
```

Tenha em atenção que o comando também identifica a subscrição _predefinida_, na qual serão aplicados todos os comandos. Se preferir trabalhar numa subscrição diferente, poderá utilizar o comando `az account set --subscription "[name]"`. Por exemplo, poderíamos definir a nossa subscrição atual para ser `Visual Studio Enterprise` na lista acima através do comando seguinte:

```azurecli
az account set --subscription "Visual Studio Enterprise"
```