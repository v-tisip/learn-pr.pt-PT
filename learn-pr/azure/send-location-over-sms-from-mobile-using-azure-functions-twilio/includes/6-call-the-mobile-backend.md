A aplicação móvel é executada e a versão inicial da função do Azure é criada. Nesta unidade, vai chamar a função do Azure a partir da aplicação móvel, ao passar a localização do utilizador e a lista de números de telefone para os quais o utilizador deseja enviar mensagens SMS.

## <a name="calling-the-azure-function-from-the-mobile-app"></a>Chamar a função do Azure a partir da aplicação móvel

1. Abra o `MainViewModel`.

2. Nesta classe, adicione um campo privado `HttpClient` chamado `client`. Vai precisar de adicionar uma referência ao espaço de nomes `System.Net.Http`.

    ```cs
    HttpClient client = new HttpClient();
    ```

3. Adicione um campo constante para o URL base da função. Defina-o como o endereço que o tempo de execução local das Funções do Azure está a escutar. Quando a função estiver implementada no Azure, esta constante poderá ser alterada para ser o URL do Azure.

    ```cs
    const string baseUrl = "http://localhost:7071";
    ```

4. No método `SendLocation`, depois de encontrar a localização, crie uma nova instância de `PostData` com a localização e a lista de números de telefone introduzidos pelo utilizador. Terá de adicionar uma diretiva using para o espaço de nomes `ImHere.Data`.

    ```cs
    PostData postData = new PostData
    {
        Latitude = location.Latitude,
        Longitude = location.Longitude,
        ToNumbers = PhoneNumbers.Split('\n')
    };
    ```

    > Este procedimento assume que os números de telefone foram introduzidos no formato correto, um por linha no controlo `Editor`. Numa aplicação com qualidade de produção, existiria validação em todo este procedimento para garantir que um ou mais números de telefone foram introduzidos e também no formato correto.

5. Para serializar o `PostData` como JSON, a maneira mais fácil é utilizar o pacote NuGet Newtonsoft.JSON. Adicione este pacote NuGet ao projeto `ImHere` da mesma forma que adicionou o Xamarin.Essentials numa unidade anterior.

6. Serialize o `PostData` para um `string` coma classe estática `JsonConvert`. Terá de adicionar uma diretiva using para o espaço de nomes `Newtonsoft.Json`. Codifique esta cadeia de caracteres numa classe `StringContent`, para que possa ser passada para a função Azure como JSON.

    ```cs
    string data = JsonConvert.SerializeObject(postData);
    StringContent content = new StringContent(data, Encoding.UTF8, "application/json");
    ```

7. Publique estes dados na função e obtenha o resultado.

   ```cs
    HttpResponseMessage result = await client.PostAsync($"{baseUrl}/api/SendLocation",
                                                        content);
   ```

   As funções do Azure são acedidas com `/api/<function name>`; por isso, supondo que a porta escolhida pelo tempo de execução local das Funções é 7071, a função `SendLocation` estará acessível em `http://localhost:7071/api/SendLocation`.

8. Consoante o resultado, mostre uma mensagem na interface de utilizador.

    ```cs
    if (result.IsSuccessStatusCode)
        Message = "Location sent successfully";
    else
        Message = $"Error - {result.ReasonPhrase}";
    ```

O código completo dos novos campos e o método `SendLocation` são apresentados abaixo.

```cs
HttpClient client = new HttpClient();
const string baseUrl = "http://localhost:7071";

async Task SendLocation()
{
    Location location = await Geolocation.GetLastKnownLocationAsync();

    if (location != null)
    {
        Message = $"Location found: {location.Latitude}, {location.Longitude}.";

        PostData postData = new PostData
        {
            Latitude = location.Latitude,
            Longitude = location.Longitude,
            ToNumbers = PhoneNumbers.Split('\n')
        };

        string data = JsonConvert.SerializeObject(postData);
        StringContent content = new StringContent(data, Encoding.UTF8, "application/json");
        HttpResponseMessage result = await client.PostAsync($"{baseUrl}/api/SendLocation",
                                                            content);

        if (result.IsSuccessStatusCode)
            Message = "Location sent successfully";
        else
            Message = $"Error - {result.ReasonPhrase}";
    }
}
```

## <a name="testing-it-out"></a>Teste

1. Verifique se a função do Azure ainda está em execução localmente e se a porta corresponde ao método `SendLocation`.

2. Defina a aplicação UWP como a aplicação de arranque e execute-a. Clique no botão **Enviar Localização**. Verá a saída na janela de consola do tempo de execução das Funções a mostrar a função a ser chamada e o registo que mostra o URL gerado.

    ![Saída da função que é chamada](../media/6-function-called.png)

3. Para testar a geração do URL, cole-o num browser na consola. Deverá mostrar a localização atual.

## <a name="summary"></a>Resumo

Nesta unidade, aprendeu como chamar uma função do Azure a partir da aplicação móvel. Esta chamada passa a localização do utilizador e os números de telefone que introduziram como JSON. Na unidade seguinte, vai vincular a função do Azure ao Twilio para enviar esta localização como uma mensagem SMS.