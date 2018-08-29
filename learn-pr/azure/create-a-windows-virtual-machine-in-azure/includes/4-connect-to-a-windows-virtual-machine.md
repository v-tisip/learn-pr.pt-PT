Como administrador de rede numa empresa de análise de dados, é responsável por ligar às máquinas virtuais no Azure e por verificar que estão corretamente configuradas. Efetua este procedimento através de um cliente do Protocolo do Ambiente de Trabalho Remoto para ligar à IU de ambiente de trabalho do Windows da VM.

## <a name="what-is-the-remote-desktop-protocol"></a>O que é o Protocolo do Ambiente de Trabalho Remoto?

O Protocolo do Ambiente de Trabalho Remoto (RDP) fornece conectividade remota à IU dos computadores baseados no Windows. O RDP permite-lhe iniciar sessão num computador Windows físico ou virtual remoto e controlá-lo como se estivesse sentado na consola.

> [!Note]
> O Windows Hyper-V no Windows Server 2016 e Windows 10 utiliza o RDP para ligar às máquinas virtuais em execução no hipervisor.

Uma ligação RDP permite-lhe realizar a grande maioria das operações que pode fazer a partir da consola de um computador físico, à exceção de algumas funções relacionadas com energia e hardware.

Uma ligação RDP requer um cliente RDP. A Microsoft fornece clientes RDP para os seguintes sistemas operativos:

* Windows
* iOS
* MacOS
* Android

Também existem clientes Linux de código-fonte aberto, como o Remmina, que lhe permitem ligar a um PC Windows a partir de uma distribuição do Ubuntu.

O Windows 10 inclui um cliente RDP.

![Cliente RDP do Windows](../images/2-rdp-client.PNG)

## <a name="what-functionality-does-an-rdp-connection-support"></a>Qual a funcionalidade suportada por uma ligação RDP?

Com uma ligação RDP, pode interagir com a IU. No entanto, também pode ligar a outros serviços no computador remoto. Estes serviços incluem:

* Ligações de impressoras que permitem ao computador remoto imprimir no seu dispositivo de impressão local.
* Reprodução de áudio, em que o áudio pode ser reproduzido no computador local ou no dispositivo remoto.
* Gravação de áudio, em que pode gravar áudio a partir do computador local e direcionar esse som para o dispositivo remoto.
* Portas, que pode redirecionar para as portas no computador local.
* Unidades, incluindo unidades de rede mapeadas, em que as unidades aparecem como ligadas ao computador remoto.
* Dispositivos de captura de vídeo, como câmaras Web integradas.
* Outros dispositivos plug-and-play suportados.

Nem todas estas funcionalidades são suportadas no Azure, uma vez que existem restrições relativamente aos ativos físicos que estão disponíveis nessa plataforma. Por exemplo, apenas impressoras de software podem ser redirecionadas através de uma ligação RDP a partir de uma VM alojada no Azure para os dispositivos de impressão do cliente.

## <a name="configure-network-settings-for-rdp-access-to-virtual-machines"></a>Configurar definições de rede para acesso RDP a máquinas virtuais

Podem ser efetuadas ligações às VMs do Azure de três formas:

1. Diretamente ao endereço IP público da VM.
2. Através de uma ligação de rede privada virtual (VPN).
3. Através de uma ligação ExpressRoute.

Um endereço IP público pode ser atribuído permanentemente ou dinâmico. Também tem de garantir que tem acesso ao endereço público da VM na porta 3389 (RDP). Esta disposição pode exigir negociação com a equipa que está a gerir a segurança da firewall da sua organização, como configurar uma regra para o endereço IP público da VM na porta 3389.

Os endereços IP públicos dinâmicos são reatribuídos sempre que a VM for reiniciada. Os endereços estáticos são persistentes, mas têm um custo superior.

Para ligar através de uma VPN, a rede local tem de ter uma ligação de VPN ativa ao Microsoft Azure.

A abordagem de ligação ExpressRoute gere a conectividade à VM. Esta abordagem também fornece a latência mais baixa e a ligação de largura de banda mais alta.

> [!Note]
> Independentemente da opção que utilizar para ligar ao Azure, tem de garantir que a máquina virtual é acessível por RDP, normalmente na porta 3389 predefinida. Pode configurar a VM para que possa ser acedida apenas a partir do seu próprio endereço IP cliente. Ligar a uma VM através da porta 3389 num endereço IP público só é recomendado para ambientes de teste. Em ambientes de produção, utilize a opção 2 ou 3.

## <a name="how-do-you-connect-to-a-vm-in-azure-using-rdp"></a>Como ligar a uma VM no Azure através de RDP?

Ligar a uma VM no Azure por RDP é um processo simples. No portal do Azure, aceda às propriedades da VM e, na parte superior, clique em **Ligar**. Esta ação transfere um ficheiro .RDP pré-configurado que o Windows abre em seguida no cliente RDP. Pode optar por ligar através do endereço IP público da VM no ficheiro RDP. Em alternativa, se estiver a ligar através de VPN ou ExpressRoute, pode selecionar o endereço IP interno. Também pode selecionar o número de porta para a ligação.

Se estiver a utilizar um endereço IP público estático para a VM, pode guardar o ficheiro .RDP no ambiente de trabalho. Se estiver a utilizar um endereço IP dinâmico, o ficheiro .RDP apenas permanece válido enquanto a VM estiver em execução. Se parar e reiniciar a VM, tem de transferir outro ficheiro .RDP.

> [!Note]
> Também pode introduzir o endereço IP público da VM no cliente RDP do Windows e clicar em **Ligar**.

Quando ligar, normalmente receberá dois avisos. Nomeadamente:

* Aviso do publicador: causado pelo ficheiro .RDP não estar assinado publicamente.
* Aviso do certificado: causado pelo certificado do computador não ser fidedigno.

Em ambientes de teste, estes avisos podem ser ignorados. Em ambientes de produção, o ficheiro .RDP pode ser assinado através do ficheiro RDPSIGN.EXE e do certificado do computador colocado no arquivo de **Autoridades de Certificação de Raiz Fidedigna** do cliente.

## <a name="summary"></a>Resumo

Agora, pode ligar a uma VM do Windows por RDP. No exercício seguinte, irá utilizar o RDP para ligar a uma VM e, em seguida, instalar uma função de servidor nesse computador.
