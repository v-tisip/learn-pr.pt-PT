Agora que criou uma máquina virtual, podemos obter informações sobre a mesma através de outros comandos.

Comecemos com `vm list`.

```azurecli
az vm list
```

Este comando irá devolver _todas_ as máquinas virtuais definidas nesta subscrição. A saída pode ser filtrada para um grupo de recursos específico através do parâmetro `--resource-group`. 

## <a name="output-types"></a>Tipos de saída
Tenha em atenção que o tipo de resposta predefinida para todos os comandos que fizemos até agora é um JSON. Isto é ótimo para a criação de scripts - mas a maioria das pessoas acha mais difícil de ler. Pode alterar o estilo de saída para qualquer resposta através do sinalizador `--output`. Por exemplo, experimente o seguinte comando no Azure Cloud Shell para ver o estilo de saída diferente.

```azurecli
az vm list --output table
```

Juntamente com `table`, pode especificar `json` (a predefinição), `jsonc` (JSON colorido) ou `tsv` (Valores Separados por Tabela). Experimente algumas variações com o comando acima para ver a diferença.

## <a name="getting-the-ip-address"></a>Obter o endereço IP

Outro comando útil é `vm list-ip-addresses`, que irá listar os endereços IP público e privado para uma VM. Se forem alterados ou não os capturar durante a criação, pode obtê-los em qualquer altura.

```azurecli
az vm list-ip-addresses -n SampleVM -o table
```

Esta ação devolve:

```
VirtualMachine    PublicIPAddresses    PrivateIPAddresses
----------------  -------------------  --------------------
SampleVM          168.61.54.62         10.0.0.4
```

> [!NOTE]
> Tenha em atenção que estamos a utilizar uma sintaxe abreviada para o sinalizador `--output` como `-o`. A maioria dos parâmetros para comandos da CLI do Azure podem ser reduzidos para um travessão único e uma letra. Por exemplo, `--name` pode ser reduzido para `-n` e `--resource-group` para `-g`. Isto é útil para escrever, mas recomendamos que utilize o nome da opção completa em scripts para maior clareza. Verifique a documentação para obter detalhes sobre cada comando.

## <a name="getting-vm-details"></a>A obter detalhes da VM

Podemos obter informações mais detalhadas sobre uma máquina virtual específica pelo nome ou ID com o comando `vm show`.

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM
```

Isto irá devolver um bloco JSON bastante grande com todos os tipos de informações sobre a VM, incluindo dispositivos de armazenamento anexados, interfaces de rede e todos os IDs de objeto para recursos a que a VM está ligada. Novamente, podemos alterar para um formato de tabela, mas isso omite quase todos os dados interessantes. Em vez disso, podemos ativar para uma linguagem de consulta incorporada para JSON denominado [JMESPath](http://jmespath.org/).

## <a name="adding-filters-to-queries-with-jmespath"></a>Adicionar filtros a consultas com JMESPath

JMESPath é uma linguagem de consulta padrão do setor criada em torno de objetos JSON. A consulta mais simples é especificar um _identificador_ que seleciona uma chave no objeto JSON.

Por exemplo, dado o objeto:

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

Podemos utilizar a consulta `people` para devolver a matriz de valores para a matriz `people`. Se queremos apenas _uma_ das pessoas, podemos utilizar um indexador. Por exemplo, `people[1]` iria devolver:

```json
{
    "name": "Barney",
    "age": 25
}
```

Também podemos adicionar qualificadores específicos que iriam devolver apenas os objetos `Fred` e `Wilma`. 

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

Por fim, pode restringir os resultados ao adicionar uma seleção: `people[?age > '25'].[name]` que devolve apenas os nomes:

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

JMESQuery tem várias outras funcionalidades interessantes da consulta. Quando tiver tempo, veja o [tutorial online](http://jmespath.org/tutorial.html) disponível no site [JMESPath.org](http://jmespath.org/).

## <a name="filtering-our-azure-cli-queries"></a>Filtrar as nossas consultas da CLI do Azure

Com uma compreensão básica das consultas JMES, podemos adicionar filtros aos dados devolvidos por consultas, como o comando `vm show`. Por exemplo, podemos recuperar o nome de utilizador administrador:

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "osProfile.adminUsername"
```

Podemos obter o tamanho atribuído à nossa VM:

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query hardwareProfile.vmSize
```

Ou para obter todos os IDs para as interfaces de rede, pode utilizar a consulta:

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "networkProfile.networkInterfaces[].id"
```

Esta técnica de consulta irá funcionar com qualquer comando da CLI do Azure e pode ser utilizada para extrair partes específicas da saída de dados na linha de comandos. Também é útil para a criação de scripts - por exemplo, pode obter um valor da sua conta do Azure e armazená-lo numa variável de ambiente ou script. Se decidir utilizá-lo desta forma, um sinalizador útil a adicionar é o parâmetro `--output tsv` (que pode ser reduzido para `-o tsv`). Isto irá devolver os resultados em valores divididos em separadores, que incluem apenas os valores de dados reais com separadores de divisão.

Por exemplo,

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "networkProfile.networkInterfaces[].id" -o tsv
```

devolve o texto: `/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources/providers/Microsoft.Network/networkInterfaces/SampleVMVMNic`
