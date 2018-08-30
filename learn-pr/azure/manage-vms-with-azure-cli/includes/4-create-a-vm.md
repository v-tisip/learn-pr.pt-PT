A CLI do Azure inclui o comando `vm` para trabalhar com máquinas virtuais no Azure. Podemos fornecer vários subcomandos para fazer tarefas específicas. Os mais comuns incluem:

| Subcomando | Descrição |
|-------------|-------------|
| `create`    | Criar uma máquina virtual nova |
| `deallocate` | Desalocar uma máquina virtual |
| `delete` | Eliminar uma máquina virtual |
| `list` | Listar as máquinas virtuais criadas na subscrição |
| `open-port` | Abrir uma porta de rede específica para o tráfego de entrada |
| `restart` | Reiniciar uma máquina virtual |
| `show` | Obter os detalhes de uma máquina virtual |
| `start` | Iniciar uma máquina virtual parada |
| `stop` | Parar uma máquina virtual em execução |
| `update` | Atualizar uma propriedade de uma máquina virtual |

> [!NOTE]
> Para obter uma lista completa de comandos, pode ver a [documentação de referência da CLI do Azure](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest).

Vamos começar com o primeiro comando: `az vm create`. Este comando é utilizado para criar uma máquina virtual num grupo de recursos. Existem vários parâmetros que pode passar para configurar todos os aspetos da nova VM. Tem de indicar os três parâmetros seguintes:

| Parâmetro | Descrição |
|-----------|-------------|
| `resource-group` | O grupo de recursos proprietário da máquina virtual |
| `name` | O nome da máquina virtual – deve ser exclusivo no grupo de recursos |
| `image` | A imagem do sistema operativo a utilizar para criar a VM |

Além disso, é útil adicionar o sinalizador `--verbose` para ver o progresso enquanto a VM está a ser criada. 

## <a name="create-a-linux-virtual-machine"></a>Criar uma máquina virtual do Linux

Vamos criar uma nova máquina virtual do Linux. Execute o seguinte comando no Azure Cloud Shell:

```azurecli
az vm create --resource-group ExerciseResources --name SampleVM --image Debian --admin-username aldis --generate-ssh-keys --verbose 
```

Este comando cria uma nova máquina virtual Linux **Debian** com o nome `SampleVM`. Tenha em atenção que a ferramenta de CLI do Azure está bloqueada enquanto a VM está a ser criada. Se preferir não esperar, poderá utilizar a opção `--no-wait` para informar a ferramenta de CLI do Azure para ficar ativa imediatamente, por exemplo, se estiver a executar o comando num script. Posteriormente no script, utilize o comando `azure vm wait --name [vm-name]` para aguardar a conclusão da criação da VM.

Se examinar as respostas verbosas, também verá que o nome `SampleVM` é utilizado como nome de várias dependências da VM.

```
Succeeded: SampleVMNSG (Microsoft.Network/networkSecurityGroups)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMPublicIP (Microsoft.Network/publicIPAddresses)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMVNET (Microsoft.Network/virtualNetworks)
Accepted: vm_deploy_vzKnQDyyq48yPUO4VrSDfFIi81vHKZ9g (Microsoft.Resources/deployments)
```

Pode substituir estes nomes de recursos gerados automaticamente com os parâmetros opcionais para `vm create`, tais como `--vnet-name` e `--public-ip-address-dns-name`.

Tenha em atenção que estamos a especificar o nome da conta de administrador através do sinalizador `admin-username` para ser “aldis”. Se o omitir, o comando `vm create` utilizará o seu _nome de utilizador atual_. Uma vez que as regras para os nomes de conta são diferentes para cada sistema operativo, é mais seguro indicar um nome específico. Os nomes comuns, como “raiz” e “admin” não são permitidos para a maioria das imagens.

Estamos também a utilizar o sinalizador `generate-ssh-keys`. Este parâmetro é utilizado para as distribuições Linux e cria um par de chaves de segurança, pelo que podemos usar a ferramenta `ssh` para aceder remotamente à máquina virtual. Os dois ficheiros são colocados na pasta `.ssh` no computador e na VM. Se já tiver uma chave SSH com o nome `id_rsa` na pasta de destino, esta será usada em vez de gerar uma chave nova.

Após a conclusão da criação da VM, obterá uma resposta JSON, que inclui o estado atual da máquina virtual e os endereços IP públicos e privados atribuídos pelo Azure:

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

