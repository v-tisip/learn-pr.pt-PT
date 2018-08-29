<span data-ttu-id="2f5be-101">O nosso objetivo é criar uma nova máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="2f5be-101">Our goal is to create a new Azure virtual machine.</span></span> <span data-ttu-id="2f5be-102">Vamos precisar de fornecer várias informações para identificar a localização do recurso, o SO a utilizar e a configuração de hardware necessária para a VM.</span><span class="sxs-lookup"><span data-stu-id="2f5be-102">We'll need to supply several pieces of information to identify the resource location, OS to use, and the hardware configuration needed for the VM.</span></span> <span data-ttu-id="2f5be-103">Vamos começar pelo **grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="2f5be-103">Let's start with the **resource group**.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="2f5be-104">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="2f5be-104">Create a resource group</span></span>

<span data-ttu-id="2f5be-105">O Azure utiliza _grupos de recursos_ para agrupar recursos relacionados, como máquinas virtuais e bases de dados.</span><span class="sxs-lookup"><span data-stu-id="2f5be-105">Azure uses _resource groups_ to group related resources such as virtual machines and databases together.</span></span> <span data-ttu-id="2f5be-106">O grupo de recursos também identifica uma localização específica (denominada "região") que vai decidir em que datacenter o recurso será colocado.</span><span class="sxs-lookup"><span data-stu-id="2f5be-106">The resource group also identifies a specific location (called a "region") which will decide what data center the resource is placed into.</span></span>

<span data-ttu-id="2f5be-107">Como estamos a experimentar, comece por criar um novo grupo de recursos com o nome `ExerciseResources` e coloque-o na região `eastus`.</span><span class="sxs-lookup"><span data-stu-id="2f5be-107">Since we're experimenting, start by creating a new resource group named `ExerciseResources` and place it into the `eastus` region.</span></span>

> [!NOTE]
> <span data-ttu-id="2f5be-108">Certifique-se de que utiliza este nome exato para o novo grupo de recursos, uma vez que o sistema Microsoft Learn irá procurar este nome de recurso mais tarde.</span><span class="sxs-lookup"><span data-stu-id="2f5be-108">Make sure to use this exact name for your new resource group, because the Microsoft Learn system will be looking for this resource name later.</span></span> 

<span data-ttu-id="2f5be-109">Escreva o seguinte comando da CLI do Azure no Azure Cloud Shell para criar o grupo de recursos na sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="2f5be-109">Type the following Azure CLI command in Azure Cloud Shell to create the resource group in your subscription.</span></span>

```azurecli
az group create --name ExerciseResources --location eastus
```

<span data-ttu-id="2f5be-110">Isto irá devolver um bloco JSON que indica que o grupo de recursos foi criado.</span><span class="sxs-lookup"><span data-stu-id="2f5be-110">This will return a JSON block indicating the resource group has been created.</span></span> <span data-ttu-id="2f5be-111">Deverá ter um aspeto semelhante a:</span><span class="sxs-lookup"><span data-stu-id="2f5be-111">It should look something like:</span></span>

```json
{
  "id": "/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources",
  "location": "eastus",
  "managedBy": null,
  "name": "ExerciseResources",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

<span data-ttu-id="2f5be-112">Repare que devolve o identificador exclusivo da subscrição, a localização e o nome como parte da resposta.</span><span class="sxs-lookup"><span data-stu-id="2f5be-112">Notice that it returns the subscription unique identifier, location, and name as part of the response.</span></span> <span data-ttu-id="2f5be-113">Pode utilizar estes dados para verificar se foi criado na subscrição e localização adequadas.</span><span class="sxs-lookup"><span data-stu-id="2f5be-113">You can use these to verify it got created in the proper subscription and location.</span></span>

<span data-ttu-id="2f5be-114">Agora que temos um grupo de recursos, vamos criar uma nova máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2f5be-114">Now that we have a resource group, let's create a new virtual machine.</span></span>