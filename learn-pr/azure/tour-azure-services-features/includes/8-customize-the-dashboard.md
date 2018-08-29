Aqui, vai criar e modificar dashboards com a IU do portal e ao editar diretamente o ficheiro JSON subjacente.

## <a name="what-is-a-dashboard"></a>O que é um Dashboard?

Um _dashboard_ é uma coleção personalizável de mosaicos da IU apresentada no portal do Azure. Pode adicionar, remover e posicionar os mosaicos para criar a vista exata que quer e guardar essa vista como um dashboard. São suportados vários dashboards e pode alternar entre eles, conforme necessário. Pode até partilhar os dashboards com outros membros da equipa.

Os dashboards dão-lhe flexibilidade considerável em termos de como gerir o Azure. Por exemplo, pode criar dashboards para funções específicas dentro da organização e utilizar o Controlo de Acesso Baseado em Funções (RBAC) para controlar quem pode aceder a esse dashboard. Por conseguinte, o administrador da base de dados teria um dashboard com vistas do serviço da base de dados SQL, ao passo que o administrador do Azure Active Directory teria vistas dos utilizadores e grupos no Azure AD.

Os dashboards são armazenados como ficheiros JavaScript Object Notation (.JSON). Isto significa que podem ser carregados e transferidos para outros computadores ou partilhados com os membros do diretório do Azure. O Azure armazena os dashboards em grupos de recursos, tal como máquinas virtuais ou contas de armazenamento que pode gerir no portal.

Uma vez que os dashboards são ficheiros .JSON, também pode personalizá-los programaticamente, o que os torna ferramentas administrativas muito poderosas. Além disso, alguns tipos de mosaico podem ser baseados em consultas para que sejam atualizados automaticamente quando os dados de origem forem alterados.

## <a name="default-dashboard"></a>Dashboard Predefinido

O Dashboard predefinido é simplesmente denominado Dashboard. Quando inicia sessão no portal, é apresentado este dashboard com cinco peças Web.

![Peças Web Predefinidas](../images/4-dashboard-default-webparts.png)

Estas peças Web predefinidas são

1. Todos os recursos
2. Inícios rápidos + tutoriais
3. Service Health
4. Marketplace
5. Introdução ao Azure

## <a name="creating-and-managing-dashboards"></a>Criar e Gerir Dashboards

Na parte superior do dashboard estão os controlos que permitem criar, carregar, transferir, editar e partilhar um dashboard. Também pode mudar um dashboard para ecrã inteiro, cloná-lo ou eliminá-lo.

![Personalizar Controlos do Dashboard](../images/7-customise-dashboard-controls.PNG)

### <a name="select-dashboard"></a>Selecionar Dashboard

À esquerda está o controlo de lista pendente Selecionar Dashboard. Clicar neste controlo permite selecionar de entre os dashboards que já definiu para a sua conta. Este controlo simplifica a definição de vários dashboards para diferentes finalidades e, em seguida, mudar simplesmente de um para outro e vice-versa, consoante o que está a tentar fazer no momento.

Tenha em atenção que quaisquer dashboards que criar serão inicialmente privados, ou seja, apenas podem ser vistos por si. Para tornar um dashboard disponível em toda a empresa, tem de partilhá-lo. Consulte a secção posterior sobre partilhar/anular a partilha de dashboards para obter mais informações.

### <a name="create-a-new-dashboard"></a>Criar um novo dashboard

Para criar um novo dashboard, basta clicar em **Novo dashboard**. É apresentada a área de trabalho do dashboard, sem mosaicos. Pode agora adicionar mosaicos, conforme detalhado na secção posterior em Editar um Dashboard através da Interface de Utilizador mais à frente nesta unidade. Quando tiver terminado de adicionar e ajustar os mosaicos, e tiver alterado o nome do dashboard, basta clicar em **Personalização concluída** para guardar e mudar para esse dashboard.

### <a name="upload-and-download"></a>Carregar e Transferir

Os botões **Carregar** e **Transferir** permitem transferir o dashboard atual como um ficheiro .JSON, personalizá-lo, distribuí-lo e carregá-lo ou ter outra pessoa a carregar esse ficheiro novamente para o Portal do Azure, substituindo assim o respetivo dashboard atual.

Se clicar em **Transferir**, o dashboard atual é transferido para a pasta Transferências predefinida. Abrir o ficheiro transferido mostra o código .JSON.

![Código JSON do dashboard](../images/7-dashboard-json-code.PNG)

Em seguida, pode editar esse código manualmente, por exemplo, ao alterar os tamanhos dos mosaicos, e carregá-lo novamente para o Azure ao clicar no botão **Carregar**.

### <a name="edit-a-dashboard"></a>Editar um Dashboard

Veja o tópico Editar um Dashboard através da Interface de Utilizador para obter mais informações sobre este assunto.

### <a name="shareunshare-a-dashboard"></a>Partilhar/Anular a Partilha de um Dashboard

Quando define um novo dashboard, este é privado e apenas está visível para a sua conta. Para torná-lo visível para outras pessoas, tem de partilhá-lo. No entanto, tal como qualquer outro recurso do Azure, tem de especificar um Grupo de Recursos (ou utilizar um grupo de recursos existente) para armazenar os dashboards partilhados. Se não tiver um grupo de recursos existente, o Azure irá criar um grupo de recursos denominado "dashboards" em qualquer localização que especificar. Se já existirem grupos de recursos, pode especificar esse grupo de recursos para armazenar os dashboards.

![Partilha e Controlo de Acesso 1](../images/7-share-dashboards-default.PNG)

Quando tiver partilhado o modelo, verá um segundo painel **Partilha + controlo de acesso**.

![Partilha e Controlo de Acesso 2](../images/7-share-dashboards-access-control.PNG)

Em seguida, pode clicar em **Gerir utilizadores** para especificar os utilizadores que têm acesso a esse dashboard.

### <a name="switching-to-a-shared-dashboard"></a>Mudar para um dashboard partilhado

Para mudar para um dashboard partilhado, clique na lista de dashboards e, em seguida, em **Procurar todos os dashboards**.

![Procurar todos os dashboards](../images/7-browse-dashboards.PNG)

Agora, verá o painel Todos os dashboards, com os nomes de quaisquer dashboards partilhados apresentados. Basta clicar num dashboard para aplicá-lo ao portal do Azure.

![Dashboards partihados](../images/7-select-shared-dashboard.png)

### <a name="display-a-dashboard-as-a-full-screen"></a>Apresentar um Dashboard como um Ecrã Inteiro

Se realmente quiser o maior dashboard, clique no botão **Ecrã inteiro** para mostrar o dashboard atual sem menus do browser. Se tiver mosaicos fora dos limites do ecrã, as barras de controlo de deslize serão apresentadas à direita e na parte inferior do ecrã.

Quando tiver terminado de trabalhar no modo de ecrã inteiro, prima a tecla ESC ou clique em **Sair do Ecrã Inteiro** junto ao nome do Dashboard na parte superior do ecrã.

### <a name="clone-a-dashboard"></a>Clonar um Dashboard

A clonagem de um dashboard cria simplesmente uma cópia instantânea denominada "Clone de (nome do dashboard)" e muda para essa cópia como dashboard atual. A clonagem é também uma forma fácil de criar dashboards antes de partilhá-los. Por exemplo, se tiver um dashboard quase conforme o quer, basta cloná-lo, fazer as alterações necessárias e, em seguida, partilhá-lo.

### <a name="delete-a-dashboard"></a>Eliminar um Dashboard

A eliminação de um dashboard remove-o da lista de dashboards disponíveis. É-lhe pedido para confirmar que quer eliminar o dashboard, mas não existe uma forma de recuperar um dashboard que tenha sido eliminado.

## <a name="edit-a-dashboard-through-the-user-interface"></a>Editar um Dashboard através da Interface de Utilizador

Embora possa editar um dashboard ao transferir o ficheiro .JSON, alterar os valores no ficheiro e carregar o ficheiro novamente para o Azure, essa abordagem não é muito intuitiva para criar uma interface de utilizador. Para utilizar a GUI para configurar o dashboard atual, clique no botão **Editar** ou clique com o botão direito do rato no dashboard e clique em **Editar**. O dashboard muda para o modo de edição.

![Editar Dashboard](../images/7-edit-dashboard.PNG)

No lado esquerdo, é apresentada a Galeria de Mosaicos, com um número de mosaicos abaixo. Pode filtrar a Galeria de Mosaicos pelos seguintes critérios:

* Geral
* Tipo
* Pesquisa
* Grupo de Recursos
* Etiqueta

![Galeria de Mosaicos](../images/7-tile-gallery.png)

Também pode refinar ainda mais cada uma destas opções por categoria, por exemplo, Azure Active Directory, Internet das Coisas, Microsoft Intune e assim sucessivamente.

Adicionar mosaicos é simplesmente uma questão de selecionar o mosaico na lista à esquerda, arrastá-lo e largá-lo na área de trabalho. Em seguida, pode mover cada mosaico, redimensioná-lo ou alterar os dados que apresenta.

A área de trabalho no modo de edição está dividida em quadrados. Cada mosaico tem de ocupar, pelo menos, um quadrado e os mosaicos serão ajustados ao maior conjunto de divisores de mosaicos mais próximo. Os mosaicos sobrepostos são retirados do caminho. Quando reduzir o tamanho de um mosaico, os mosaicos ao redor serão movidos em direção ao mesmo.

### <a name="change-tile-sizes"></a>Alterar tamanhos de mosaicos

Alguns mosaicos têm um tamanho definido e apenas pode editar o tamanho programaticamente. No entanto, os mosaicos com um canto inferior direito cinzento podem ser editados ao arrastar e largar o indicador de canto.

![Mosaico Redimensionável](../images/7-resizable-tile.png)

Em alternativa, clique com o botão direito do rato no menu de contexto e especifique o tamanho que quer.

![Tamanho do Mosaico](../images/7-tile-size.png)

Para criar o dashboard, basta extrair mosaicos da Galeria de Mosaicos para a área de trabalho e, em seguida, reorganizá-los.

### <a name="change-tile-settings"></a>Alterar definições de mosaicos

Alguns mosaicos têm definições editáveis. Por exemplo, com o mosaico de relógio, quando o arrasta para a área de trabalho, abre o mosaico **Editar relógio**. Em seguida, pode definir o fuso horário e se deve apresentar o formato de 12 ou 24 horas.

![Editar Relógio](../images/7-edit-clock.png)

Para empresas multinacionais ou transcontinentais, pode adicionar mais relógios, cada um num fuso horário diferente.

### <a name="accepting-your-edits"></a>Aceitar as edições

Quando tiver organizado os mosaicos conforme os quer, clique em **Personalização concluída** ou clique com o botão direito do rato e clique em **Personalização concluída**.

## <a name="edit-a-dashboard-by-changing-the-json-file"></a>Editar um Dashboard ao alterar o ficheiro .JSON

Também pode editar um dashboard ao alterar o ficheiro .JSON. Esta abordagem fornece mais opções para alterar as definições, mas não é possível ver as alterações até carregar o ficheiro novamente para o Azure.

![Definições de JSON](../images/7-json-code.png)

No exemplo acima, para alterar o tamanho do mosaico, edite as variáveis colSpan e rowSpan e, em seguida, guarde o ficheiro e carregue-o novamente para o Azure. Também pode distribuir o ficheiro a outros utilizadores.

## <a name="reset-a-dashboard"></a>Repor um dashboard

Pode repor qualquer dashboard para o estilo predefinido. No modo de edição, clique com o botão direito do rato e selecione **Repor para o estado predefinido**. Uma caixa de diálogo irá pedir-lhe para confirmar que quer repor esse dashboard.

## <a name="summary"></a>Resumo

Os dashboards fornecem uma ferramenta flexível para gerir diversos aspetos dos serviços do Azure através do Portal. Facilitam a monitorização do estado dos seus serviços. Como são partilháveis, ajudam a garantir que todas as pessoas na sua equipa veem os mesmos dados e o estado dos componentes críticos.