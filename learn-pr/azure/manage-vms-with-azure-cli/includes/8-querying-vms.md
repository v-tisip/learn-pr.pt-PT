<span data-ttu-id="6863b-101">Agora que criou uma máquina virtual, podemos obter informações sobre a mesma através de outros comandos.</span><span class="sxs-lookup"><span data-stu-id="6863b-101">Now that a virtual machine has been created, we can get information about it through other commands.</span></span>

<span data-ttu-id="6863b-102">Comecemos com `vm list`.</span><span class="sxs-lookup"><span data-stu-id="6863b-102">Let's start with `vm list`.</span></span>

```azurecli
az vm list
```

<span data-ttu-id="6863b-103">Este comando irá devolver _todas_ as máquinas virtuais definidas nesta subscrição.</span><span class="sxs-lookup"><span data-stu-id="6863b-103">This command will return _all_ virtual machines defined in this subscription.</span></span> <span data-ttu-id="6863b-104">A saída pode ser filtrada para um grupo de recursos específico através do parâmetro `--resource-group`.</span><span class="sxs-lookup"><span data-stu-id="6863b-104">The output can be filtered to a specific resource group through the `--resource-group` parameter.</span></span> 

## <a name="output-types"></a><span data-ttu-id="6863b-105">Tipos de saída</span><span class="sxs-lookup"><span data-stu-id="6863b-105">Output types</span></span>
<span data-ttu-id="6863b-106">Tenha em atenção que o tipo de resposta predefinida para todos os comandos que fizemos até agora é um JSON.</span><span class="sxs-lookup"><span data-stu-id="6863b-106">Notice that the default response type for all the commands we've done so far is JSON.</span></span> <span data-ttu-id="6863b-107">Isto é ótimo para a criação de scripts - mas a maioria das pessoas acha mais difícil de ler.</span><span class="sxs-lookup"><span data-stu-id="6863b-107">This is great for scripting - but most people find it harder to read.</span></span> <span data-ttu-id="6863b-108">Pode alterar o estilo de saída para qualquer resposta através do sinalizador `--output`.</span><span class="sxs-lookup"><span data-stu-id="6863b-108">You can change the output style for any response through the `--output` flag.</span></span> <span data-ttu-id="6863b-109">Por exemplo, experimente o seguinte comando no Azure Cloud Shell para ver o estilo de saída diferente.</span><span class="sxs-lookup"><span data-stu-id="6863b-109">For example, try the following command in Azure Cloud Shell to see the different output style.</span></span>

```azurecli
az vm list --output table
```

<span data-ttu-id="6863b-110">Juntamente com `table`, pode especificar `json` (a predefinição), `jsonc` (JSON colorido) ou `tsv` (Valores Separados por Tabela).</span><span class="sxs-lookup"><span data-stu-id="6863b-110">Along with `table`, you can specify `json` (the default), `jsonc` (colorized JSON), or `tsv` (Table-Separated Values).</span></span> <span data-ttu-id="6863b-111">Experimente algumas variações com o comando acima para ver a diferença.</span><span class="sxs-lookup"><span data-stu-id="6863b-111">Try a few variations with the above command to see the difference.</span></span>

## <a name="getting-the-ip-address"></a><span data-ttu-id="6863b-112">Obter o endereço IP</span><span class="sxs-lookup"><span data-stu-id="6863b-112">Getting the IP address</span></span>

<span data-ttu-id="6863b-113">Outro comando útil é `vm list-ip-addresses`, que irá listar os endereços IP público e privado para uma VM.</span><span class="sxs-lookup"><span data-stu-id="6863b-113">Another useful command is `vm list-ip-addresses`, which will list the public and private IP addresses for a VM.</span></span> <span data-ttu-id="6863b-114">Se forem alterados ou não os capturar durante a criação, pode obtê-los em qualquer altura.</span><span class="sxs-lookup"><span data-stu-id="6863b-114">If they change, or you didn't capture them during creation, you can retrieve them at any time.</span></span>

```azurecli
az vm list-ip-addresses -n SampleVM -o table
```

<span data-ttu-id="6863b-115">Esta ação devolve:</span><span class="sxs-lookup"><span data-stu-id="6863b-115">This returns:</span></span>

```
VirtualMachine    PublicIPAddresses    PrivateIPAddresses
----------------  -------------------  --------------------
SampleVM          168.61.54.62         10.0.0.4
```

> [!NOTE]
> <span data-ttu-id="6863b-116">Tenha em atenção que estamos a utilizar uma sintaxe abreviada para o sinalizador `--output` como `-o`.</span><span class="sxs-lookup"><span data-stu-id="6863b-116">Notice that we are using a shorthand syntax for the `--output` flag as `-o`.</span></span> <span data-ttu-id="6863b-117">A maioria dos parâmetros para comandos da CLI do Azure podem ser reduzidos para um travessão único e uma letra.</span><span class="sxs-lookup"><span data-stu-id="6863b-117">Most parameters to Azure CLI commands can be shortened to a single dash and letter.</span></span> <span data-ttu-id="6863b-118">Por exemplo, `--name` pode ser reduzido para `-n` e `--resource-group` para `-g`.</span><span class="sxs-lookup"><span data-stu-id="6863b-118">For example, `--name` can be shortened to `-n` and `--resource-group` to `-g`.</span></span> <span data-ttu-id="6863b-119">Isto é útil para escrever, mas recomendamos que utilize o nome da opção completa em scripts para maior clareza.</span><span class="sxs-lookup"><span data-stu-id="6863b-119">This is handy for typing, but we recommend using the full option name in scripts for clarity.</span></span> <span data-ttu-id="6863b-120">Verifique a documentação para obter detalhes sobre cada comando.</span><span class="sxs-lookup"><span data-stu-id="6863b-120">Check the documentation for details on each command.</span></span>

## <a name="getting-vm-details"></a><span data-ttu-id="6863b-121">A obter detalhes da VM</span><span class="sxs-lookup"><span data-stu-id="6863b-121">Getting VM details</span></span>

<span data-ttu-id="6863b-122">Podemos obter informações mais detalhadas sobre uma máquina virtual específica pelo nome ou ID com o comando `vm show`.</span><span class="sxs-lookup"><span data-stu-id="6863b-122">We can get more detailed information about a specific virtual machine by name or ID using the `vm show` command.</span></span>

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM
```

<span data-ttu-id="6863b-123">Isto irá devolver um bloco JSON bastante grande com todos os tipos de informações sobre a VM, incluindo dispositivos de armazenamento anexados, interfaces de rede e todos os IDs de objeto para recursos a que a VM está ligada.</span><span class="sxs-lookup"><span data-stu-id="6863b-123">This will return a fairly large JSON block with all sorts of information about the VM, including attached storage devices, network interfaces, and all of the object IDs for resources that the VM is connected to.</span></span> <span data-ttu-id="6863b-124">Novamente, podemos alterar para um formato de tabela, mas isso omite quase todos os dados interessantes.</span><span class="sxs-lookup"><span data-stu-id="6863b-124">Again, we could change to a table format, but that omits almost all of the interesting data.</span></span> <span data-ttu-id="6863b-125">Em vez disso, podemos ativar para uma linguagem de consulta incorporada para JSON denominado [JMESPath](http://jmespath.org/).</span><span class="sxs-lookup"><span data-stu-id="6863b-125">Instead, we can turn to a built-in query language for JSON called [JMESPath](http://jmespath.org/).</span></span>

## <a name="adding-filters-to-queries-with-jmespath"></a><span data-ttu-id="6863b-126">Adicionar filtros a consultas com JMESPath</span><span class="sxs-lookup"><span data-stu-id="6863b-126">Adding filters to queries with JMESPath</span></span>

<span data-ttu-id="6863b-127">JMESPath é uma linguagem de consulta padrão do setor criada em torno de objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="6863b-127">JMESPath is an industry-standard query language built around JSON objects.</span></span> <span data-ttu-id="6863b-128">A consulta mais simples é especificar um _identificador_ que seleciona uma chave no objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="6863b-128">The simplest query is to specify an _identifier_ that selects a key in the JSON object.</span></span>

<span data-ttu-id="6863b-129">Por exemplo, dado o objeto:</span><span class="sxs-lookup"><span data-stu-id="6863b-129">For example, given the object:</span></span>

```json
{
  "people": [
    {
      "name": "Fred",
      "age": 28
    },
    {
      "name": "Barney",
      "age": 25
    },
    {
      "name": "Wilma",
      "age": 27
    }
  ]
}
```

<span data-ttu-id="6863b-130">Podemos utilizar a consulta `people` para devolver a matriz de valores para a matriz `people`.</span><span class="sxs-lookup"><span data-stu-id="6863b-130">We can use the query `people` to return the array of values for the `people` array.</span></span> <span data-ttu-id="6863b-131">Se queremos apenas _uma_ das pessoas, podemos utilizar um indexador.</span><span class="sxs-lookup"><span data-stu-id="6863b-131">If we just want _one_ of the people, we can use an indexer.</span></span> <span data-ttu-id="6863b-132">Por exemplo, `people[1]` iria devolver:</span><span class="sxs-lookup"><span data-stu-id="6863b-132">For example, `people[1]` would return:</span></span>

```json
{
    "name": "Barney",
    "age": 25
}
```

<span data-ttu-id="6863b-133">Também podemos adicionar qualificadores específicos que iriam devolver apenas os objetos `Fred` e `Wilma`.</span><span class="sxs-lookup"><span data-stu-id="6863b-133">We can also add specific qualifiers that would return just the `Fred` and `Wilma` objects.</span></span> 

```json
[
  {
    "name": "Fred",
    "age": 28
  },
  {
    "name": "Wilma",
    "age": 27
  }
]
```

<span data-ttu-id="6863b-134">Por fim, pode restringir os resultados ao adicionar uma seleção: `people[?age > '25'].[name]` que devolve apenas os nomes:</span><span class="sxs-lookup"><span data-stu-id="6863b-134">Finally, we can constrain the results by adding a select: `people[?age > '25'].[name]` that returns just the names:</span></span>

```json
[
  [
    "Fred"
  ],
  [
    "Wilma"
  ]
]
```

<span data-ttu-id="6863b-135">JMESQuery tem várias outras funcionalidades interessantes da consulta.</span><span class="sxs-lookup"><span data-stu-id="6863b-135">JMESQuery has several other interesting query features.</span></span> <span data-ttu-id="6863b-136">Quando tiver tempo, veja o [tutorial online](http://jmespath.org/tutorial.html) disponível no site [JMESPath.org](http://jmespath.org/).</span><span class="sxs-lookup"><span data-stu-id="6863b-136">When you have time, check out the [online tutorial](http://jmespath.org/tutorial.html) available on the [JMESPath.org](http://jmespath.org/) site.</span></span>

## <a name="filtering-our-azure-cli-queries"></a><span data-ttu-id="6863b-137">Filtrar as nossas consultas da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="6863b-137">Filtering our Azure CLI queries</span></span>

<span data-ttu-id="6863b-138">Com uma compreensão básica das consultas JMES, podemos adicionar filtros aos dados devolvidos por consultas, como o comando `vm show`.</span><span class="sxs-lookup"><span data-stu-id="6863b-138">With a basic understanding of JMES queries, we can add filers to the data being returned by queries like the `vm show` command.</span></span> <span data-ttu-id="6863b-139">Por exemplo, podemos recuperar o nome de utilizador administrador:</span><span class="sxs-lookup"><span data-stu-id="6863b-139">For example, we can retrieve the admin user name:</span></span>

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "osProfile.adminUsername"
```

<span data-ttu-id="6863b-140">Podemos obter o tamanho atribuído à nossa VM:</span><span class="sxs-lookup"><span data-stu-id="6863b-140">We can get the size assigned to our VM:</span></span>

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query hardwareProfile.vmSize
```

<span data-ttu-id="6863b-141">Ou para obter todos os IDs para as interfaces de rede, pode utilizar a consulta:</span><span class="sxs-lookup"><span data-stu-id="6863b-141">Or to retrieve all the IDs for your network interfaces, you can use the query:</span></span>

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "networkProfile.networkInterfaces[].id"
```

<span data-ttu-id="6863b-142">Esta técnica de consulta irá funcionar com qualquer comando da CLI do Azure e pode ser utilizada para extrair partes específicas da saída de dados na linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="6863b-142">This query technique will work with any Azure CLI command and can be used to pull specific bits of data out on the command line.</span></span> <span data-ttu-id="6863b-143">Também é útil para a criação de scripts - por exemplo, pode obter um valor da sua conta do Azure e armazená-lo numa variável de ambiente ou script.</span><span class="sxs-lookup"><span data-stu-id="6863b-143">It is useful for scripting as well - for example, you can pull a value out of your Azure account and store it in an environment or script variable.</span></span> <span data-ttu-id="6863b-144">Se decidir utilizá-lo desta forma, um sinalizador útil a adicionar é o parâmetro `--output tsv` (que pode ser reduzido para `-o tsv`).</span><span class="sxs-lookup"><span data-stu-id="6863b-144">If you decide to use it this way, a useful flag to add is the `--output tsv` parameter (which can be shortened to `-o tsv`).</span></span> <span data-ttu-id="6863b-145">Isto irá devolver os resultados em valores divididos em separadores, que incluem apenas os valores de dados reais com separadores de divisão.</span><span class="sxs-lookup"><span data-stu-id="6863b-145">This will return the results in tab-separated values that only include the actual data values with tab separators.</span></span>

<span data-ttu-id="6863b-146">Por exemplo,</span><span class="sxs-lookup"><span data-stu-id="6863b-146">As an example,</span></span>

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "networkProfile.networkInterfaces[].id" -o tsv
```

<span data-ttu-id="6863b-147">devolve o texto: `/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources/providers/Microsoft.Network/networkInterfaces/SampleVMVMNic`</span><span class="sxs-lookup"><span data-stu-id="6863b-147">returns the text: `/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources/providers/Microsoft.Network/networkInterfaces/SampleVMVMNic`</span></span>
