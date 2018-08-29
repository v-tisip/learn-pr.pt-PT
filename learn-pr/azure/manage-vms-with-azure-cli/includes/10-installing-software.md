A última coisa que queremos experimentar na nossa VM é instalar um servidor Web. Um dos pacotes mais fácil de instalar é `nginx`.

1. Localize o endereço IP público da sua máquina virtual do Linux. Lembre-se de que pode utilizar o comando `vm list-ip-addresses` para o procurar.

2. Em seguida, abra uma ligação `ssh` à máquina como fez quando a testámos. Lembre-se de que tem de transmitir o nome de administrador ("**aldis**").

3. Na shell apresentada, execute o seguinte comando para instalar o servidor Web `nginx`.

```azurecli
sudo apt-get -y update && sudo apt-get -y install nginx
```

4. No Azure Cloud Shell, utilize `curl` para ler a página predefinida a partir do seu servidor Web do Linux. Pode, em alternativa, abrir um novo separador do browser para navegar para o endereço IP público.

```azurecli
curl 168.61.54.62
```

A operação irá falhar porque a máquina virtual do Linux não expõe a porta 80 (`http`) através da firewall incorporada. Felizmente, a CLI do Azure tem um comando para isso: `vm open-port`. 

5. Escreva o seguinte no Cloud Shell para abrir a porta 80:

```
az vm open-port --port 80 --resource-group ExerciseResources --name SampleVM
```

Por fim, experimente `curl` novamente. Desta vez, deverá devolver dados. Também pode ver a página num browser.



