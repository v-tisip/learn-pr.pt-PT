Utilizámos `Debian` para a imagem para criar a máquina virtual. O Azure tem várias imagens de VM padrão que pode utilizar para criar uma máquina virtual. 

Pode obter uma lista das imagens disponíveis com o comando `az vm image list --output table`. Este procedimento mostrará as imagens mais populares que fazem parte de uma lista offline criada na CLI do Azure. No entanto, existem _centenas_ de opções de imagens disponíveis no Azure Marketplace. 

> [!TIP]
> Para obter uma lista completa, adicione sinalizador `--all` ao comando. Uma vez que a lista de imagens no Marketplace é muito grande, é útil filtrar a lista com as opções `--publisher` ou `–-offer`.

Algumas imagens só estão disponíveis em determinadas localizações. Tente adicionar o sinalizador `--location [location]` ao comando para restringir os resultados para os disponíveis na região onde pretende criar a máquina virtual. Por exemplo, escreva o seguinte no Azure Cloud Shell para obter uma lista de imagens disponíveis na região `eastus`.

```azurecli
az vm image list --location eastus --output table
```

> [!NOTE]
> Estas são as imagens padrão que são fornecidas pelo Azure. Tenha em atenção que também pode [criar e carregar as suas próprias imagens personalizadas](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-custom-images) para criar VMs com base em configurações exclusivas ou versões menos comuns ou distribuições de um sistema operativo.