
Neste exercício, vai utilizar a CLI do Azure no computador local para criar um grupo de recursos e, em seguida, implementar uma aplicação Web neste grupo de recursos. 

### <a name="steps-to-create-a-resource-group"></a>Passos para criar um grupo de recursos
1. Abra uma shell do Bash no Linux ou macOS ou, em alternativa, abra a janela Linha de Comandos ou o PowerShell se estiver a trabalhar no Windows.

1. Inicie a CLI do Azure e execute o comando de início de sessão.

    ```bash
    az login
    ```
    Se não surgir uma página de início de sessão do Azure no browser, siga as instruções da linha de comandos e introduza um código de autorização em [https://aka.ms/devicelogin](https://aka.ms/devicelogin).

1. Crie um grupo de recursos.

    ```bash
    az group create --location westeurope --name popupResGroup
    ```

1. Verifique se o grupo de recursos foi criado com êxito ao listar todos os grupos de recursos numa tabela.

    ```bash
    az group list --output table
    ```
1. Opcionalmente, verifique se o recurso foi criado no portal do Azure. Abra um browser, inicie sessão no portal e navegue para a secção **Grupos de Recursos** (ver abaixo). O novo grupo de recursos deverá ser apresentado na lista.

![Utilizar o Portal para Listar os Grupos de Recursos](../media-drafts/5-listing-resource-groups.png)

### <a name="steps-to-create-a-service-plan"></a>Passos para criar um plano do serviço
Ao executar Aplicações Web, com o Serviço de Aplicações do Azure, paga os recursos de computação do Azure utilizados pela aplicação, o que depende do plano do Serviço de Aplicações associado às suas Aplicações Web. Os planos de serviço determinam a região utilizada para o datacenter da aplicação, o número de VMs utilizadas e o escalão de preços.

1. Crie um plano do Serviço da Aplicações para executar a aplicação. O nome da aplicação e do plano tem de ser exclusivo, assim, altere a cadeia de caracteres “12345” para um número aleatório. O comando seguinte não especifica um escalão de preço nem os detalhes de instância de VM; assim, por norma, obterá um plano **Básico** com 1 instância de VM **Pequena**.

    ```bash
    az appservice plan create --name popupapp12345 --resource-group popupResGroup --location westeurope
    ```

1. Verifique se o plano de serviço foi criado com êxito ao listar todos os planos numa tabela.

    ```bash
    az appservice plan list --output table
    ```

### <a name="steps-to-create-a-web-app"></a>Passos para criar uma aplicação Web
Em seguida, vai criar a aplicação Web no plano de serviço. Pode implementar o código ao mesmo tempo, mas, no nosso exemplo, vamos fazê-lo em passos distintos.

1. Crie a aplicação Web, lembrando-se de alterar a cadeia de caracteres “12345” para o mesmo número aleatório que utilizou anteriormente.
    ```bash
    az webapp create --name popupapp12345 --resource-group popupResGroup --plan popupapp12345
    ```

1. Verifique se a aplicação foi criada com êxito ao listar todas as aplicações numa tabela.

    ```bash
    az webapp list --output table
    ```

1. Anote o **DefaultHostName**; vai precisar dele posteriormente.

### <a name="steps-to-deploy-code-from-github"></a>Passos para implementar o código a partir do GitHub
1. A etapa final é implementar código a partir de um repositório do GitHub na aplicação Web, lembrando-se igualmente de alterar a cadeia de caracteres “12345” para o mesmo número aleatório que utilizou anteriormente.
    ```bash
    az webapp deployment source config --name popupapp12345 --resource-group popupResGroup --repo-url "https://github.com/Azure-Samples/php-docs-hello-world" --branch master --manual-integration
    ```

1. Copie o URL seguinte para um browser para ver a aplicação Web.
http://popupapp12345.azurewebsites.net

1. A página apresenta “OláMundo!”

1. Feche a janela do browser.

## <a name="summary"></a>Resumo
Este exercício demonstrou um padrão típico de uma sessão interativa da CLI do Azure. Primeiro, utilizou um comando padrão para criar um novo grupo de recursos. Em seguida, utilizou um conjunto de comandos para implementar um recurso (neste exemplo, uma aplicação Web) para este grupo de recursos. Este conjunto de comandos poderá ser facilmente combinado num script de shell e executado sempre que precisar de criar o mesmo recurso.
