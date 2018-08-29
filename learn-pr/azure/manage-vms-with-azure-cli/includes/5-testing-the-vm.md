Quando cria uma máquina virtual, é atribuído à mesma um endereço IP público, acessível através da Internet, e um endereço IP privado utilizado no datacenter do Azure. Pode utilizar a ferramenta `ssh` para testar rapidamente se a VM do Linux está operacional. Lembre-se de que definimos o nosso nome de administrador como `aldis`, pelo que temos de especificar isso.

```azurecli
ssh 168.61.54.62 -l aldis
```

> [!NOTE]
> Não precisamos de palavra-passe porque gerámos um par de chaves SSH como parte da criação da VM. Na primeira vez em que utilizar a shell para entrar na VM, receberá um aviso sobre a autenticidade do anfitrião. 
> 
> Isso ocorre porque estamos a atingir um endereço IP diretamente em vez de um nome de anfitrião. Responder "Sim" irá guardar o IP como um anfitrião válido para ligação e permitir que a ligação prossiga.

```
The authenticity of host '168.61.54.62 (168.61.54.62)' can't be established.
RSA key fingerprint is SHA256:hlFnTCAzgWVFiMxHK194I2ap6+5hZoj9ex8+/hoM7rE.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '168.61.54.62' (RSA) to the list of known hosts.
```

Em seguida, é-lhe apresentada uma shell remota na qual pode introduzir comandos do Linux.

```
The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
aldis@SampleVM:~$
```

Experimente alguns comandos para praticar e, quando tiver acabado, termine a sessão da sua conta (escreva `logout` ou `exit` na shell).