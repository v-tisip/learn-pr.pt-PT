Neste exercício, vai utilizar o cliente RDP para ligar à VM do Windows que criou na unidade anterior. Pode ligar ao transferir e executar um ficheiro RDP a partir do portal do Azure. Este ficheiro RDP vai ter:

* O endereço IP público da VM.
* O número da porta.

## <a name="motivation"></a>Motivação

A partir do cenário do nosso exercício, é agora um estudante e quer aprender sobre adicionar funções e funcionalidades a um computador do Windows Server. No entanto, o seu administrador de rede não quer que faça isto num computador físico na rede, além de os computadores da escola terem más especificações para executar o Windows Hyper-V. O Azure oferece a solução perfeita.

## <a name="configure-network-and-public-ip-address-settings"></a>Configurar a rede e as definições de endereço IP público

1. No portal do Azure, certifique-se de que o painel para a máquina virtual que criou mais cedo está aberto. Pode encontrar o painel sob **Todos os Recursos** se precisar de abri-lo.

1. Vá para a secção de **Redes**. A parte superior desta secção tem ligações à sub-rede virtual e ao endereço IP dinâmico que foi criado juntamente com a nossa VM desde que utilizámos as predefinições. Se quiséssemos alterar essas ligações, seguiríamos essas ligações (por exemplo, a alteração para um endereço IP estático).

1. Clique em **Adicionar regra de porta de entrada**.

1. Na parte superior da caixa de diálogo **Adicionar regra de segurança de entrada**, clique em **básica**.

1. Em **Serviço**, selecione **RDP** e, em seguida, clique em **Adicionar**.

## <a name="connect-to-the-vm-by-using-rdp"></a>Ligar à VM através de RDP

Para transferir o ficheiro de RDP e ligar à VM, realize os passos seguintes.

### <a name="download-the-rdp-file"></a>Transferir o ficheiro RDP

1. Na secção do painel da máquina virtual **Descrição geral**, clique em **Ligar**.

1. No painel **Ligar a máquina virtual**, repare nas definições de **Endereço IP** e **Número de porta** e clique em **Transferir Ficheiro RDP**.

1. No seu browser, clique em **Abrir** ou **Executar** para abrir o ficheiro RDP.

### <a name="connect-to-the-windows-vm"></a>Ligue-se à VM do Windows

1. Na caixa de diálogo **Ligação de Ambiente de Trabalho Remoto**, aponte o aviso de segurança e no endereço IP do computador remoto e clique em **Ligar**.

1. Na caixa de diálogo **Segurança do Windows**, introduza o seu nome de utilizador e palavra-passe que utilizou nos passos 6 e 7.

1. Na segunda caixa de diálogo **Ligação de Ambiente de Trabalho Remoto**, repare nos erros de certificado e clique em **Sim**.

   > [!Note]
   > A área de trabalho da máquina virtual demora um pouco a aparecer. Este efeito deve-se por a imagem B1 estar subespecificada. Pode receber uma mensagem sobre a alocação de memória baixa.

1. Na caixa de diálogo de **Redes**, clique em **Não**.

### <a name="resize-the-vm-in-the-azure-portal"></a>Redimensione a VM no portal do Azure

1. Regresse ao portal do Azure. Na página de propriedades da máquina virtual, em **Definições**, clique em **Tamanho**.

1. Clique em **D2s_v3** (2 vCPUs, 8 GB de RAM) e, em seguida, clique em **Selecionar**. Vai ser apresentada uma mensagem de redimensionamento de máquina virtual. A VM na janela RDP também vai fechar.

1. Regresse ao portal do Azure. No painel do lado esquerdo, clique em **Máquinas virtuais**.

1. Em **Máquinas virtuais**, aguarde até que a sua VM mostre um estado **Em execução**. Pode ter de clicar em **Atualizar**.

1. Clique no nome da máquina virtual e em seguida, em **Configurações**, clique em **Tamanho**. Tenha em atenção que o tamanho da VM está agora definido como **D2s_v3**.

### <a name="reconnect-to-the-resized-vm"></a>Volte a ligar à VM redimensionada

1. Clique em **Máquinas virtuais** e então na sua VM. Repare que o valor de **Endereço IP Público** foi provavelmente alterado. Clique em **Ligar** e então em **Executar** ou **Abrir** no seu browser.

1. Na caixa de diálogo **Ligação de Ambiente de Trabalho Remoto**, aponte o aviso de segurança e no endereço IP do computador remoto e clique em **Ligar**.

1. Na caixa de diálogo **Segurança do Windows**, introduza o seu nome de utilizador e palavra-passe que utilizou nos passos 6 e 7.

1. Na segunda caixa de diálogo **Ligação de Ambiente de Trabalho Remoto**, repare nos erros de certificado e clique em **Sim**. Repare no quanto mais responsiva está a máquina virtual no processo de início de sessão.

1. Clique duas vezes na barra de tarefas e clique em **Gestor de Tarefas**.

1. Na janela de **Gestor de Tarefas**, clique em **Mais detalhes**.

1. Clique no separador **Desempenho**. Tenha em atenção a memória total disponível de 8 GB, dos quais cerca de 1,2 GB vão estar em utilização. Fechar o **Gestor de Tarefas**.

## <a name="summary"></a>Resumo

Ligou a uma VM do Windows com o RDP. Com o acesso à IU de Ambiente de Trabalho, pode administrar esta VM como faria com qualquer computador Windows.
