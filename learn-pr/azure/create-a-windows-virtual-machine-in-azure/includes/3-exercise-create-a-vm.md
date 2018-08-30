Neste exercício, vai criar uma máquina virtual do Windows no Azure.

## <a name="motivation"></a>Motivação

Vamos considerar um cenário alternativo para este exercício. Aqui, a sua organização é uma instituição de ensino que utiliza as máquinas virtuais do Windows para acelerar ambientes de teste em que os estudantes instalam aplicações Web, configurar domínios e explorar as funcionalidades e serviços do Windows sem afetar os computadores da instituição de ensino. Os professores ligam-se a estas VMs através do RDP e verificam o progresso dos alunos.

## <a name="create-a-windows-vm"></a>Criar uma VM do Windows

Para criar uma VM do Windows, execute os seguintes passos:

1. Inicie sessão no Azure através do [portal do Azure](https://portal.azure.com).

1. Clique em **Criar um recurso**, no canto superior esquerdo do portal do Azure.

1. Na **barra de pesquisa**, introduza **Windows Server 2016 Datacenter** e, em seguida, clique na ligação com o mesmo título.

### <a name="configure-the-vm-settings"></a>Configurar as definições da VM

1. Em **Noções básicas**, no campo **Nome**, introduza um nome para a VM, por exemplo, “VM_aluno”.

1. No campo **Tipo de Disco da VM**, clique no menu pendente para ver as opções. Verifique se **SSD** está selecionado.

1. No campo **Nome de utilizador**, introduza um nome de utilizador adequado para utilizar para iniciar sessão na VM.

1. No campo **Palavra-passe**, introduza uma palavra-passe que tenha, pelo menos, 12 carateres. Também tem de ter carateres em maiúsculas e minúsculas, números e carateres especiais.

1. Em **Grupo de recursos**, clique em **Criar nova**. Dê um nome ao grupo de recursos, por exemplo, “meuGRteste”.

1. Selecione uma localização adequada para a VM a ser criada e clique em **OK**.

### <a name="select-the-vm-image-size-and-options"></a>Selecionar as opções e o tamanho da imagem da VM

1. Na página **Escolher um tamanho**, clique na imagem **B1s** e, em seguida, em **Selecionar**.

   > [!Note] 
   > A imagem B1 tem apenas 1 GB de RAM e resultará em erros de memória quando iniciar sessão pela primeira vez. No entanto, pode redimensionar a imagem mais tarde como parte de um laboratório posterior.

1. Na página **Definições**, em **Selecionar Portas de Entrada Pública**, selecione **Nenhuma porta de entrada pública**. Vamos configurar o acesso do RDP posteriormente.

### <a name="finish-configuring-the-vm-and-create-the-image"></a>Concluir a configuração da VM e criar a imagem

1. Desloque-se para baixo e clique em **OK**.

1. Em **Criar**, verifique as definições que configurou. Na parte inferior, clique em **Criar**. O dashboard do Azure mostrará a VM que está a ser implementada. Este processo pode demorar vários minutos.

## <a name="summary"></a>Resumo

Acabou de criar uma máquina virtual do Windows Server adequada para os requisitos dos alunos e acessível a partir da rede da instituição de ensino. Na unidade seguinte, verá como se ligar e gerir essa VM através do RDP.
