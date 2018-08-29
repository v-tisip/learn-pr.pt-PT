Neste exercício, vai criar e configurar um dashboard personalizado.

## <a name="create-a-new-dashboard"></a>Criar um novo dashboard

1. No portal do Azure, clique no botão **Novo Dashboard**.

2. Na caixa que indica **O Meu Dashboard**, altere o nome para **Dashboard de Cliente**.

## <a name="add-and-configure-the-clock-tile"></a>Adicionar e configurar o mosaico de Relógio

1. Na galeria de mosaicos, arraste e largue o relógio na área de trabalho. Coloque-o na parte superior direita do espaço disponível.

2. No painel Editar Relógio, altere a Localização para **Hora do Pacífico (EUA e Canadá)**.

3. Em **Formato de hora**, clique em **24 horas**.

4. Clique em **Concluído**.

5. Repita os quatro passos acima, exceto selecionar **Hora do Leste (EUA e Canadá)**. Deve ter agora dois relógios, um com a hora na Costa Oeste e outro com a hora na Costa Leste.

## <a name="resize-a-tile"></a>Redimensionar um mosaico

1. No painel Galeria de Mosaicos, clique em **Todos os recursos** e, em seguida, largue o mosaico na parte superior esquerda da área de trabalho do novo dashboard.

2. Clique no mosaico, clique com o botão direito do rato nas reticências e clique em **6x6**.

3. Clique no canto cinzento na parte inferior direita do mosaico e redimensione o mosaico para 3,5 verticalmente por 6 horizontalmente. Tenha em atenção que quando largar o canto, será redimensionado para 4x6.

4. Na Galeria de Mosaicos, clique no mosaico **Grupos de Recursos** e arraste-o para a área de trabalho. Coloque-o por baixo do mosaico **Todos os recursos**.

5. Na Galeria de Mosaicos, clique no mosaico **Estado de Funcionamento do Serviço** e arraste-o para a área de trabalho. Coloque-o à direita do mosaico **Todos os recursos**.

6. Continue a adicionar os mosaicos seguintes e reorganize-os de acordo com:

    * Ajuda + Suporte
    * Tarefas Rápidas
    * Marketplace
    * Novidades

7. Quando tiver adicionado destes mosaicos, clique em **Personalização concluída**. Deverá ser apresentado o dashboard **Dashboard de Cliente**.

## <a name="clone-a-dashboard"></a>Clonar um dashboard

Quer agora criar um dashboard muito semelhante para outros clientes

1. Clique no botão **Clonar**.

2. Mude o nome do dashboard de **Clone do Dashboard de Cliente** para **Dashboard de Administração do Azure AD**.

3. No mosaico **Grupos de Recursos**, clique no ícone de lixo para eliminar este mosaico.

4. Na Galeria de Mosaicos, adicione os seguintes mosaicos:

    * Identidade da Organização
    * Utilizadores e Grupos
    * Resumo da Atividade do Utilizador
    * Bem-vindo ao Centro de Administração do Azure AD

5. Reposicione os mosaicos conforme necessário e, em seguida, clique em **Personalização concluída**.

## <a name="share-a-dashboard"></a>Partilhar um dashboard

Quer agora disponibilizar este dashboard para outros utilizadores. Para tal, execute os seguintes passos:

1. Certifique-se de que o Dashboard de Administração do Azure AD está selecionado e, em seguida, clique em **Partilhar**.

2. No painel **Partilha e controlo de acesso**, certifique-se de que a opção **Publicar no grupo de recursos "dashboards"** está selecionada.

3. Defina a **Localização** para uma adequada à sua região geográfica. Normalmente, este valor é predefinido para o seu datacenter mais próximo.

4. Clique em **Publicar** e, em seguida, feche o painel **Partilha + controlo de acesso**.

5. Clique em **Dashboard de Administração do Azure AD** e selecione **Dashboard de Cliente**.

6. Tenha em atenção que em **Todos os recursos**, apareceu um recurso de dashboard Partilhado e, em **Grupos de recursos**, também apareceu um grupo de recursos de dashboards.

7. Repita os passos 1 a 3 para partilhar o Dashboard de Cliente.

## <a name="edit-a-dashboard-file"></a>Editar um Ficheiro de Dashboard

Para mostrar como pode transferir e editar um ficheiro de dashboard, execute os seguintes passos:

1. Clique em **Transferir**.

2. Abra o Explorador do Windows e navegue para a pasta Transferências.

3. Localize o ficheiro **Customer Dashboard.json** e clique duas vezes no mesmo.

4. No editor de ficheiros, procure o texto "ClockPart"

5. Na primeira ocorrência de ClockPart, altere o valor rowSpan anterior para 1.

6. Na segunda ocorrência de ClockPart, altere também o valor rowSpan anterior para 1.

7. Na segunda ocorrência de Clockpart, altere o valor Y de 2 para 1.

8. Guarde o ficheiro Customer Dashboard.json e feche o editor de código.

9. No dashboard do Azure, clique em **Carregar**.

10. Na caixa de diálogo **Abrir**, navegue para a pasta Transferências e faça duplo clique em **Customer Dashboard.json**.

11. Tenha em atenção como os relógios foram redimensionados para uma linha acima e o relógio inferior foi movido uma linha para cima.

## <a name="select-a-shared-dashboard"></a>Selecionar um Dashboard Partilhado

Percebeu que não gosta dos relógios mais pequenos e quer voltar à versão partilhada anteriormente do Dashboard de Cliente. Pode fazê-lo ao editar o ficheiro e ao carregá-lo novamente ou ao aceder à versão partilhada. Para tal, execute os seguintes passos:

1. Clique na seta para baixo junto a **Dashboard de Cliente**.

2. Clique em **Procurar todos os dashboards**.

3. No painel **Todos os dashboards**, em **TIPO**, selecione **Dashboards partilhados**.

4. Clique em **Dashboard de Cliente**.

5. Feche o painel **Todos os dashboards**.

6. Tenha em atenção como os relógios voltaram ao tamanho original.

## <a name="switch-to-full-screen"></a>Mudar para Ecrã Inteiro

1. Clique na seta para baixo junto a **Dashboard de Cliente**. Tenha em atenção que não existe outro Dashboard de Cliente, sem o símbolo de partilhado junto ao mesmo. Clique na versão do Dashboard de Cliente e os relógios voltam a ficar pequenos.

2. Mude novamente para o Dashboard de Cliente partilhado.

3. Clique no botão **Ecrã Inteiro**. Tenha em atenção como todos os menus e barras do browser desapareceram.

4. Clique em **Sair do Ecrã Inteiro** para voltar ao ecrã normal.

## <a name="unshare-a-dashboard"></a>Anular a partilha de um dashboard

Se quiser impedir que um determinado dashboard partilhado esteja disponível para seleção, pode anular a respetiva partilha. Para anular a partilha de um dashboard, execute os seguintes passos:

1. Clique no botão **Anular partilha**. É apresentado o painel **Partilha + controlo de acesso**.

2. Clique no botão **Anular publicação**.

3. Na caixa de mensagem de confirmação, clique em **OK**.

4. Clique na seta para baixo junto a **Dashboard de Cliente**.

5. Clique em **Procurar todos os dashboards**.

6. No painel **Todos os dashboards**, em **TIPO**, selecione **Dashboards partilhados**.

7. Tenha em atenção que o Dashboard de Cliente já não aparece na lista de dashboards disponíveis.

8. Feche o painel "Todos os dashboards".

## <a name="delete-a-dashboard"></a>Eliminar um dashboard

1. Certifique-se de que o Dashboard de Administração do Azure AD está selecionado.

2. Clique no botão **Eliminar**.

3. Na caixa de mensagem **Confirmação**, selecione a caixa de verificação para confirmar que este dashboard vai deixar de estar visível e, em seguida, clique em **OK**.

## <a name="reset-a-dashboard"></a>Repor um dashboard

1. Certifique-se de que o Dashboard de Cliente está selecionado.

2. Clique em **Editar**.

3. Clique com o botão direito do rato na área de trabalho e clique em **Repor para o estado predefinido**.

4. Na caixa de mensagem **Repor dashboard para o estado predefinido**, clique em **Sim**.

5. Tenha em atenção como o Dashboard de Cliente foi reposto para os mosaicos predefinidos.

6. Clique em **Personalização concluída**.

7. Clique no seu nome na parte superior direita do Portal.

8. Clique em Terminar sessão.

9. Feche o browser.

## <a name="summary"></a>Resumo

Acabou de criar e editar dashboards, partilhou-os, alterou-os como ficheiros .JSON, anulou a partilha e, por fim, foram repostos para o estado predefinido. Já deve conseguir ver as ferramentas poderosas que os dashboards podem ser e como pode utilizá-los para criar interfaces eficientes para diferentes funções dentro de uma organização.