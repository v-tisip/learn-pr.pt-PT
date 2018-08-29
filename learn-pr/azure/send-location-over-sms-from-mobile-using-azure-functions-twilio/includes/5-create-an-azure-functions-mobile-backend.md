Neste momento, a aplicação está a trabalhar para obter a localização do utilizador e está pronta para ser enviada para uma função do Azure. Nesta unidade, vai criar a função do Azure.

## <a name="create-an-azure-functions-project"></a>Criar um projeto das Funções do Azure

1. Adicione um novo projeto à solução `ImHere` ao clicar com o botão direito do rato na solução e selecione *Adicionar->Novo Projeto...*.

2. Na árvore do lado esquerdo, selecione *Visual C#->Cloud* e, em seguida, selecione *Funções do Azure* no painel do centro.

3. Nomeie o projeto "ImHere.Functions" e, em seguida, clique em **OK**.

    ![A caixa de diálogo Adicionar Novo Projeto](../media/5-add-new-functions-project.png)

4. Na caixa de diálogo de configuração **Novo Projeto**, deixe a versão das Funções definida como *Funções do Azure v1 (.NET Framework)*. Selecione *Acionador Http*, deixe a conta de armazenamento definida como *Emulador de Armazenamento* e defina os direitos de acesso para *Anónimo*. Em seguida, clique em **OK**.

    ![A caixa de diálogo de configuração de projeto da Função do Azure](../media/5-configure-trigger.png)

O novo projeto será criado e tem uma função predefinida denominada `Function1`.

> Esta função foi criada com acesso anónimo. Depois de estar publicado no Azure, qualquer pessoa que conhece o URL poderá chamar esta função. Num cenário do mundo real, teria de proteger isto com algum tipo de autenticação, como a [autenticação do Serviço de Aplicações do Azure](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview) ou o [Azure Active Directory B2C](https://docs.microsoft.com/azure/active-directory-b2c).

## <a name="create-the-function"></a>Criar a função

O projeto das Funções do Azure é criado com uma única função de acionador HTTP chamada `Function1`. A função em si é implementada como um método `Run` estático na classe `Function1`.

1. Renomeie o ficheiro no Explorador de Soluções de "Function1.cs" para "SendLocation.cs". Quando lhe for pedido para mudar o nome de todas as referências do elemento de código `Function1`, clique em **Sim**.

2. Mude o nome da função no atributo para "SendLocation".

    ```cs
    [FunctionName("SendLocation")]
    ```

3. Elimine o conteúdo da função, exceto a primeira linha que escreve uma mensagem de informações no logger.

    ```cs
    public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                                   "get", "post",
                                                                   Route = null)]HttpRequestMessage req,
                                                       TraceWriter log)
    {
        log.Info("C# HTTP trigger function processed a request.");
    }
    ```

## <a name="create-a-class-to-share-data-between-the-mobile-app-and-function"></a>Crie uma classe para partilhar dados entre a aplicação móvel e a função

Quando os dados são enviados para a função do Azure, serão enviados como JSON. A aplicação móvel vai serializar dados no JSON e a função vai anular a serialização do JSON. Para manter estes dados consistentes entre a aplicação móvel e a função, crie um novo projeto que contém uma classe para manter a localização e os dados do número de telefone. Este projeto será, em seguida, referenciado pela aplicação e pela função.

1. Crie um novo projeto sob a solução `ImHere` ao clicar com o botão direito do rato na solução e selecionar *Adicionar->Novo Projeto...*.

2. Na árvore do lado esquerdo, selecione *Visual C#->.NET Standard* e, em seguida, selecione *Biblioteca de Classes (.NET Standard)* no painel do centro.

3. Nomeie o projeto "ImHere.Data" e, em seguida, clique em **OK**.

    ![A caixa de diálogo Adicionar Novo Projeto](../media/5-add-new-net-standard-project.png)

4. Elimine o ficheiro "Class1.cs" gerado automaticamente.

5. Crie uma nova classe no projeto `ImHere.Data` chamada `PostData` ao clicar com o botão direito do rato no projeto e, em seguida, selecione *Adicionar->Classe...* . Nomeie a nova classe "PostData" e clique em **OK**.

6. Adicione as propriedades `double` para a latitude e a longitude, bem como uma propriedade `string[]` para os números de telefone a enviar.

    ```cs
    public class PostData
    {
        public double Latitude { get; set; }
        public double Longitude { get; set; }
        public string[] ToNumbers { get; set; }
    }
    ```

7. Adicione uma referência a este projeto para os projetos `ImHere.Functions` e `ImHere` ao clicar com o botão direito do rato no projeto e, em seguida, selecione *Adicionar->Referência...* . Selecione *Projetos* na árvore do lado esquerdo e, em seguida, assinale a caixa junto a *ImHere.Data*.

    ![Configurar referências do projeto](../media/5-configure-project-references.png)

## <a name="read-the-data-sent-to-the-function"></a>Ler os dados enviados para a função

Na função do Azure, o parâmetro `req` contém o pedido HTTP que foi feito e os dados contidos neste pedido serão um objeto `PostData` serializado JSON.

1. Abra a classe `SendLocation` no projeto `ImHere.Functions`.

2. Leia o conteúdo do pedido HTTP para um objeto `PostData`, ao adicionar uma diretiva em utilização para o espaço de nomes `ImHere.Data`.

    ```cs
    PostData data = await req.Content.ReadAsAsync<PostData>();
    ```

3. Construa um URL do Google Maps com a latitude e a longitude a partir de `PostData`.

   ```cs
   string url = $"https://www.google.com/maps/search/?api=1&query={data.Latitude},{data.Longitude}";
   ```

4. Registe o URL.

    ```cs
    log.Info($"URL created - {url}");
    ```

5. Devolva um código de estado 200 para mostrar a função que foi concluída sem erros.

    ```cs
    return req.CreateResponse(HttpStatusCode.OK);
    ```

A função concluída é mostrada abaixo.

```cs
public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                                "get", "post",
                                                                Route = null)]HttpRequestMessage req,
                                                    TraceWriter log)
{
    log.Info("C# HTTP trigger function processed a request.");
    PostData data = await req.Content.ReadAsAsync<PostData>();
    string url = $"https://www.google.com/maps/search/?api=1&query={data.Latitude},{data.Longitude}";
    log.Info($"URL created - {url}");
    return req.CreateResponse(HttpStatusCode.OK);
}
```

## <a name="run-the-azure-function-locally"></a>Executar a função do Azure localmente

As funções podem ser executadas localmente com uma conta de armazenamento local e o runtime das Funções do Azure local. Este runtime local permite-lhe testar a sua função antes de o implementar no Azure.

1. Clique com o botão direito do rato no projeto `ImHere.Functions` no explorador de soluções e, em seguida, selecione *Configurar como Projeto de Arranque*.

2. No menu *Depurar*, selecione *Iniciar Sem Depuração*. O runtime local das Funções do Azure será lançado dentro de uma janela de consola e irá iniciar a sua função, ao escutar numa porta disponível no `localhost`.

    ![A função do Azure em execução localmente](../media/5-function-running-locally.png)

3. Tome nota da porta que a função está a escutar. Irá precisar da unidade seguinte para testar a aplicação móvel. Na imagem acima, a função está a escutar na porta **7071**.

    ```sh
    Listening on http://localhost:7071/
    ```

4. Deixe a função em execução para que possa testar a aplicação móvel na unidade seguinte.

## <a name="summary"></a>Resumo

Nessa unidade, aprendeu a criar um projeto das Funções do Azure no Visual Studio, adicionou um projeto partilhado com um objeto de dados para ser partilhado entre a aplicação móvel e a função, e aprendeu a criar uma implementação básica da função para anular a serialização de dados passados. Também aprendeu a executar localmente uma função do Azure. Na unidade seguinte, irá chamar a função do Azure a partir da aplicação móvel.