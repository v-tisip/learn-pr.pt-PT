## <a name="motivation"></a>Motivação
A CLI do Azure permite-lhe escrever comandos e executá-los imediatamente. Lembre-se de que o objetivo geral no exemplo de desenvolvimento de software é implementar novas compilações de uma aplicação Web para fins de teste. O primeiro passo é criar um grupo de recursos. Lembre-se de que o objetivo aqui é criar estes recursos com uma instalação local da CLI do Azure. 

Esta unidade mostra-lhe como utilizar a CLI do Azure para iniciar sessão na sua subscrição do Azure e criar um novo recurso.

## <a name="what-azure-resources-can-be-managed-using-the-azure-cli"></a>Que recursos do Azure podem ser geridos com a CLI do Azure?
A CLI do Azure permite-lhe controlar praticamente todos os aspectos de cada recurso do Azure. Pode trabalhar com grupos de recursos, armazenamento, máquinas virtuais, Azure Active Directory (Azure AD), contentores, aprendizagem automática e assim por diante.

Os comandos da CLI são estruturados em grupos e subgrupos. Cada grupo representa um serviço fornecido pelo Azure, sendo que os subgrupos dividem os comandos desses serviços em agrupamentos lógicos. Por exemplo, o grupo **armazenamento** contém subgrupos que incluem **conta**, **blob**, **armazenamento** e **fila**.

Assim, como encontrar os comandos específicos de que precisa? Uma das formas é usar **az find**. Por exemplo, se quiser localizar comandos que podem ajudá-lo a gerir um **blob** de armazenamento, usará o seguinte comando de pesquisa:

```bash
az find -q blob
```

Se já sabe o nome do comando que pretende, o argumento **--help** desse comando poderá ser mais útil. Obtém informações detalhadas sobre o comando e, para um grupo de comandos, uma lista de subcomandos disponíveis. Assim, com o nosso exemplo de armazenamento, apresentamos a seguir como pode obter uma lista dos comandos e dos subgrupos para gerir o armazenamento de blobs:

```bash
az storage blob --help
```

## <a name="how-to-create-an-azure-resource"></a>Como criar um recurso do Azure
Ao criar um novo recurso do Azure, normalmente, existem três passos: ligar-se à sua subscrição do Azure, criar o recurso e verificar se a criação foi concluída com êxito (ver abaixo).

![Passos para criar um recurso com a CLI do Azure](../media-drafts/4-create-resources-overview.png)

Cada passo corresponde a um comando da CLI do Azure diferente.

### <a name="connect"></a>Ligar
Dado que está a trabalhar com uma instalação local da CLI do Azure, terá de se autenticar para poder executar os comandos do Azure, através do comando **login** da CLI do Azure. 

```bash
az login
```

A CLI do Azure, normalmente, iniciará o seu browser predefinido para abrir a página de início de sessão do Azure. Se não funcionar, siga as instruções da linha de comandos e introduza um código de autorização em [https://aka.ms/devicelogin](https://aka.ms/devicelogin).

Após iniciar sessão, estará conectado à sua subscrição do Azure. 

### <a name="create"></a>Criar
Muitas vezes, terá de criar um novo grupo de recursos antes de criar um novo serviço do Azure, pelo que vamos utilizar grupos de recursos como exemplo para mostrar como criar recursos do Azure a partir da CLI.

O comando **group create** da CLI do Azure cria um grupo de recursos. Tem de especificar um nome e a localização. O nome tem de ser exclusivo na sua subscrição. A localização determina onde os metadados do grupo de recursos serão armazenados. Utilize cadeias de caracteres como “EUA Oeste”, “Europa do Norte” ou “Oeste da Índia” para especificar a localização; em alternativa, pode usar equivalentes de palavra única, por exemplo, euaoeste, europanorte ou oesteíndia. A sintaxe principal é:

```bash
az group create --name <name> --location <location>
```

### <a name="verify"></a>Verificar
Para muitos recursos do Azure, a CLI do Azure fornece um subcomando de **lista** para ver os detalhes dos recursos. Por exemplo, a **lista de grupos** da CLI do Azure lista os seus grupos de recursos do Azure. Este subcomando é útil para verificar se a criação do grupo de recursos foi concluída com êxito:

```bash
az group list
```

Para obter uma vista mais concisa, pode formatar a saída para ser uma tabela simples:

```bash
az group list --output table
```
