<span data-ttu-id="280d4-101">Criou uma nova máquina virtual Linux, alterou o seu tamanho, parou-a e iniciou-a e atualizou a configuração com a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="280d4-101">You've created a new Linux virtual machine, changed its size, stopped and started it, and updated the configuration with the Azure CLI.</span></span>

## <a name="cleanup"></a><span data-ttu-id="280d4-102">Limpeza</span><span class="sxs-lookup"><span data-stu-id="280d4-102">Cleanup</span></span>

<span data-ttu-id="280d4-103">Agora que já não precisamos da VM, vamos eliminar os recursos.</span><span class="sxs-lookup"><span data-stu-id="280d4-103">Now that we're finished with the VM and no longer need it, let's delete the resources.</span></span> <span data-ttu-id="280d4-104">A limpeza é importante para os recursos de computação e de armazenamento que podem continuar a ser faturados na sua conta.</span><span class="sxs-lookup"><span data-stu-id="280d4-104">Cleanup is important for compute and storage resources that can continue to be billed against your account.</span></span> 

<span data-ttu-id="280d4-105">Pode eliminar recursos individuais com o comando `delete`, mas a forma mais fácil de remover tudo é com `az group delete`.</span><span class="sxs-lookup"><span data-stu-id="280d4-105">You can delete individual resources with the `delete` command, but the easiest way to remove everything is with `az group delete`.</span></span> <span data-ttu-id="280d4-106">Execute o seguinte comando na CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="280d4-106">Execute the following command in the Azure CLI:</span></span>

```azurecli
az group delete --name ExerciseResources --no-wait
```

<span data-ttu-id="280d4-107">Responda “sim” na linha de comandos, quando solicitado, ou utilize o parâmetro `--yes` para responder de forma automática ao prompt.</span><span class="sxs-lookup"><span data-stu-id="280d4-107">Answer "yes" to the prompt when shown, or use the `--yes` parameter to auto-answer the prompt.</span></span>

<span data-ttu-id="280d4-108">Este comando elimina todos os recursos associados ao grupo de recursos e desaloca-os garantidamente pela ordem correta.</span><span class="sxs-lookup"><span data-stu-id="280d4-108">This command deletes all of the resources associated with the resource group, and is guaranteed to deallocate them in the correct order.</span></span> <span data-ttu-id="280d4-109">O parâmetro `--no-wait` impede que a CLI do Azure bloqueie enquanto a eliminação está em curso.</span><span class="sxs-lookup"><span data-stu-id="280d4-109">The `--no-wait` parameter keeps the Azure CLI from blocking while the deletion takes place.</span></span> <span data-ttu-id="280d4-110">Deixe-a desativada para aguardar que os recursos sejam eliminados.</span><span class="sxs-lookup"><span data-stu-id="280d4-110">Leave it off to wait for the resources to be deleted.</span></span> <span data-ttu-id="280d4-111">Em alternativa, utilize o comando `az group wait -n ExerciseResources --deleted` posteriormente no script para aguardar que a eliminação chegue ao fim.</span><span class="sxs-lookup"><span data-stu-id="280d4-111">Or use the `az group wait -n ExerciseResources --deleted` command later in your script to wait for the deletion to finish.</span></span>


## <a name="further-reading"></a><span data-ttu-id="280d4-112">Leitura adicional</span><span class="sxs-lookup"><span data-stu-id="280d4-112">Further reading</span></span>

* [<span data-ttu-id="280d4-113">Descrição geral da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="280d4-113">Azure CLI overview</span></span>](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest)
* [<span data-ttu-id="280d4-114">Referência de comandos da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="280d4-114">Azure CLI command reference</span></span>](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest)
