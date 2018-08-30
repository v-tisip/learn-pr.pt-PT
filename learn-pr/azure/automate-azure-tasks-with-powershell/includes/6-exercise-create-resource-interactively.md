Suponha que trabalha numa empresa que produz um conjunto de ferramentas de administração do Linux. A sua função é ajudar os potenciais clientes a experimentar o software antes de o comprarem. Uma vez que o software faz alterações a nível de raiz no sistema operativo, você decidiu criar uma VM do Linux para cada cliente de avaliação. Cria as VMs, conforme necessário, e elimina-as no final da subscrição de avaliação. Dessa forma, cada cliente começa com uma versão limpa do sistema operativo. 

Para manter estas VMs separadas das VMs que a sua empresa utiliza para testes internos, vai criar um grupo de recursos dedicado para as alojar. Só precisa de um grupo de recursos, por isso, utilizar o Azure PowerShell no modo interativo é uma opção razoável para esta tarefa.

## <a name="steps-to-create-a-resource-group"></a>Passos para criar um grupo de recursos

1. Inicie o PowerShell.

1. Importe o módulo para a sessão atual para que tenha acesso aos cmdlets do Azure.

   ```powershell
   Import-Module AzureRM
   ```

1. Ligue-se ao Azure com o comando mostrado abaixo. Depois de introduzir o comando, autentique-se ao fornecer as credenciais do Azure.

   ```powershell
   Connect-AzureRmAccount
   ```

1. Crie um grupo de recursos.

    ```powershell
    New-AzureRmResourceGroup -Name "TrialsResourceGroup" -Location "East US"
    ```

1. Verifique se o grupo de recursos foi criado com êxito.

    ```powershell
    Get-AzureRmResource | Format-Table
    ```
Outra forma de verificar se o grupo de recursos foi criado com êxito é utilizar o Portal do Azure. Para tal, inicie sessão no Portal e navegue para a secção **Grupos de Recursos** (ver abaixo). O novo grupo de recursos deverá ser apresentado na lista.

![Utilizar o Portal para Listar os Grupos de Recursos](../media-drafts/6-listing-resource-groups.png)

## <a name="summary"></a>Resumo
Este exercício mostra um padrão comum para uma sessão interativa do PowerShell. Utilizou um cmdlet padrão para importar o módulo AzureRM e, em seguida, os cmdlets do Azure PowerShell para executar uma tarefa específica. Agora tem um grupo de recursos na sua subscrição e está pronto para criar VMs.