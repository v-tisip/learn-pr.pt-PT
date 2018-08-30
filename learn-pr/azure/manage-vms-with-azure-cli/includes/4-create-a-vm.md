<span data-ttu-id="0846b-101">A CLI do Azure inclui o comando `vm` para trabalhar com máquinas virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="0846b-101">The Azure CLI includes the `vm` command to work with virtual machines in Azure.</span></span> <span data-ttu-id="0846b-102">Podemos fornecer vários subcomandos para fazer tarefas específicas.</span><span class="sxs-lookup"><span data-stu-id="0846b-102">We can supply several subcommands to do specific tasks.</span></span> <span data-ttu-id="0846b-103">Os mais comuns incluem:</span><span class="sxs-lookup"><span data-stu-id="0846b-103">The most common include:</span></span>

| <span data-ttu-id="0846b-104">Subcomando</span><span class="sxs-lookup"><span data-stu-id="0846b-104">Sub-command</span></span> | <span data-ttu-id="0846b-105">Descrição</span><span class="sxs-lookup"><span data-stu-id="0846b-105">Description</span></span> |
|-------------|-------------|
| `create`    | <span data-ttu-id="0846b-106">Criar uma máquina virtual nova</span><span class="sxs-lookup"><span data-stu-id="0846b-106">Create a new virtual machine</span></span> |
| `deallocate` | <span data-ttu-id="0846b-107">Desalocar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="0846b-107">Deallocate a virtual machine</span></span> |
| `delete` | <span data-ttu-id="0846b-108">Eliminar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="0846b-108">Delete a virtual machine</span></span> |
| `list` | <span data-ttu-id="0846b-109">Listar as máquinas virtuais criadas na subscrição</span><span class="sxs-lookup"><span data-stu-id="0846b-109">List the created virtual machines in your subscription</span></span> |
| `open-port` | <span data-ttu-id="0846b-110">Abrir uma porta de rede específica para o tráfego de entrada</span><span class="sxs-lookup"><span data-stu-id="0846b-110">Open a specific network port for inbound traffic</span></span> |
| `restart` | <span data-ttu-id="0846b-111">Reiniciar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="0846b-111">Restart a virtual machine</span></span> |
| `show` | <span data-ttu-id="0846b-112">Obter os detalhes de uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="0846b-112">Get the details for a virtual machine</span></span> |
| `start` | <span data-ttu-id="0846b-113">Iniciar uma máquina virtual parada</span><span class="sxs-lookup"><span data-stu-id="0846b-113">Start a stopped virtual machine</span></span> |
| `stop` | <span data-ttu-id="0846b-114">Parar uma máquina virtual em execução</span><span class="sxs-lookup"><span data-stu-id="0846b-114">Stop a running virtual machine</span></span> |
| `update` | <span data-ttu-id="0846b-115">Atualizar uma propriedade de uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="0846b-115">Update a property of a virtual machine</span></span> |

> [!NOTE]
> <span data-ttu-id="0846b-116">Para obter uma lista completa de comandos, pode ver a [documentação de referência da CLI do Azure](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest).</span><span class="sxs-lookup"><span data-stu-id="0846b-116">For a complete list of commands, you can check the [Azure CLI reference documentation](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest).</span></span>

<span data-ttu-id="0846b-117">Vamos começar com o primeiro comando: `az vm create`.</span><span class="sxs-lookup"><span data-stu-id="0846b-117">Let's start with the first one: `az vm create`.</span></span> <span data-ttu-id="0846b-118">Este comando é utilizado para criar uma máquina virtual num grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0846b-118">This command is used to create a virtual machine in a resource group.</span></span> <span data-ttu-id="0846b-119">Existem vários parâmetros que pode passar para configurar todos os aspetos da nova VM.</span><span class="sxs-lookup"><span data-stu-id="0846b-119">There are several parameters you can pass to configure all the aspects of the new VM.</span></span> <span data-ttu-id="0846b-120">Tem de indicar os três parâmetros seguintes:</span><span class="sxs-lookup"><span data-stu-id="0846b-120">The three parameters that must be supplied are:</span></span>

| <span data-ttu-id="0846b-121">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="0846b-121">Parameter</span></span> | <span data-ttu-id="0846b-122">Descrição</span><span class="sxs-lookup"><span data-stu-id="0846b-122">Description</span></span> |
|-----------|-------------|
| `resource-group` | <span data-ttu-id="0846b-123">O grupo de recursos proprietário da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="0846b-123">The resource group that will own the virtual machine</span></span> |
| `name` | <span data-ttu-id="0846b-124">O nome da máquina virtual – deve ser exclusivo no grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="0846b-124">The name of the virtual machine - must be unique within the resource group</span></span> |
| `image` | <span data-ttu-id="0846b-125">A imagem do sistema operativo a utilizar para criar a VM</span><span class="sxs-lookup"><span data-stu-id="0846b-125">The operating system image to use to create the VM</span></span> |

<span data-ttu-id="0846b-126">Além disso, é útil adicionar o sinalizador `--verbose` para ver o progresso enquanto a VM está a ser criada.</span><span class="sxs-lookup"><span data-stu-id="0846b-126">In addition, it's helpful to add the `--verbose` flag to see progress while the VM is being created.</span></span> 

## <a name="create-a-linux-virtual-machine"></a><span data-ttu-id="0846b-127">Criar uma máquina virtual do Linux</span><span class="sxs-lookup"><span data-stu-id="0846b-127">Create a Linux virtual machine</span></span>

<span data-ttu-id="0846b-128">Vamos criar uma nova máquina virtual do Linux.</span><span class="sxs-lookup"><span data-stu-id="0846b-128">Let's create a new Linux virtual machine.</span></span> <span data-ttu-id="0846b-129">Execute o seguinte comando no Azure Cloud Shell:</span><span class="sxs-lookup"><span data-stu-id="0846b-129">Execute the following command in Azure Cloud Shell:</span></span>

```azurecli
az vm create --resource-group ExerciseResources --name SampleVM --image Debian --admin-username aldis --generate-ssh-keys --verbose 
```

<span data-ttu-id="0846b-130">Este comando cria uma nova máquina virtual Linux **Debian** com o nome `SampleVM`.</span><span class="sxs-lookup"><span data-stu-id="0846b-130">This command will create a new **Debian** Linux virtual machine with the name `SampleVM`.</span></span> <span data-ttu-id="0846b-131">Tenha em atenção que a ferramenta de CLI do Azure está bloqueada enquanto a VM está a ser criada.</span><span class="sxs-lookup"><span data-stu-id="0846b-131">Notice that the Azure CLI tool is blocked while the VM is being created.</span></span> <span data-ttu-id="0846b-132">Se preferir não esperar, poderá utilizar a opção `--no-wait` para informar a ferramenta de CLI do Azure para ficar ativa imediatamente, por exemplo, se estiver a executar o comando num script.</span><span class="sxs-lookup"><span data-stu-id="0846b-132">If you would prefer not to wait, you can use the `--no-wait` option to tell the Azure CLI tool to return immediately, for example if you're executing the command in a script.</span></span> <span data-ttu-id="0846b-133">Posteriormente no script, utilize o comando `azure vm wait --name [vm-name]` para aguardar a conclusão da criação da VM.</span><span class="sxs-lookup"><span data-stu-id="0846b-133">Later in the script, use the `azure vm wait --name [vm-name]` command to wait for the VM to finish being created.</span></span>

<span data-ttu-id="0846b-134">Se examinar as respostas verbosas, também verá que o nome `SampleVM` é utilizado como nome de várias dependências da VM.</span><span class="sxs-lookup"><span data-stu-id="0846b-134">If you look at the verbose responses, you will also see that the `SampleVM` name is used to name various dependencies for the VM.</span></span>

```
Succeeded: SampleVMNSG (Microsoft.Network/networkSecurityGroups)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMPublicIP (Microsoft.Network/publicIPAddresses)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMVNET (Microsoft.Network/virtualNetworks)
Accepted: vm_deploy_vzKnQDyyq48yPUO4VrSDfFIi81vHKZ9g (Microsoft.Resources/deployments)
```

<span data-ttu-id="0846b-135">Pode substituir estes nomes de recursos gerados automaticamente com os parâmetros opcionais para `vm create`, tais como `--vnet-name` e `--public-ip-address-dns-name`.</span><span class="sxs-lookup"><span data-stu-id="0846b-135">You can override these auto-generated resource names using optional parameters to `vm create`, such as `--vnet-name` and `--public-ip-address-dns-name`.</span></span>

<span data-ttu-id="0846b-136">Tenha em atenção que estamos a especificar o nome da conta de administrador através do sinalizador `admin-username` para ser “aldis”.</span><span class="sxs-lookup"><span data-stu-id="0846b-136">Notice that we are specifying the admin account name through the `admin-username` flag to be "aldis".</span></span> <span data-ttu-id="0846b-137">Se o omitir, o comando `vm create` utilizará o seu _nome de utilizador atual_.</span><span class="sxs-lookup"><span data-stu-id="0846b-137">If you omit this, the `vm create` command will use your _current user name_.</span></span> <span data-ttu-id="0846b-138">Uma vez que as regras para os nomes de conta são diferentes para cada sistema operativo, é mais seguro indicar um nome específico.</span><span class="sxs-lookup"><span data-stu-id="0846b-138">Since the rules for account names are different for each OS, it's safer to specify a specific name.</span></span> <span data-ttu-id="0846b-139">Os nomes comuns, como “raiz” e “admin” não são permitidos para a maioria das imagens.</span><span class="sxs-lookup"><span data-stu-id="0846b-139">Common names such as "root" and "admin" are not allowed for most images.</span></span>

<span data-ttu-id="0846b-140">Estamos também a utilizar o sinalizador `generate-ssh-keys`.</span><span class="sxs-lookup"><span data-stu-id="0846b-140">We are also using the `generate-ssh-keys` flag.</span></span> <span data-ttu-id="0846b-141">Este parâmetro é utilizado para as distribuições Linux e cria um par de chaves de segurança, pelo que podemos usar a ferramenta `ssh` para aceder remotamente à máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0846b-141">This parameter is used for Linux distributions and creates a pair of security keys so we can use the `ssh` tool to access the virtual machine remotely.</span></span> <span data-ttu-id="0846b-142">Os dois ficheiros são colocados na pasta `.ssh` no computador e na VM.</span><span class="sxs-lookup"><span data-stu-id="0846b-142">The two files are placed into the `.ssh` folder on your machine and in the VM.</span></span> <span data-ttu-id="0846b-143">Se já tiver uma chave SSH com o nome `id_rsa` na pasta de destino, esta será usada em vez de gerar uma chave nova.</span><span class="sxs-lookup"><span data-stu-id="0846b-143">If you already have an SSH key named `id_rsa` in the target folder, then it will be used rather than having a new key generated.</span></span>

<span data-ttu-id="0846b-144">Após a conclusão da criação da VM, obterá uma resposta JSON, que inclui o estado atual da máquina virtual e os endereços IP públicos e privados atribuídos pelo Azure:</span><span class="sxs-lookup"><span data-stu-id="0846b-144">Once it finishes creating the VM, you will get a JSON response which includes the current state of the virtual machine and its public and private IP addresses assigned by Azure:</span></span>

```json
{
  "fqdns": "",
  "id": "/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources/providers/Microsoft.Compute/virtualMachines/SampleVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-1A-D9-74",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "168.61.54.62",
  "resourceGroup": "ExerciseResources",
  "zones": ""
}
```

