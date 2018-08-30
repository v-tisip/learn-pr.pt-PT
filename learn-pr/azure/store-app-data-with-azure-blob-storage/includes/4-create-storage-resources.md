Assim que tivermos uma ideia sobre como vamos armazenar dados entre contas de armazenamento, contentores e blobs, podemos pensar sobre os recursos do Azure que temos de criar para suportar a aplicação.

### <a name="storage-accounts"></a>Contas de armazenamento

A criação da conta de armazenamento é uma atividade administrativa/gestão que ocorre antes de implementar e executar a sua aplicação. As contas são, normalmente, criadas por um script de configuração de implementação ou ambiente, um modelo do Azure Resource Manager ou manualmente por um administrador. As aplicações que não são ferramentas administrativas, geralmente não devem ter permissões para criar contas de armazenamento.

### <a name="containers"></a>Contentores

Ao contrário da criação da conta de armazenamento, a criação do contentor é uma atividade simples que faz sentido executar a partir de uma aplicação. É habitual as aplicações criarem e eliminarem contentores como parte do seu trabalho.

Para aplicações que dependem de um conjunto conhecido de contentores com nomes codificados ou pré-configurados, o mais habitual é permitir que a aplicação crie os contentores que precisa ao arrancar ou na primeira utilização, se ainda não existirem. Permitir que a sua aplicação possa criar contentores, em vez de fazê-lo como parte da implementação da aplicação, elimina a necessidade da sua aplicação e do processo de implementação conhecerem os nomes dos contentores que a aplicação utiliza.

## <a name="exercise"></a>Exercício

Vamos concluir uma aplicação ASP.NET Core incompleta ao adicionar código para utilizar o armazenamento de Blobs do Azure. Este exercício é mais sobre explorar a API de armazenamento de Blobs, do que estruturar uma organização e esquema de nomenclatura, mas aqui está uma rápida descrição geral da aplicação e como ela armazena dados:

**Captura de ecrã da lista de tarefas da aplicação, uma vez que não poderá ser vista até ao fim**

A nossa aplicação funciona como uma pasta partilhada que aceita carregamentos de ficheiros e torna-os disponíveis para download. Ela não utiliza uma base de dados para organizar os blobs &mdash;, em vez disso, limpa os nomes dos ficheiros carregados e utiliza-os diretamente como nomes de blobs. Todos os ficheiros carregados são armazenados num único contentor.

O código com que vamos começar é compilado e executado, mas as partes responsáveis por armazenar e carregar os dados estão vazias. Depois de concluirmos o código, iremos implementar a aplicação no Serviço de Aplicações do Azure e testá-la.

Vamos configurar a infraestrutura de armazenamento na nossa aplicação.

### <a name="resource-group-and-storage-account"></a>Grupo de recursos e conta de armazenamento
Em primeiro lugar, vamos criar um grupo de recursos para conter todos os recursos neste exercício. Vamos eliminá-lo no final para limpar tudo o que criamos. Também vamos criar a conta de armazenamento que a nossa aplicação irá utilizar para armazenar blobs.

Utilize o terminal do Azure Cloud Shell para criar o grupo de recursos e a conta de armazenamento ao executar os seguintes comandos da CLI do Azure. Terá de indicar um nome exclusivo para a conta de armazenamento &mdash;, tome nota da mesma para utilizar mais tarde. A escolha de `eastus` para a localização é arbitrária.

```console
az group create --name blob-exercise-group --location eastus
az storage account create --name <your-unique-storage-account-name> --resource-group blob-exercise-group --location eastus --kind StorageV2
```

**A lista de tarefas abaixo deve estar no módulo de Armazenamento do Azure**

> [!NOTE]
> Porquê `--kind StorageV2`? Existem alguns tipos diferentes de contas de armazenamento. Na maioria dos cenários, deve utilizar contas de armazenamento para fins gerais v2 (demonstradas com `StorageV2`). O único motivo de as contas de armazenamento v2 terem de ser especificadas aqui deve-se a ainda serem relativamente novas e não estarem predefinidas no Portal do Azure ou na CLI do Azure.

### <a name="container"></a>Contentor
A aplicação com que iremos trabalhar neste módulo utiliza um único contentor. Vamos seguir a melhor prática de permitir que a aplicação crie o contentor no arranque. No entanto, a criação do contentor pode ser feita a partir da CLI do Azure: execute `az storage container create -h` no terminal do Cloud Shell, se gostaria de ver a documentação.