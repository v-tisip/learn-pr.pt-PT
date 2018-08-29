Os produtos do Azure têm uma hierarquia profunda. Por exemplo, vamos supor que precisava de criar uma Máquina Virtual Linux. Pode navegar por estes níveis de: **Início** **>** **Máquinas virtuais** **>** **Computação** **>** **Ubuntu Server**. O portal do Azure otimiza a interface de utilizador para tornar este tipo de sequência de navegação mais intuitiva. Aqui, vai conhecer os principais elementos da interface de utilizador que tornam tudo isto possível. vai navegar por menus e submenus, bem como utilizar painéis para encontrar e configurar serviços.

## <a name="azure-portal-layout"></a>Esquema do Portal do Azure

O portal do Azure é a Interface Gráfica (GUI) para controlar o Microsoft Azure. Pode realizar a grande maioria das ações de gestão no portal e o portal é, regra geral, a melhor interface para a realização de tarefas únicas ou sempre que pretender examinar as opções de configuração em detalhe.

No painel esquerdo do portal encontra-se o painel de recursos, que lista os principais tipos de recursos. Tenha em atenção que o Azure tem muitos mais tipos de recursos do que apenas os exibidos.

## <a name="using-blades-in-azure-portal"></a>Utilizar os painéis no Portal do Azure

O Portal do Azure utiliza um modelo de painéis para a navegação. Um _painel_ é um painel de deslize que contém a interface de utilizador para um único nível numa sequência de navegação. Por exemplo, cada um destes elementos nesta sequência seria representado por um painel: **Máquinas virtuais** **>** **Computação** **>** **Ubuntu Server**.

Normalmente, cada painel na interface de utilizador contém um número de opções configuráveis. Algumas destas opções geram outro painel, que se revela à direita de qualquer painel existente. No novo painel, quaisquer novas opções configuráveis irão gerar outro painel e assim sucessivamente. Em pouco tempo, pode acabar com vários painéis abertos em simultâneo. Também pode maximizar os painéis, para que eles preencham o ecrã inteiro.

Sempre que tentar fechar um painel sem antes guardar as alterações de configuração efetuadas, recebe uma notificação.

## <a name="configuring-settings-in-azure-portal"></a>Configurar Definições no Portal do Azure

O portal do Azure apresenta várias opções de configuração, principalmente na barra de estado, no canto superior direito do ecrã.

### <a name="notifications"></a>Notificações

Clicar no ícone de campainha mostra o painel Notificações. Este painel lista as últimas ações executadas, juntamente com o respetivo estado.

![Painel Notificações](../images/2-notifications-blade.PNG)

### <a name="cloud-shell"></a>Cloud Shell,

Clique no ícone de Cloud Shell (>_), vai criar uma nova sessão do cloud shell. Ser-lhe-á pedido que utilize o Linux Bash ou o PowerShell no Linux nessa sessão.

![Cloud Shell,](../images/2-choose-shell.PNG)

### <a name="settings"></a>Definições

Clicar no ícone de "engrenagem" para alterar as definições do Portal do Azure. Estas definições incluem:

* Hora de fim de sessão
* Esquema de cores
* Temas de alto contraste
* Notificações de alerta (para um dispositivo móvel)
* Faça duplo clique para alterar o tema
* Idioma
* Formato regional

![Definições do Portal](../images/2-settings-blade.PNG)

Quando tiver alterado as definições, clique em **Aplicar** para aceitar as alterações.

### <a name="feedback-blade"></a>Painel Comentários

Clique no ícone expressivo sorridente para abrir o painel **Envie-nos comentários**. Aqui pode enviar comentários à Microsoft sobre o Azure. Tenha em atenção que pode especificar se a Microsoft pode responder aos seus comentários por e-mail.

![Comentários](../images/2-feedback-blade.PNG)

### <a name="help-blade"></a>Painel Ajuda

Clique no ponto de interrogação para mostrar o painel **Ajuda**. Aqui, pode escolher entre vários tópicos, incluindo:

* Novidades
* Roteiro do Azure
* Iniciar visita guiada
* Atalhos de teclado
* Mostrar diagnósticos
* Privacidade + termos

### <a name="directory-and-subscription"></a>Diretório e Subscrição

Clique no ícone de Livro e Filtro para mostrar o painel **Diretório + subscrição**.

O Azure permite-lhe ter mais do que uma subscrição associada a um diretório. Nos painéis Diretório e Subscrição, pode alterar entre subscrições. Aqui, pode alterar a sua subscrição ou alterar para outro diretório.

![Diretório](../images/2-directory-blade-1.PNG)

### <a name="profile-settings"></a>Definições de Perfil

Basta clicar no seu nome, no canto superior direito, para poder alterar as suas definições de perfil.
As opções incluem:

* Terminar sessão do Azure
* Alterar palavra-passe
* Alterar informações de contacto
* Ver permissões
* Submeter uma ideia para a equipa do Azure
* Ver a sua fatura
* Trocar diretório (mostra o painel Diretório + Subscrição como na secção anterior)

![Definições de Perfil](../images/2-portal-menu.png)

Se agora clicar em **Ver a minha fatura**, o Azure leva-o para a página **Gestão de Custos + Faturação - Faturas**, que o ajuda a analisar onde o Azure está a gerar os custos.

![Página Faturação](../images/2-portal-billing.PNG)

## <a name="summary"></a>Resumo

O Azure é um grande produto e a interface de utilizador do portal reflete isso. A principal forma a que o portal recorre para o ajudar a navegar nesta complexidade é com os painéis, para indicar a hierarquia. Os painéis permitem-lhe focar-se numa tarefa específica, ao mesmo tempo que indica claramente o caminho que tomou para atingir esse ponto.