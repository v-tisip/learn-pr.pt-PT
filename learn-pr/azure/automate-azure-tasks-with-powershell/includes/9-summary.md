Neste módulo, escrevemos um script para automatizar a criação de múltiplas VMs. Ainda que o script seja relativamente curto, pode ver o seu potencial quando combina ciclos, variáveis e funções do PowerShell com cmdlets do Azure PowerShell.

O Azure PowerShell é uma boa opção de automatização para os administradores que tenham experiência com o PowerShell. A combinação de uma sintaxe clara e uma poderosa linguagem de script também justifica que considere esta opção mesmo que não esteja familiarizado com o PowerShell. Este nível de automatização de tarefas demoradas e propensas a erros deve ajudá-lo a reduzir o tempo administrativo e a aumentar a qualidade.

## <a name="cleanup"></a>Limpeza
As VMs aprovisionadas e em execução implicam custos na sua subscrição. Deve remover as VMs de que não precisa para evitar custos desnecessários. A maneira mais fácil de limpar a sua subscrição do Azure é remover o grupo de recursos associado. Esta ação também eliminará todas as VMs no grupo. E pode fazer isto no PowerShell! Quando tiver terminado, execute o seguinte cmdlet do Azure PowerShell:

```powershell
Remove-AzureRmResourceGroup -Name TrialsResourceGroup
```

Quando lhe for pedido que confirme a eliminação, responda **Sim**. Este comando pode demorar vários minutos a concluir.