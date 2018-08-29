Neste momento, a aplicação móvel é uma aplicação "Hello World" simples. Nesta unidade, vai adicionar a IU e alguma lógica de aplicação básica.

A IU da aplicação consiste em:

* Num controlo de entrada de texto para introduzir alguns números de telefone.
* Num botão para enviar a sua localização para esses números através de uma função do Azure.
* Numa etiqueta que mostra uma mensagem ao utilizador sobre o estado atual, como a localização a enviar e a localização enviada com êxito.

O Xamarin.Forms suporta um padrão de design denominado Model-View-ViewModel (MVVM). Pode ler mais sobre o MVVM nos [documentos do Xamarin MVVM](https://docs.microsoft.com/xamarin/xamarin-forms/enterprise-application-patterns/mvvm), mas a essência do mesmo é que cada página (View) tem um ViewModel que expõe as propriedades e o comportamento.

As propriedades do ViewModel estão "vinculadas" aos componentes na IU por nome e este enlace sincroniza os dados entre o View e o ViewModel. Por exemplo, uma propriedade `string` num ViewModel denominada `Name` pode estar vinculada à propriedade `Text` de um controlo de entrada de texto na IU. O controlo de entrada de texto mostra o valor na propriedade `Name` e, quando o utilizador altera o texto na IU, a propriedade `Name` é atualizada. Se o valor da propriedade `Name` for alterada no ViewModel, é gerado um evento para informar a IU para atualizar.

O comportamento do ViewModel é exposto como propriedades de comando, um comando como objeto que encapsula uma ação executada quando o comando é invocado. Estes comandos estão vinculados por nome a controlos como botões e tocar num botão invocará o comando.

## <a name="create-a-base-viewmodel"></a>Criar um ViewModel base

Todos os ViewModels implementam a interface `INotifyPropertyChanged`. Esta interface possui um único evento, `PropertyChanged`, que é utilizado para notificar a IU de todas as atualizações. Este evento tem argumentos com o nome da propriedade que foi alterada. É prática comum criar uma classe ViewModel base ao implementar esta interface e ao fornecer alguns métodos auxiliares.

1. Crie uma nova classe no projeto .NET padrão `ImHere` chamada `BaseViewModel` ao clicar com o botão direito do rato no projeto e, em seguida, ao selecionar *Adicionar->Classe...*. Atribua um nome à nova classe "BaseViewModel" e clique em **Adicionar**.

2. Torne a classe `public` e derivada de `INotifyPropertyChanged`. Terá de adicionar uma diretiva para `System.ComponentModel`.

3. Implemente a interface `INotifyPropertyChanged` ao adicionar o evento `PropertyChanged`:

    ```cs
    public event PropertyChangedEventHandler PropertyChanged;
    ```

4. O padrão comum para as propriedades do ViewModel é ter uma propriedade pública com um campo de apoio privado. No setter da propriedade, o campo de apoio é comparado ao novo valor. Se o novo valor for diferente do campo de apoio, este é atualizado e é gerado o evento `PropertyChanged`. Esta lógica é fácil de utilizar num método, por isso, adicione o método `Set`. Terá de adicionar uma diretiva para o espaço de nomes `System.Runtime.CompilerServices`.

    ```cs
    protected void Set<T>(ref T field, T value, [CallerMemberName] string propertyName = null)
    {
        if (Equals(field, value)) return;
        field = value;
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
    }
    ```

    Este método faz referência ao campo de apoio, ao novo valor e ao nome da propriedade. Se o campo não for alterado, o método volta, caso contrário, o campo é atualizado e é gerado o evento `PropertyChanged`. O parâmetro `propertyName` no método `Set` é um parâmetro predefinido e está marcado com o atributo `CallerMemberName`. Quando este método é chamado a partir de um setter de propriedade, este parâmetro é normalmente deixado como valor predefinido. Em seguida, o compilador vai definir automaticamente o valor do parâmetro para ser o nome da propriedade chamada.

O código completo para esta classe é apresentado abaixo.

```cs
using System.ComponentModel;
using System.Runtime.CompilerServices;

namespace ImHere
{
    public class BaseViewModel : INotifyPropertyChanged
    {
        public event PropertyChangedEventHandler PropertyChanged;

        protected void Set<T>(ref T field, T value, [CallerMemberName] string propertyName = null)
        {
            if (Equals(field, value)) return;
            field = value;
            PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
        }
    }
}
```

## <a name="create-a-viewmodel-for-the-page"></a>Criar um ViewModel para a página

`MainPage` terá um controlo de entrada de texto para números de telefone e uma etiqueta para apresentar uma mensagem. Estes controlos estarão vinculados às propriedades num ViewModel.

1. Crie uma classe denominada `MainViewModel` no projeto .NET padrão `ImHere`.

2. Torne esta classe pública e derivada de `BaseViewModel`.

3. Adicione duas propriedades `string`, `PhoneNumbers` e `Message`, cada uma com um campo de apoio. No setter da propriedade, utilize o método da classe base `Set` para atualizar o valor e elevar o evento `PropertyChanged`.

   ```cs
    string message = "";
    public string Message
    {
        get => message;
        set => Set(ref message, value);
    }

    string phoneNumbers = "";
    public string PhoneNumbers
    {
        get => phoneNumbers;
        set => Set(ref phoneNumbers, value);
    }
   ```

4. Adicione uma propriedade de comando só de leitura denominada `SendLocationCommand`. Este comando terá um tipo de `ICommand` a partir do espaço de nomes `System.Windows.Input`.

    ```cs
    public ICommand SendLocationCommand { get; }
    ```

5. Adicione um construtor à classe e inicialize `SendLocationCommand` como um novo `Command` partir do espaço de nomes `Xamarin.Forms`. O construtor para este comando utiliza `Action` para executar quando o comando é invocado, pelo que crie um método `async` denominado `SendLocation` e transmita uma função lambda que `await` esta chamada para o construtor. O corpo do método `SendLocation` será implementado nas unidades mais adiante neste módulo. Terá de adicionar uma diretiva para o espaço de nomes `System.Threading.Tasks` conseguir devolver `Task`.

    ```cs
    public MainViewModel()
    {
        SendLocationCommand = new Command(async () => await SendLocation());
    }

    async Task SendLocation()
    {
    }
    ```

O código para esta classe é apresentado abaixo.

```cs
using System.Threading.Tasks;
using System.Windows.Input;
using Xamarin.Forms;

namespace ImHere
{
    public class MainViewModel : BaseViewModel
    {
        string message = "";
        public string Message
        {
            get => message;
            set => Set(ref message, value);
        }

        string phoneNumbers = "";
        public string PhoneNumbers
        {
            get => phoneNumbers;
            set => Set(ref phoneNumbers, value);
        }

        public MainViewModel()
        {
            SendLocationCommand = new Command(async () => await SendLocation());
        }

        public ICommand SendLocationCommand { get; }

        async Task SendLocation()
        {
        }
    }
}
```

## <a name="create-the-user-interface"></a>Criar a interface de utilizador

As IUs do Xamarin.Forms podem ser criadas com XAML.

1. Abra o ficheiro `MainPage.xaml` a partir do projeto `ImHere`. A página será aberta no editor de XAML.

    NOTA: o projeto `ImHere.UWP` também contém um ficheiro chamado `MainPage.xaml`. Certifique-se de que está a editar o existente na biblioteca .NET padrão.

2. Antes de poder vincular controlos às propriedades num ViewModel, é necessário definir uma instância do ViewModel como contexto de enlace da página. Adicione o seguinte XAML no `ContentPage` de nível superior.

    ```xml
    <ContentPage.BindingContext>
        <local:MainViewModel/>
    </ContentPage.BindingContext>
    ```

3. Elimine o conteúdo de `StackLayout` e adicione algum preenchimento para ajudar a melhorar o aspeto da IU.

    ```xml
    <StackLayout Padding="20">
    </StackLayout>
    ```

4. Adicione um controlo `Editor` que o utilizador possa utilizar para adicionar números de telefone a `StackLayout`, com um `Label` acima para descrever para que serve o controlo de entrada. A pilha de `StackLayout` é controlada horizontal ou verticalmente na ordem pela qual os controlos são adicionados, pelo que adicionar `Label` primeiro vai colocá-la acima de `Editor`. Os controlos de `Editor` são de entrada com várias linhas, o que permite ao utilizador introduzir vários números de telefone, um por linha.

    ```xml
    <StackLayout Padding="20">
        <Label Text="Phone numbers to send to:" HorizontalOptions="Center"/>
        <Editor Text="{Binding PhoneNumbers}" HeightRequest="100"/>
    </StackLayout>
    ```

    A propriedade `Text` em `Editor` está vinculada à propriedade `PhoneNumbers` em `MainViewModel`. A sintaxe de enlace é definir o valor da propriedade como `"{Binding <property name>}"`. As chavetas indicam ao compilador XAML que este valor é especial e deve ser tratado de forma diferente de uma simples propriedade `string`.

5. Adicione `Button` para enviar a localização do utilizador por baixo de `Editor`.

    ```xml
    <Button Text="Send Location" BackgroundColor="Blue" TextColor="White"
            Command="{Binding SendLocationCommand}" />
    ```

    A propriedade `Command` está vinculada ao comando `SendLocationCommand` no ViewModel. Quando tocar no botão, o comando será executado.

6. Adicione `Label` para mostrar a mensagem de estado por baixo de `Button`.

    ```xml
    <Label Text="{Binding Message}"
           HorizontalOptions="Center" VerticalOptions="CenterAndExpand" />
    ```

O código completo para esta página é apresentado abaixo.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:ImHere"
             x:Class="ImHere.MainPage">
    <ContentPage.BindingContext>
        <local:MainViewModel/>
    </ContentPage.BindingContext>
    <StackLayout Padding="20">
        <Label Text="Phone numbers to send to:" HorizontalOptions="Center"/>
        <Editor Text="{Binding PhoneNumbers}" HeightRequest="100"/>
        <Button Text="Send Location" BackgroundColor="Blue" TextColor="White"
                Command="{Binding SendLocationCommand}" />
        <Label Text="{Binding Message}"
               HorizontalOptions="Center" VerticalOptions="CenterAndExpand" />
    </StackLayout>
</ContentPage>
```

Execute a aplicação para ver a nova IU. Se quiser validar os enlaces neste momento, pode fazê-ao adicionar pontos de interrupção às propriedades ou ao método `SendLocation`.

![A nova IU da aplicação](../media/3-new-ui.png)

## <a name="summary"></a>Resumo

Nesta unidade, aprendeu a criar a IU para a aplicação com XAML, juntamente com um ViewModel para processar a lógica das aplicações. Também aprendeu a vincular o ViewModel à IU. Na unidade seguinte, vai adicionar pesquisa de localização ao ViewModel.