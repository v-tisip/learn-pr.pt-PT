As máquinas virtuais têm de ser dimensionadas de forma adequada para o trabalho esperado. Uma VM sem a quantidade correta de memória ou de CPU falhará quando em carga ou será executada muito lentamente para ser eficiente. 

Quando cria uma máquina virtual, pode indicar um valor de _tamanho da VM_ para determinar a quantidade de recursos de computação que será dedicada à VM. Tal inclui a CPU, a GPU e a memória que ficam disponíveis para a máquina virtual do Azure.

O Azure define um conjunto de [tamanhos predefinidos de VM](https://docs.microsoft.com/azure/virtual-machines/linux/sizes) para o Linux e o Windows escolherem com base na utilização esperada. 

| Tipo | Tamanhos | Descrição |
|------|-------|-------------|
| Fins gerais   | Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7 | CPU-para-memória equilibrada. Ideal para desenvolvimento/teste e aplicações e soluções de dados pequenas a médias. |
| Com otimização de computação | Fs, F | CPU-para-memória elevada. Adequada para aplicações de tráfego médio, dispositivos de rede e processos em lote. |
| Com otimização de memória  | Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D   | Memória-para-núcleo elevada. É ideal para bases de dados relacionais, caches médias a grandes e análise dentro da memória. |
| Com otimização de armazenamento | Ls | Débito e E/S de disco elevados. Ideal para bases de dados de macrodados, SQL e NoSQL. |
| Com otimização de GPU | NV, NC | VMs especializadas destinadas a composição gráfica e edição de vídeo exigentes. |
| Elevado desempenho | H, A8-11 | As nossas mais poderosas VMs com CPU, com interfaces de rede de alto débito (RDMA) opcionais. | 

A alteração de tamanhos disponíveis com base na região em que está a criar a VM. Pode obter uma lista dos tamanhos disponíveis com o comando `vm list-sizes`. Tente digitá-lo no Azure Cloud Shell:

```azurecli
az vm list-sizes --location eastus --output table
```

Esta é uma resposta abreviada para `eastus`:

```
  MaxDataDiskCount    MemoryInMb  Name                      NumberOfCores    OsDiskSizeInMb    ResourceDiskSizeInMb
------------------  ------------  ----------------------  ---------------  ----------------  ----------------------
                 2          2048  Standard_B1ms                         1           1047552                    4096
                 2          1024  Standard_B1s                          1           1047552                    2048
                 4          8192  Standard_B2ms                         2           1047552                   16384
                 4          4096  Standard_B2s                          2           1047552                    8192
                 8         16384  Standard_B4ms                         4           1047552                   32768
                16         32768  Standard_B8ms                         8           1047552                   65536
                 4          3584  Standard_DS1_v2                       1           1047552                    7168
                 8          7168  Standard_DS2_v2                       2           1047552                   14336
                16         14336  Standard_DS3_v2                       4           1047552                   28672
                32         28672  Standard_DS4_v2                       8           1047552                   57344
                64         57344  Standard_DS5_v2                      16           1047552                  114688
        ....
                64       3891200  Standard_M128-32ms                  128           1047552                 4096000
                64       3891200  Standard_M128-64ms                  128           1047552                 4096000
                64       3891200  Standard_M128ms                     128           1047552                 4096000
                64       2048000  Standard_M128s                      128           1047552                 4096000
                64       1024000  Standard_M64                         64           1047552                 8192000
                64       1792000  Standard_M64m                        64           1047552                 8192000
                64       2048000  Standard_M128                       128           1047552                16384000
                64       3891200  Standard_M128m                      128           1047552                16384000
```

Não especificámos um tamanho quando criámos a nossa VM, pelo que o Azure selecionou um tamanho para fins gerais predefinido de `Standard_DS1_v2`. No entanto, podemos especificar o tamanho como parte do comando `vm create` com o parâmetro `--size`.

```azurecli
az vm create --resource-group ExerciseResources --name SampleVM \
  --image Debian --admin-username aldis --generate-ssh-keys --verbose \
  --size "Standard_DS5_v2"
```

## <a name="resizing-an-existing-vm"></a>Redimensionar uma VM existente
Também poderemos redimensionar uma VM existente se a carga de trabalho for alterada ou se tiver sido dimensionada incorretamente durante a criação. Antes de pedirmos um redimensionamento, devemos verificar se o tamanho desejado está disponível no cluster de que faz parte a VM. Podemos fazer isto com o comando `vm list-vm-resize-options`:

```azurecli
az vm list-vm-resize-options --resource-group ExerciseResources --name SampleVM --output table
```

Esta ação devolverá uma lista de todas as configurações de tamanho possíveis disponíveis no grupo de recursos. Se o tamanho que queremos não estiver disponível no nosso cluster, mas _estiver_ disponível na região, poderemos [desalocar a VM](https://docs.microsoft.com/cli/azure/vm?view=azure-cli-latest#az-vm-deallocate). Este comando para a VM em execução e remova-a do cluster atual sem perder quaisquer recursos. Em seguida, podemos redimensioná-la, o que voltará a criar a VM num novo cluster onde a configuração de tamanho esteja disponível.

Para redimensionar uma VM, usamos o comando `vm resize`. Por exemplo, vamos reduzir os nossos recursos de VM atuais para o mínimo: 2 G de memória, 1 núcleo de CPU e 4 G de espaço em disco. Escreva este comando no Cloud Shell:

```azurecli
az vm resize --resource-group ExerciseResources --name SampleVM --size "Standard_B1ms"
```

Este comando demorará alguns minutos a reduzir os recursos da VM e, uma vez concluído, devolverá uma nova configuração de JSON.