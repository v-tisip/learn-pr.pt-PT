## <a name="creating-key-vaults-for-your-applications"></a>Criar Cofres de Chaves para as suas aplicações

Uma prática recomendada é atribuir a cada aplicação um cofre separado para cada ambiente de implementação que utilizar, como, por exemplo, desenvolvimento, teste e produção. Ainda que lhe seja conveniente partilhar segredos entre as várias aplicações, lembre-se que o risco de um atacante obter acesso de leitura a um cofre aumenta com o número de segredos no cofre.

> [!TIP]
> Se utilizar os mesmos nomes para segredos entre os diferentes ambientes, a única configuração específica do ambiente que tem de ser alterada na aplicação é o URL do cofre.

Criar um cofre não requer qualquer configuração inicial. À sua identidade de utilizador é automaticamente concedido o conjunto completo de permissões de gestão de segredos e pode começar a adicionar segredos imediatamente. Assim que tiver um cofre, pode adicionar e gerir segredos a partir de qualquer interface administrativa do Azure, incluindo o portal do Azure, a CLI do Azure e o Azure PowerShell. Quando configurar a sua aplicação para utilizar o cofre, terá de atribuir as permissões corretas para-lo. Vamos ver isto na unidade seguinte.

## <a name="vault-authentication-and-permissions"></a>Permissões e autenticação do cofre

A API do Azure Key Vault utiliza o Azure Active Directory para autenticar utilizadores e aplicações. As políticas de acesso ao cofre baseiam-se em *ações* e são aplicadas à totalidade do cofre. Por exemplo, numa aplicação com as permissões **Obter** (ler valores secretos), **Listar** (listar nomes de todos os segredos), e **Definir** (criar ou atualizar valores secretos) para um cofre, é possível criar segredos, listar todos os nomes de segredos e obter e definir todos os valores dos segredos nesse cofre.

*Todas* as ações realizadas num cofre requerem autenticação e autorização &mdash; não é possível conceder qualquer tipo de acesso anónimo.

> [!TIP]
> Ao conceder acesso ao cofre a programadores e aplicações, conceda apenas o conjunto mínimo de permissões necessárias. As restrições de permissões ajudam a evitar acidentes provocados por erros de código e a reduzir o risco de credenciais roubadas ou código malicioso injetado na sua aplicação.

Regra geral, os programadores necessitam apenas das permissões **Obter** e **Listar** para um cofre de ambiente de desenvolvimento. Um programador chefe ou sénior necessitará de todas as permissões do cofre, para poder alterar e adicionar segredos sempre que necessário. Por norma, todas as permissões para os cofres de ambiente de produção estão reservadas para técnicos operacionais séniores.

No caso das aplicações, apenas as permissões **Obter** são, normalmente, necessárias. Algumas aplicações podem exigir permissões **Listar**, dependendo da forma como a aplicação for implementada. A aplicação que vamos implementar no exercício deste módulo precisa da permissão **Listar**, devido à técnica utilizada para ler os segredos do cofre.

## <a name="exercise"></a>Exercício

Tendo em conta todos os problemas que a empresa tem tido com os segredos da aplicação, a direção pediu-lhe para criar uma pequena aplicação de arranque para que os outros programadores possam seguir no caminho certo. A aplicação precisa de mostrar as melhores práticas para a gestão de segredos, da forma mais simples e mais segura possível.

Para começar, vai criar um cofre e armazenar um segredo.

### <a name="create-a-resource-group"></a>Criar um grupo de recursos

Crie um grupo de recursos com o nome `keyvault-exercise-group` para todos os recursos neste exercício. No final deste módulo, este grupo de recursos será eliminado para limpar tudo ao mesmo tempo. Vamos utilizar `eastus` como a localização para tudo neste exercício.

Utilize o terminal do Azure Cloud Shell no lado direito para executar o seguinte comando da CLI do Azure. Isso cria o grupo de recursos na sua subscrição.

```azurecli
az group create --name keyvault-exercise-group --location eastus
```

### <a name="create-the-vault-and-store-the-secret-in-it"></a>Criar o cofre e armazenar o segredo no mesmo

Criar o cofre e armazenar o segredo no mesmo.

**Os nomes do cofre de chaves têm de ser globalmente exclusivos e, portanto, precisará de escolher um nome exclusivo**. Os nomes do cofre têm de ter entre 3 e 24 carateres de comprimento e conter apenas carateres alfanuméricos e travessões.

```azurecli
az keyvault create --name <your-unique-vault-name> --resource-group keyvault-exercise-group --location eastus
```

Quando terminar, verá a saída JSON que descreve o novo cofre.

Agora, adicione o segredo: o nosso segredo terá o nome **SecretPassword** com um valor de **reindeer_flotilla**.

```azurecli
az keyvault secret set --name SecretPassword --value open_sesame --vault-name <your-unique-vault-name>
```

Tome nota do nome do cofre &mdash; vai precisar dele novamente em breve.

Vamos escrever o código para a nossa aplicação daqui a pouco, mas, primeiro, é necessário saber como a nossa aplicação se vai autenticar num cofre.