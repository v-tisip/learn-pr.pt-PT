<span data-ttu-id="24f84-101">Uma das principais tarefas que vai querer efetuar em máquinas virtuais em execução é iniciá-las e pará-las.</span><span class="sxs-lookup"><span data-stu-id="24f84-101">One of the main tasks you'll want to do to running virtual machines is to start and stop them.</span></span>

## <a name="stopping-a-vm"></a><span data-ttu-id="24f84-102">Parar uma VM</span><span class="sxs-lookup"><span data-stu-id="24f84-102">Stopping a VM</span></span>

<span data-ttu-id="24f84-103">Podemos parar uma VM em execução com o comando `vm stop`.</span><span class="sxs-lookup"><span data-stu-id="24f84-103">We can stop a running VM with the `vm stop` command.</span></span> <span data-ttu-id="24f84-104">Tem de transmitir o nome e o grupo de recursos, ou o ID exclusivo para a VM:</span><span class="sxs-lookup"><span data-stu-id="24f84-104">You must pass the name and resource group, or the unique ID for the VM:</span></span>

```azurecli
az vm stop -n SampleVM -g ExerciseResources
```

<span data-ttu-id="24f84-105">Podemos verificar se foi parada ao tentar enviar um ping para o endereço IP público, através de `ssh` ou do comando `vm get-instance-view`.</span><span class="sxs-lookup"><span data-stu-id="24f84-105">We can verify it has stopped by attempting to ping the public IP address, using `ssh`, or through the `vm get-instance-view` command.</span></span> <span data-ttu-id="24f84-106">Esta abordagem final devolve os mesmos dados básicos que `vm show`, mas inclui detalhes sobre a própria instância.</span><span class="sxs-lookup"><span data-stu-id="24f84-106">This final approach returns the same basic data as `vm show` but includes details about the instance itself.</span></span> <span data-ttu-id="24f84-107">Experimente escrever o seguinte comando no Azure Cloud Shell para ver o estado de execução atual da sua VM:</span><span class="sxs-lookup"><span data-stu-id="24f84-107">Try typing the following command into Azure Cloud Shell to see the current running state of your VM:</span></span>

```azurecli
az vm get-instance-view -n SampleVM -g ExerciseResources --query "instanceView.statuses[?starts_with(code, 'PowerState/') == `true`].displayStatus" -o tsv
```

<span data-ttu-id="24f84-108">Este comando deverá devolver `VM stopped` como resultado.</span><span class="sxs-lookup"><span data-stu-id="24f84-108">This command should return `VM stopped` as the result.</span></span>

## <a name="starting-a-vm"></a><span data-ttu-id="24f84-109">Iniciar uma VM</span><span class="sxs-lookup"><span data-stu-id="24f84-109">Starting a VM</span></span>

<span data-ttu-id="24f84-110">Podemos fazer o inverso através do comando `vm start`.</span><span class="sxs-lookup"><span data-stu-id="24f84-110">We can do the reverse through the `vm start` command.</span></span>

```azurecli
az vm start -n SampleVM -g ExerciseResources
```

<span data-ttu-id="24f84-111">Este comando irá iniciar uma VM parada.</span><span class="sxs-lookup"><span data-stu-id="24f84-111">This command will start a stopped VM.</span></span> <span data-ttu-id="24f84-112">Podemos verificá-lo através da consulta `vm get-instance-view`, que agora deverá devolver `VM running`.</span><span class="sxs-lookup"><span data-stu-id="24f84-112">We can verify it through the `vm get-instance-view` query, which should now return `VM running`.</span></span>

## <a name="restarting-a-vm"></a><span data-ttu-id="24f84-113">Reiniciar uma VM</span><span class="sxs-lookup"><span data-stu-id="24f84-113">Restarting a VM</span></span>

<span data-ttu-id="24f84-114">Por fim, podemos reiniciar uma VM se tivermos feito alterações que exijam um reinício através do comando `vm restart`.</span><span class="sxs-lookup"><span data-stu-id="24f84-114">Finally, we can restart a VM if we have made changes that require a reboot using the `vm restart` command.</span></span> <span data-ttu-id="24f84-115">Pode adicionar o sinalizador `--no-wait` se quiser que a CLI do Azure regresse imediatamente sem aguardar que a VM reinicie.</span><span class="sxs-lookup"><span data-stu-id="24f84-115">You can add the `--no-wait` flag if you want the Azure CLI to return immediately without waiting for the VM to reboot.</span></span>

