O nosso objetivo é criar uma nova máquina virtual do Azure. Vamos precisar de fornecer várias informações para identificar a localização do recurso, o SO a utilizar e a configuração de hardware necessária para a VM. Vamos começar pelo **grupo de recursos**.

## <a name="create-a-resource-group"></a>Criar um grupo de recursos

O Azure utiliza _grupos de recursos_ para agrupar recursos relacionados, como máquinas virtuais e bases de dados. O grupo de recursos também identifica uma localização específica (denominada "região") que vai decidir em que datacenter o recurso será colocado.

Como estamos a experimentar, comece por criar um novo grupo de recursos com o nome `ExerciseResources` e coloque-o na região `eastus`.

> [!NOTE]
> Certifique-se de que utiliza este nome exato para o novo grupo de recursos, uma vez que o sistema Microsoft Learn irá procurar este nome de recurso mais tarde. 

Escreva o seguinte comando da CLI do Azure no Azure Cloud Shell para criar o grupo de recursos na sua subscrição.

```azurecli
az group create --name ExerciseResources --location eastus
```

Isto irá devolver um bloco JSON que indica que o grupo de recursos foi criado. Deverá ter um aspeto semelhante a:

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

Repare que devolve o identificador exclusivo da subscrição, a localização e o nome como parte da resposta. Pode utilizar estes dados para verificar se foi criado na subscrição e localização adequadas.

Agora que temos um grupo de recursos, vamos criar uma nova máquina virtual.