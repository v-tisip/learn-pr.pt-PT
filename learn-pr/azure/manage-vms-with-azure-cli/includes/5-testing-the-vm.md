<span data-ttu-id="1b52b-101">Quando cria uma máquina virtual, é atribuído à mesma um endereço IP público, acessível através da Internet, e um endereço IP privado utilizado no datacenter do Azure.</span><span class="sxs-lookup"><span data-stu-id="1b52b-101">When you create a virtual machine, it gets assigned a public IP address that is reachable over the Internet, and a private IP address used within the Azure data center.</span></span> <span data-ttu-id="1b52b-102">Pode utilizar a ferramenta `ssh` para testar rapidamente se a VM do Linux está operacional.</span><span class="sxs-lookup"><span data-stu-id="1b52b-102">We can quickly test that the Linux VM is up and running using the `ssh` tool.</span></span> <span data-ttu-id="1b52b-103">Lembre-se de que definimos o nosso nome de administrador como `aldis`, pelo que temos de especificar isso.</span><span class="sxs-lookup"><span data-stu-id="1b52b-103">Remember that we set our admin name to `aldis`, so we have to specify that.</span></span>

```azurecli
ssh 168.61.54.62 -l aldis
```

> [!NOTE]
> <span data-ttu-id="1b52b-104">Não precisamos de palavra-passe porque gerámos um par de chaves SSH como parte da criação da VM.</span><span class="sxs-lookup"><span data-stu-id="1b52b-104">We don't need a password because we generated an SSH key pair as part of the VM creation.</span></span> <span data-ttu-id="1b52b-105">Na primeira vez em que utilizar a shell para entrar na VM, receberá um aviso sobre a autenticidade do anfitrião.</span><span class="sxs-lookup"><span data-stu-id="1b52b-105">The first time you shell into the VM, it will give you a prompt about the authenticity of the host.</span></span> 
> 
> <span data-ttu-id="1b52b-106">Isso ocorre porque estamos a atingir um endereço IP diretamente em vez de um nome de anfitrião.</span><span class="sxs-lookup"><span data-stu-id="1b52b-106">This is because we are hitting an IP address directly instead of a host name.</span></span> <span data-ttu-id="1b52b-107">Responder "Sim" irá guardar o IP como um anfitrião válido para ligação e permitir que a ligação prossiga.</span><span class="sxs-lookup"><span data-stu-id="1b52b-107">Answering "yes" will save the IP as a valid host for connection and allow the connection to proceed.</span></span>

```
The authenticity of host '168.61.54.62 (168.61.54.62)' can't be established.
RSA key fingerprint is SHA256:hlFnTCAzgWVFiMxHK194I2ap6+5hZoj9ex8+/hoM7rE.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '168.61.54.62' (RSA) to the list of known hosts.
```

<span data-ttu-id="1b52b-108">Em seguida, é-lhe apresentada uma shell remota na qual pode introduzir comandos do Linux.</span><span class="sxs-lookup"><span data-stu-id="1b52b-108">Then you'll be presented with a remote shell where you can enter Linux commands.</span></span>

```
The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
aldis@SampleVM:~$
```

<span data-ttu-id="1b52b-109">Experimente alguns comandos para praticar e, quando tiver acabado, termine a sessão da sua conta (escreva `logout` ou `exit` na shell).</span><span class="sxs-lookup"><span data-stu-id="1b52b-109">Try a few commands as practice and when you are finished, sign out of your account (type `logout` or `exit` in the shell).</span></span>