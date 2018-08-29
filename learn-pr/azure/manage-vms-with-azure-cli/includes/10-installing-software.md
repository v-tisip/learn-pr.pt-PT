<span data-ttu-id="9617a-101">A última coisa que queremos experimentar na nossa VM é instalar um servidor Web.</span><span class="sxs-lookup"><span data-stu-id="9617a-101">The last thing we want to try on our VM is to install a web server.</span></span> <span data-ttu-id="9617a-102">Um dos pacotes mais fácil de instalar é `nginx`.</span><span class="sxs-lookup"><span data-stu-id="9617a-102">One of the easiest packages to install is `nginx`.</span></span>

1. <span data-ttu-id="9617a-103">Localize o endereço IP público da sua máquina virtual do Linux.</span><span class="sxs-lookup"><span data-stu-id="9617a-103">Locate the public IP address of your Linux virtual machine.</span></span> <span data-ttu-id="9617a-104">Lembre-se de que pode utilizar o comando `vm list-ip-addresses` para o procurar.</span><span class="sxs-lookup"><span data-stu-id="9617a-104">Remember you can use the `vm list-ip-addresses` command to look it up.</span></span>

2. <span data-ttu-id="9617a-105">Em seguida, abra uma ligação `ssh` à máquina como fez quando a testámos.</span><span class="sxs-lookup"><span data-stu-id="9617a-105">Next, open an `ssh` connection to the machine like you did when we tested it.</span></span> <span data-ttu-id="9617a-106">Lembre-se de que tem de transmitir o nome de administrador ("**aldis**").</span><span class="sxs-lookup"><span data-stu-id="9617a-106">Remember you will need to pass in the admin name ("**aldis**").</span></span>

3. <span data-ttu-id="9617a-107">Na shell apresentada, execute o seguinte comando para instalar o servidor Web `nginx`.</span><span class="sxs-lookup"><span data-stu-id="9617a-107">In the presented shell, execute the following command to install the `nginx` web server.</span></span>

```azurecli
sudo apt-get -y update && sudo apt-get -y install nginx
```

4. <span data-ttu-id="9617a-108">No Azure Cloud Shell, utilize `curl` para ler a página predefinida a partir do seu servidor Web do Linux.</span><span class="sxs-lookup"><span data-stu-id="9617a-108">In Azure Cloud Shell, use `curl` to read the default page from your Linux web server.</span></span> <span data-ttu-id="9617a-109">Pode, em alternativa, abrir um novo separador do browser para navegar para o endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="9617a-109">Alternatively, you can open a new browser tab and browse to the public IP address.</span></span>

```azurecli
curl 168.61.54.62
```

<span data-ttu-id="9617a-110">A operação irá falhar porque a máquina virtual do Linux não expõe a porta 80 (`http`) através da firewall incorporada.</span><span class="sxs-lookup"><span data-stu-id="9617a-110">It will fail because the Linux virtual machine doesn't expose port 80 (`http`) through the built-in firewall.</span></span> <span data-ttu-id="9617a-111">Felizmente, a CLI do Azure tem um comando para isso: `vm open-port`.</span><span class="sxs-lookup"><span data-stu-id="9617a-111">Luckily, the Azure CLI has a command for that: `vm open-port`.</span></span> 

5. <span data-ttu-id="9617a-112">Escreva o seguinte no Cloud Shell para abrir a porta 80:</span><span class="sxs-lookup"><span data-stu-id="9617a-112">Type the following into Cloud Shell to open port 80:</span></span>

```
az vm open-port --port 80 --resource-group ExerciseResources --name SampleVM
```

<span data-ttu-id="9617a-113">Por fim, experimente `curl` novamente.</span><span class="sxs-lookup"><span data-stu-id="9617a-113">Finally, try `curl` again.</span></span> <span data-ttu-id="9617a-114">Desta vez, deverá devolver dados.</span><span class="sxs-lookup"><span data-stu-id="9617a-114">This time it should return data.</span></span> <span data-ttu-id="9617a-115">Também pode ver a página num browser.</span><span class="sxs-lookup"><span data-stu-id="9617a-115">You can see the page in a browser as well.</span></span>



