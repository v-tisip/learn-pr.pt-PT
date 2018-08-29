## <a name="motivation"></a>Motivação
Suponha que a sua empresa escolheu a CLI do Azure como solução de linha de comandos para gerir recursos do Azure. Os administradores e programadores preferem executar os comandos e scripts localmente em vez de através de um browser. A equipa utiliza máquinas com Linux, macOS e Windows. Tem de colocar a CLI do Azure a funcionar em todos os dispositivos.

## <a name="what-is-the-azure-cli"></a>O que é a CLI do Azure?
A CLI do Azure é um programa de linha de comandos para ligar ao Azure e executar comandos administrativos nos recursos do Azure. Por exemplo, para reiniciar uma Máquina Virtual (VM), teria de utilizar um comando semelhante ao seguinte:

 ```bash
 az vm restart -g MyResourceGroup -n MyVm
 ```

A CLI do Azure fornece ferramentas de linha de comandos para várias plataformas para gerir recursos do Azure e pode ser instalada localmente em computadores com Linux, Mac ou Windows. A CLI do Azure também pode ser utilizada a partir de um browser através do Azure Cloud Shell. Em ambos os casos, pode ser utilizada interativamente ou em scripts. Para uma utilização interativa, primeiro tem de iniciar uma shell, como cmd.exe no Windows ou Bash no Linux ou macOS e, em seguida, emitir o comando na linha de comandos da shell. Para automatizar tarefas repetitivas, tem de montar os comandos da CLI num script da shell através da sintaxe de script da shell escolhida e, em seguida, executar o script.

## <a name="how-to-install-azure-cli"></a>Como instalar a CLI do Azure
No Linux e no macOS, utilize um gestor de pacotes para instalar o PowerShell Core. O gestor de pacotes recomendado é diferente consoante o SO e a distribuição:
- Linux: **apt-get** no Ubuntu, **yum** no Red Hat e **zypper** no OpenSUSE
- Mac: **Homebrew**

A CLI do Azure está disponível no repositório da Microsoft, pelo que primeiro tem de adicionar esse repositório ao gestor de pacotes.

No Windows, instala a CLI do Azure ao transferir e executar um ficheiro MSI.

## <a name="using-the-azure-cli-in-scripts"></a>Utilizar a CLI do Azure em scripts
Se quiser utilizar os comandos da CLI do Azure em scripts, tem de estar atento a quaisquer problemas na "shell" ou no ambiente utilizado para executar o script. Por exemplo, numa shell de bash, é utilizada a seguinte sintaxe quando definir variáveis:

 ```bash
 variable="string"
 variable=integer
 ```

Se utilizar um ambiente do PowerShell para executar scripts da CLI do Azure, terá de utilizar esta sintaxe para as variáveis:

 ```powershell
 $variable="string"
 $variable=integer
 ```

## <a name="summary"></a>Resumo
A CLI do Azure tem de estar instalada antes de poder ser utilizada para gerir recursos do Azure a partir de um computador local. Os passos de instalação variam para Windows, Linux e macOS, mas uma vez instalada, os comandos são comuns entre as plataformas. 
