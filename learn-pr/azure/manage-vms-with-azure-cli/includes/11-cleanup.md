Criou uma nova máquina virtual Linux, alterou o seu tamanho, parou-a e iniciou-a e atualizou a configuração com a CLI do Azure.

## <a name="cleanup"></a>Limpeza

Agora que já não precisamos da VM, vamos eliminar os recursos. A limpeza é importante para os recursos de computação e de armazenamento que podem continuar a ser faturados na sua conta. 

Pode eliminar recursos individuais com o comando `delete`, mas a forma mais fácil de remover tudo é com `az group delete`. Execute o seguinte comando na CLI do Azure:

```azurecli
az group delete --name ExerciseResources --no-wait
```

Responda “sim” na linha de comandos, quando solicitado, ou utilize o parâmetro `--yes` para responder de forma automática ao prompt.

Este comando elimina todos os recursos associados ao grupo de recursos e desaloca-os garantidamente pela ordem correta. O parâmetro `--no-wait` impede que a CLI do Azure bloqueie enquanto a eliminação está em curso. Deixe-a desativada para aguardar que os recursos sejam eliminados. Em alternativa, utilize o comando `az group wait -n ExerciseResources --deleted` posteriormente no script para aguardar que a eliminação chegue ao fim.


## <a name="further-reading"></a>Leitura adicional

* [Descrição geral da CLI do Azure](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest)
* [Referência de comandos da CLI do Azure](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest)
