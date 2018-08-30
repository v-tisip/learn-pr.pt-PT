Neste exercício, vai continuar com o exemplo de uma empresa que cria ferramentas de administração do Linux. Lembre-se de que planeia utilizar VMs do Linux para permitir aos potenciais clientes testar o seu software. Tem um grupo de recursos pronto e agora chegou a altura de criar as VMs.

A sua empresa tem um stand numa grande feira sobre Linux. Planeia uma área de demonstração com três terminais cada ligados a uma VM do Linux separada. No final de cada dia, quer eliminar as VMs e recriá-las, para que recomecem do zero todas as manhãs. Criar as VMs manualmente depois do trabalho quando está cansado seria propenso a erros. Quer escrever um script do PowerShell para automatizar o processo de criação das VMs.

## <a name="write-a-script-that-creates-virtual-machines"></a>Escrever um script que cria Máquinas Virtuais

Siga estes passos para escrever o script:

1. Crie um novo ficheiro de texto chamado **ConferenceDailyReset.ps1**.

2. Capture o parâmetro numa variável:

    ```powershell
    param([string]$resourceGroup)
    ```

3. Autentique no Azure com as suas credenciais:

    ```powershell
    Connect-AzureRmAccount
    ```

4. Solicite um nome de utilizador e uma palavra-passe para a conta de administrador da VM e capture o resultado numa variável:

    ```powershell
    $adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."
    ```

5. Crie um ciclo que seja executado três vezes:

    ```powershell
    For ($i = 1; $i -le 3; $i++) 
    {

    }
    ```

6. No corpo do ciclo, crie um nome para cada VM e armazene-o numa variável:

    ```powershell
    $vmName = "ConferenceDemo" + $i
    ```

7. Em seguida, crie uma VM com a variável `$vmName`:

   ```powershell
   New-AzureRmVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Location "East US" -Image UbuntuLTS
   ```

8. Guarde o ficheiro.

O script completo deve ter o seguinte aspeto:

```powershell
param([string]$resourceGroup)

$adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."

Connect-AzureRmAccount

For ($i = 1; $i -le 3; $i++)
{
    $vmName = "ConferenceDemo" + $i

    New-AzureRmVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Location "East US" -Image UbuntuLTS
}
```

## <a name="execute-the-script"></a>Executar o script

Inicie o PowerShell e altere o diretório onde guardou o ficheiro de script. Para executar o script, execute o seguinte comando:

```powershell
.\ConferenceDailyReset.ps1 TrialsResourceGroup
```

O script pode demorar alguns minutos a ser concluído. Quando estiver concluído, certifique-se de que foi executado com êxito:

1. Num browser, inicie sessão no portal do Azure.
2. Na navegação à esquerda, clique em **Grupos de Recursos**.
3. Na lista de grupos de recursos, clique em **TrialsResourceGroup**. Na lista de recursos, deverá ver as VMs recentemente criadas e os recursos associados.

## <a name="summary"></a>Resumo
Escreveu um script que automatizou a criação de três VMs no grupo de recursos indicado por um parâmetro de script. O script é curto e simples, mas automatiza um processo que levaria muito tempo a ser concluído manualmente com o portal.