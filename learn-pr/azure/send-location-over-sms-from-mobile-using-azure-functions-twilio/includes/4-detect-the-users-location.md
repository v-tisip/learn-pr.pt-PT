A aplicação tem uma interface de utilizador e um ViewModel. Nesta unidade, vai adicionar a pesquisa de localizações ao ViewModel com o Xamarin.Essentials.

## <a name="enable-location-permissions"></a>Ativar as permissões de localização

Todas as plataformas móveis têm segurança no que diz respeito às informações do utilizador e a determinado hardware, como a câmara, a biblioteca de fotografias e a localização do utilizador. Para que uma aplicação possa aceder à localização do utilizador, este terá de dar permissão: ao conceder implicitamente essas permissões na altura da instalação ou ao optar por conceder a permissão no momento da execução. Quando vê uma aplicação UWP na loja, a listagem mostrará as permissões necessárias para aceder à aplicação. Ao instalar a aplicação, concede implicitamente permissão. Estas permissões são configuradas num ficheiro de manifesto da aplicação.

1. No projeto da aplicação `ImHere.UWP`, abra o ficheiro `Package.appxmanifest`.

2. Vá para o separador **Capacidades** e verifique a capacidade *Localização*.

    ![O separador de capacidades da UWP](../media/4-uwp-location-capability.png)

> Se quiser suporte para Android ou iOS, as permissões terão de ser configuradas de forma diferente. Esse procedimento é detalhado nos [documentos de Geolocalização do Xamarin.Essentials](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=android#getting-started).

## <a name="query-for-the-users-location"></a>Consulta da localização do utilizador

Existem duas formas de obter a localização do utilizador: a última conhecida ou a atual. A obtenção da localização atual pode demorar algum tempo, uma vez que o dispositivo poderá ter de estabelecer uma ligação GPS e esperar até que a localização exata seja obtida. A forma mais rápida é obter a última localização detetada pelo dispositivo conhecida. A última localização conhecida é potencialmente menos precisa, mas é uma chamada muito mais rápida. As localizações são fornecidas com a latitude e a longitude em [graus decimais](https://en.wikipedia.org/wiki/Decimal_degrees) e a altitude do dispositivo em metros acima do nível do mar.

1. Abra a classe `MainViewModel` no projeto .NET `ImHere` padrão.

2. No método `SendLocation`, crie uma chamada para o método estático `GetLastKnownLocationAsync` na classe `Geolocation` no espaço de nomes `Xamarin.Essentials`.

    ```cs
    Location location = await Geolocation.GetLastKnownLocationAsync();
    ```

3. Atualize a propriedade `Message` com a localização do utilizador, caso encontre alguma.

    ```cs
    if (location != null)
    {
        Message = $"Location found: {location.Latitude}, {location.Longitude}.";
    }
    ```

O código completo para este método é apresentado abaixo.

```cs
async Task SendLocation()
{
    Location location = await Geolocation.GetLastKnownLocationAsync();

    if (location != null)
    {
        Message = $"Location found: {location.Latitude}, {location.Longitude}.";
    }
}
```

Execute a aplicação e clique no botão **Enviar Localização** para ver a localização na interface do utilizador.

![A aplicação em execução a mostrar a localização do utilizador](../media/4-running-app-showing-location.png)

> Esta aplicação utiliza a última localização conhecida. Numa aplicação com qualidade de produção, poderá querer obter a localização exata atual dentro de um limite de tempo e, se nenhuma for encontrada, reverter para a última conhecida. Pode ler mais sobre como fazê-lo nos [documentos de Geolocalização do Xamarin.Essentials](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=uwp#using-geolocation). Esta aplicação não tem processamento de erros. Numa aplicação com qualidade de produção, deve processar as possíveis exceções, por exemplo, se a localização não estava disponível e tiver sido emitida uma exceção.

## <a name="summary"></a>Resumo

Nesta unidade, aprendeu a utilizar o Xamarin.Essentials para obter a localização do utilizador. Na unidade seguinte, vai criar uma função do Azure para atuar como um back-end da aplicação móvel.