Uma das principais tarefas que vai querer efetuar em máquinas virtuais em execução é iniciá-las e pará-las.

## <a name="stopping-a-vm"></a>Parar uma VM

Podemos parar uma VM em execução com o comando `vm stop`. Tem de transmitir o nome e o grupo de recursos, ou o ID exclusivo para a VM:

```azurecli
az vm stop -n SampleVM -g ExerciseResources
```

Podemos verificar se foi parada ao tentar enviar um ping para o endereço IP público, através de `ssh` ou do comando `vm get-instance-view`. Esta abordagem final devolve os mesmos dados básicos que `vm show`, mas inclui detalhes sobre a própria instância. Experimente escrever o seguinte comando no Azure Cloud Shell para ver o estado de execução atual da sua VM:

```azurecli
az vm get-instance-view -n SampleVM -g ExerciseResources --query "instanceView.statuses[?starts_with(code, 'PowerState/') == `true`].displayStatus" -o tsv
```

Este comando deverá devolver `VM stopped` como resultado.

## <a name="starting-a-vm"></a>Iniciar uma VM

Podemos fazer o inverso através do comando `vm start`.

```azurecli
az vm start -n SampleVM -g ExerciseResources
```

Este comando irá iniciar uma VM parada. Podemos verificá-lo através da consulta `vm get-instance-view`, que agora deverá devolver `VM running`.

## <a name="restarting-a-vm"></a>Reiniciar uma VM

Por fim, podemos reiniciar uma VM se tivermos feito alterações que exijam um reinício através do comando `vm restart`. Pode adicionar o sinalizador `--no-wait` se quiser que a CLI do Azure regresse imediatamente sem aguardar que a VM reinicie.

