<span data-ttu-id="e87f7-101">Neste momento, a aplicação móvel é uma aplicação "Hello World" simples.</span><span class="sxs-lookup"><span data-stu-id="e87f7-101">At this point, the mobile app is a simple "Hello World" app.</span></span> <span data-ttu-id="e87f7-102">Nesta unidade, vai adicionar a IU e alguma lógica de aplicação básica.</span><span class="sxs-lookup"><span data-stu-id="e87f7-102">In this unit, you add the UI and some basic application logic.</span></span>

<span data-ttu-id="e87f7-103">A IU da aplicação consiste em:</span><span class="sxs-lookup"><span data-stu-id="e87f7-103">The UI for the app will consist of:</span></span>

* <span data-ttu-id="e87f7-104">Num controlo de entrada de texto para introduzir alguns números de telefone.</span><span class="sxs-lookup"><span data-stu-id="e87f7-104">A text-entry control to enter some phone numbers.</span></span>
* <span data-ttu-id="e87f7-105">Num botão para enviar a sua localização para esses números através de uma função do Azure.</span><span class="sxs-lookup"><span data-stu-id="e87f7-105">A button to send your location to those numbers using an Azure function.</span></span>
* <span data-ttu-id="e87f7-106">Numa etiqueta que mostra uma mensagem ao utilizador sobre o estado atual, como a localização a enviar e a localização enviada com êxito.</span><span class="sxs-lookup"><span data-stu-id="e87f7-106">A label that will show a message to the user of the current status, such as the location being sent and location sent successfully.</span></span>

<span data-ttu-id="e87f7-107">O Xamarin.Forms suporta um padrão de design denominado Model-View-ViewModel (MVVM).</span><span class="sxs-lookup"><span data-stu-id="e87f7-107">Xamarin.Forms supports a design pattern called Model-View-ViewModel (MVVM).</span></span> <span data-ttu-id="e87f7-108">Pode ler mais sobre o MVVM nos [documentos do Xamarin MVVM](https://docs.microsoft.com/xamarin/xamarin-forms/enterprise-application-patterns/mvvm), mas a essência do mesmo é que cada página (View) tem um ViewModel que expõe as propriedades e o comportamento.</span><span class="sxs-lookup"><span data-stu-id="e87f7-108">You can read more about MVVM in the [Xamarin MVVM docs](https://docs.microsoft.com/xamarin/xamarin-forms/enterprise-application-patterns/mvvm), but the essence of it is, each page (View) has a ViewModel that exposes properties and behavior.</span></span>

<span data-ttu-id="e87f7-109">As propriedades do ViewModel estão "vinculadas" aos componentes na IU por nome e este enlace sincroniza os dados entre o View e o ViewModel.</span><span class="sxs-lookup"><span data-stu-id="e87f7-109">ViewModel properties are 'bound' to components on the UI by name, and this binding synchronizes data between the View and ViewModel.</span></span> <span data-ttu-id="e87f7-110">Por exemplo, uma propriedade `string` num ViewModel denominada `Name` pode estar vinculada à propriedade `Text` de um controlo de entrada de texto na IU.</span><span class="sxs-lookup"><span data-stu-id="e87f7-110">For example, a `string` property on a ViewModel called `Name` could be bound to the `Text` property of a text-entry control on the UI.</span></span> <span data-ttu-id="e87f7-111">O controlo de entrada de texto mostra o valor na propriedade `Name` e, quando o utilizador altera o texto na IU, a propriedade `Name` é atualizada.</span><span class="sxs-lookup"><span data-stu-id="e87f7-111">The text-entry control shows the value in the `Name` property and, when the user changes the text in the UI, the `Name` property is updated.</span></span> <span data-ttu-id="e87f7-112">Se o valor da propriedade `Name` for alterada no ViewModel, é gerado um evento para informar a IU para atualizar.</span><span class="sxs-lookup"><span data-stu-id="e87f7-112">If the value of the `Name` property is changed in the ViewModel, an event is raised to tell the UI to update.</span></span>

<span data-ttu-id="e87f7-113">O comportamento do ViewModel é exposto como propriedades de comando, um comando como objeto que encapsula uma ação executada quando o comando é invocado.</span><span class="sxs-lookup"><span data-stu-id="e87f7-113">ViewModel behavior is exposed as command properties, a command being an object that wraps an action that is executed when the command is invoked.</span></span> <span data-ttu-id="e87f7-114">Estes comandos estão vinculados por nome a controlos como botões e tocar num botão invocará o comando.</span><span class="sxs-lookup"><span data-stu-id="e87f7-114">These commands are bound by name to controls like buttons, and tapping a button will invoke the command.</span></span>

## <a name="create-a-base-viewmodel"></a><span data-ttu-id="e87f7-115">Criar um ViewModel base</span><span class="sxs-lookup"><span data-stu-id="e87f7-115">Create a base ViewModel</span></span>

<span data-ttu-id="e87f7-116">Todos os ViewModels implementam a interface `INotifyPropertyChanged`.</span><span class="sxs-lookup"><span data-stu-id="e87f7-116">ViewModels all implement the `INotifyPropertyChanged` interface.</span></span> <span data-ttu-id="e87f7-117">Esta interface possui um único evento, `PropertyChanged`, que é utilizado para notificar a IU de todas as atualizações.</span><span class="sxs-lookup"><span data-stu-id="e87f7-117">This interface has a single event, `PropertyChanged`, which is used to notify the UI of any updates.</span></span> <span data-ttu-id="e87f7-118">Este evento tem argumentos com o nome da propriedade que foi alterada.</span><span class="sxs-lookup"><span data-stu-id="e87f7-118">This event has event args that contain the name of the property that has changed.</span></span> <span data-ttu-id="e87f7-119">É prática comum criar uma classe ViewModel base ao implementar esta interface e ao fornecer alguns métodos auxiliares.</span><span class="sxs-lookup"><span data-stu-id="e87f7-119">It's common practice to create a base ViewModel class implementing this interface and providing some helper methods.</span></span>

1. <span data-ttu-id="e87f7-120">Crie uma nova classe no projeto .NET padrão `ImHere` chamada `BaseViewModel` ao clicar com o botão direito do rato no projeto e, em seguida, ao selecionar *Adicionar->Classe...*. Atribua um nome à nova classe "BaseViewModel" e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e87f7-120">Create a new class in the `ImHere` .NET standard project called `BaseViewModel` by right-clicking on the project, and then selecting *Add->Class...*. Name the new class "BaseViewModel" and click **Add**.</span></span>

2. <span data-ttu-id="e87f7-121">Torne a classe `public` e derivada de `INotifyPropertyChanged`.</span><span class="sxs-lookup"><span data-stu-id="e87f7-121">Make the class `public` and derive from `INotifyPropertyChanged`.</span></span> <span data-ttu-id="e87f7-122">Terá de adicionar uma diretiva para `System.ComponentModel`.</span><span class="sxs-lookup"><span data-stu-id="e87f7-122">You'll need to add a using directive for `System.ComponentModel`.</span></span>

3. <span data-ttu-id="e87f7-123">Implemente a interface `INotifyPropertyChanged` ao adicionar o evento `PropertyChanged`:</span><span class="sxs-lookup"><span data-stu-id="e87f7-123">Implement the `INotifyPropertyChanged` interface by adding the `PropertyChanged` event:</span></span>

    ```cs
    public event PropertyChangedEventHandler PropertyChanged;
    ```

4. <span data-ttu-id="e87f7-124">O padrão comum para as propriedades do ViewModel é ter uma propriedade pública com um campo de apoio privado.</span><span class="sxs-lookup"><span data-stu-id="e87f7-124">The common pattern for ViewModel properties is to have a public property with a private backing field.</span></span> <span data-ttu-id="e87f7-125">No setter da propriedade, o campo de apoio é comparado ao novo valor.</span><span class="sxs-lookup"><span data-stu-id="e87f7-125">In the property setter, the backing field is checked against the new value.</span></span> <span data-ttu-id="e87f7-126">Se o novo valor for diferente do campo de apoio, este é atualizado e é gerado o evento `PropertyChanged`.</span><span class="sxs-lookup"><span data-stu-id="e87f7-126">If the new value is different to the backing field, the backing field is updated and the `PropertyChanged` event is raised.</span></span> <span data-ttu-id="e87f7-127">Esta lógica é fácil de utilizar num método, por isso, adicione o método `Set`.</span><span class="sxs-lookup"><span data-stu-id="e87f7-127">This logic is easy to factor out into a method, so add the `Set` method.</span></span> <span data-ttu-id="e87f7-128">Terá de adicionar uma diretiva para o espaço de nomes `System.Runtime.CompilerServices`.</span><span class="sxs-lookup"><span data-stu-id="e87f7-128">You'll need to add a using directive for the `System.Runtime.CompilerServices` namespace.</span></span>

    ```cs
    protected void Set<T>(ref T field, T value, [CallerMemberName] string propertyName = null)
    {
        if (Equals(field, value)) return;
        field = value;
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
    }
    ```

    <span data-ttu-id="e87f7-129">Este método faz referência ao campo de apoio, ao novo valor e ao nome da propriedade.</span><span class="sxs-lookup"><span data-stu-id="e87f7-129">This method takes a reference to the backing field, the new value, and the property name.</span></span> <span data-ttu-id="e87f7-130">Se o campo não for alterado, o método volta, caso contrário, o campo é atualizado e é gerado o evento `PropertyChanged`.</span><span class="sxs-lookup"><span data-stu-id="e87f7-130">If the field hasn't changed, the method returns, otherwise, the field is updated and the `PropertyChanged` event is raised.</span></span> <span data-ttu-id="e87f7-131">O parâmetro `propertyName` no método `Set` é um parâmetro predefinido e está marcado com o atributo `CallerMemberName`.</span><span class="sxs-lookup"><span data-stu-id="e87f7-131">The `propertyName` parameter on the `Set` method is a default parameter and is marked with the `CallerMemberName` attribute.</span></span> <span data-ttu-id="e87f7-132">Quando este método é chamado a partir de um setter de propriedade, este parâmetro é normalmente deixado como valor predefinido.</span><span class="sxs-lookup"><span data-stu-id="e87f7-132">When this method is called from a property setter, this parameter is normally left as the default value.</span></span> <span data-ttu-id="e87f7-133">Em seguida, o compilador vai definir automaticamente o valor do parâmetro para ser o nome da propriedade chamada.</span><span class="sxs-lookup"><span data-stu-id="e87f7-133">The compiler will then automatically set the parameter value to be the name of the calling property.</span></span>

<span data-ttu-id="e87f7-134">O código completo para esta classe é apresentado abaixo.</span><span class="sxs-lookup"><span data-stu-id="e87f7-134">The full code for this class is below.</span></span>

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

## <a name="create-a-viewmodel-for-the-page"></a><span data-ttu-id="e87f7-135">Criar um ViewModel para a página</span><span class="sxs-lookup"><span data-stu-id="e87f7-135">Create a ViewModel for the page</span></span>

<span data-ttu-id="e87f7-136">`MainPage` terá um controlo de entrada de texto para números de telefone e uma etiqueta para apresentar uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="e87f7-136">The `MainPage` will have a text-entry control for phone numbers and a label to display a message.</span></span> <span data-ttu-id="e87f7-137">Estes controlos estarão vinculados às propriedades num ViewModel.</span><span class="sxs-lookup"><span data-stu-id="e87f7-137">These controls will be bound to properties on a ViewModel.</span></span>

1. <span data-ttu-id="e87f7-138">Crie uma classe denominada `MainViewModel` no projeto .NET padrão `ImHere`.</span><span class="sxs-lookup"><span data-stu-id="e87f7-138">Create a class called `MainViewModel` in the `ImHere` .NET standard project.</span></span>

2. <span data-ttu-id="e87f7-139">Torne esta classe pública e derivada de `BaseViewModel`.</span><span class="sxs-lookup"><span data-stu-id="e87f7-139">Make this class public and derive from `BaseViewModel`.</span></span>

3. <span data-ttu-id="e87f7-140">Adicione duas propriedades `string`, `PhoneNumbers` e `Message`, cada uma com um campo de apoio.</span><span class="sxs-lookup"><span data-stu-id="e87f7-140">Add two `string` properties, `PhoneNumbers` and `Message`, each with a backing field.</span></span> <span data-ttu-id="e87f7-141">No setter da propriedade, utilize o método da classe base `Set` para atualizar o valor e elevar o evento `PropertyChanged`.</span><span class="sxs-lookup"><span data-stu-id="e87f7-141">In the property setter, use the base class `Set` method to update the value and raise the `PropertyChanged` event.</span></span>

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

4. <span data-ttu-id="e87f7-142">Adicione uma propriedade de comando só de leitura denominada `SendLocationCommand`.</span><span class="sxs-lookup"><span data-stu-id="e87f7-142">Add a read-only command property called `SendLocationCommand`.</span></span> <span data-ttu-id="e87f7-143">Este comando terá um tipo de `ICommand` a partir do espaço de nomes `System.Windows.Input`.</span><span class="sxs-lookup"><span data-stu-id="e87f7-143">This command will have a type of `ICommand` from the `System.Windows.Input` namespace.</span></span>

    ```cs
    public ICommand SendLocationCommand { get; }
    ```

5. <span data-ttu-id="e87f7-144">Adicione um construtor à classe e inicialize `SendLocationCommand` como um novo `Command` partir do espaço de nomes `Xamarin.Forms`.</span><span class="sxs-lookup"><span data-stu-id="e87f7-144">Add a constructor to the class, and in this constructor, initialize the `SendLocationCommand` as a new `Command` from the `Xamarin.Forms` namespace.</span></span> <span data-ttu-id="e87f7-145">O construtor para este comando utiliza `Action` para executar quando o comando é invocado, pelo que crie um método `async` denominado `SendLocation` e transmita uma função lambda que `await` esta chamada para o construtor.</span><span class="sxs-lookup"><span data-stu-id="e87f7-145">The constructor for this command takes an `Action` to run when the command is invoked, so create an `async` method called `SendLocation` and pass a lambda function that `await`s this call to the constructor.</span></span> <span data-ttu-id="e87f7-146">O corpo do método `SendLocation` será implementado nas unidades mais adiante neste módulo.</span><span class="sxs-lookup"><span data-stu-id="e87f7-146">The body of the `SendLocation` method will be implemented in later units in this module.</span></span> <span data-ttu-id="e87f7-147">Terá de adicionar uma diretiva para o espaço de nomes `System.Threading.Tasks` conseguir devolver `Task`.</span><span class="sxs-lookup"><span data-stu-id="e87f7-147">You'll need to add a using directive for the `System.Threading.Tasks` namespace to be able to return a `Task`.</span></span>

    ```cs
    public MainViewModel()
    {
        SendLocationCommand = new Command(async () => await SendLocation());
    }

    async Task SendLocation()
    {
    }
    ```

<span data-ttu-id="e87f7-148">O código para esta classe é apresentado abaixo.</span><span class="sxs-lookup"><span data-stu-id="e87f7-148">The code for this class is shown below.</span></span>

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

## <a name="create-the-user-interface"></a><span data-ttu-id="e87f7-149">Criar a interface de utilizador</span><span class="sxs-lookup"><span data-stu-id="e87f7-149">Create the user interface</span></span>

<span data-ttu-id="e87f7-150">As IUs do Xamarin.Forms podem ser criadas com XAML.</span><span class="sxs-lookup"><span data-stu-id="e87f7-150">Xamarin.Forms UIs can be built using XAML.</span></span>

1. <span data-ttu-id="e87f7-151">Abra o ficheiro `MainPage.xaml` a partir do projeto `ImHere`.</span><span class="sxs-lookup"><span data-stu-id="e87f7-151">Open the `MainPage.xaml` file from the `ImHere` project.</span></span> <span data-ttu-id="e87f7-152">A página será aberta no editor de XAML.</span><span class="sxs-lookup"><span data-stu-id="e87f7-152">The page will open in the XAML editor.</span></span>

    <span data-ttu-id="e87f7-153">NOTA: o projeto `ImHere.UWP` também contém um ficheiro chamado `MainPage.xaml`.</span><span class="sxs-lookup"><span data-stu-id="e87f7-153">NOTE - The `ImHere.UWP` project also contains a file called `MainPage.xaml`.</span></span> <span data-ttu-id="e87f7-154">Certifique-se de que está a editar o existente na biblioteca .NET padrão.</span><span class="sxs-lookup"><span data-stu-id="e87f7-154">Make sure you're editing the one in the .NET standard library.</span></span>

2. <span data-ttu-id="e87f7-155">Antes de poder vincular controlos às propriedades num ViewModel, é necessário definir uma instância do ViewModel como contexto de enlace da página.</span><span class="sxs-lookup"><span data-stu-id="e87f7-155">Before you can bind controls to properties on a ViewModel, you have to set an instance of the ViewModel as the binding context of the page.</span></span> <span data-ttu-id="e87f7-156">Adicione o seguinte XAML no `ContentPage` de nível superior.</span><span class="sxs-lookup"><span data-stu-id="e87f7-156">Add the following XAML inside the top-level `ContentPage`.</span></span>

    ```xml
    <ContentPage.BindingContext>
        <local:MainViewModel/>
    </ContentPage.BindingContext>
    ```

3. <span data-ttu-id="e87f7-157">Elimine o conteúdo de `StackLayout` e adicione algum preenchimento para ajudar a melhorar o aspeto da IU.</span><span class="sxs-lookup"><span data-stu-id="e87f7-157">Delete the contents of the `StackLayout` and add some padding inside it to help make the UI look better.</span></span>

    ```xml
    <StackLayout Padding="20">
    </StackLayout>
    ```

4. <span data-ttu-id="e87f7-158">Adicione um controlo `Editor` que o utilizador possa utilizar para adicionar números de telefone a `StackLayout`, com um `Label` acima para descrever para que serve o controlo de entrada.</span><span class="sxs-lookup"><span data-stu-id="e87f7-158">Add an `Editor` control that the user can use to add phone numbers to the `StackLayout`, with a `Label` above to describe what the entry control is for.</span></span> <span data-ttu-id="e87f7-159">A pilha de `StackLayout` é controlada horizontal ou verticalmente na ordem pela qual os controlos são adicionados, pelo que adicionar `Label` primeiro vai colocá-la acima de `Editor`.</span><span class="sxs-lookup"><span data-stu-id="e87f7-159">`StackLayout`'s stack child controls either horizontally or vertically in the order in which the controls are added, so adding the `Label` first will put it above the `Editor`.</span></span> <span data-ttu-id="e87f7-160">Os controlos de `Editor` são de entrada com várias linhas, o que permite ao utilizador introduzir vários números de telefone, um por linha.</span><span class="sxs-lookup"><span data-stu-id="e87f7-160">`Editor` controls are multi-line entry controls, allowing the user to enter multiple phone numbers, one per line.</span></span>

    ```xml
    <StackLayout Padding="20">
        <Label Text="Phone numbers to send to:" HorizontalOptions="Center"/>
        <Editor Text="{Binding PhoneNumbers}" HeightRequest="100"/>
    </StackLayout>
    ```

    <span data-ttu-id="e87f7-161">A propriedade `Text` em `Editor` está vinculada à propriedade `PhoneNumbers` em `MainViewModel`.</span><span class="sxs-lookup"><span data-stu-id="e87f7-161">The `Text` property on the `Editor` is bound to the `PhoneNumbers` property on the `MainViewModel`.</span></span> <span data-ttu-id="e87f7-162">A sintaxe de enlace é definir o valor da propriedade como `"{Binding <property name>}"`.</span><span class="sxs-lookup"><span data-stu-id="e87f7-162">The syntax for binding is to set the property value to `"{Binding <property name>}"`.</span></span> <span data-ttu-id="e87f7-163">As chavetas indicam ao compilador XAML que este valor é especial e deve ser tratado de forma diferente de uma simples propriedade `string`.</span><span class="sxs-lookup"><span data-stu-id="e87f7-163">The curly braces will tell the XAML compiler that this value is special and should be treated differently from a simple `string`.</span></span>

5. <span data-ttu-id="e87f7-164">Adicione `Button` para enviar a localização do utilizador por baixo de `Editor`.</span><span class="sxs-lookup"><span data-stu-id="e87f7-164">Add a `Button` to send the user's location below the `Editor`.</span></span>

    ```xml
    <Button Text="Send Location" BackgroundColor="Blue" TextColor="White"
            Command="{Binding SendLocationCommand}" />
    ```

    <span data-ttu-id="e87f7-165">A propriedade `Command` está vinculada ao comando `SendLocationCommand` no ViewModel.</span><span class="sxs-lookup"><span data-stu-id="e87f7-165">The `Command` property is bound to the `SendLocationCommand` command on the ViewModel.</span></span> <span data-ttu-id="e87f7-166">Quando tocar no botão, o comando será executado.</span><span class="sxs-lookup"><span data-stu-id="e87f7-166">When the button is tapped, the command will be executed.</span></span>

6. <span data-ttu-id="e87f7-167">Adicione `Label` para mostrar a mensagem de estado por baixo de `Button`.</span><span class="sxs-lookup"><span data-stu-id="e87f7-167">Add a `Label` to show the status message below the `Button`.</span></span>

    ```xml
    <Label Text="{Binding Message}"
           HorizontalOptions="Center" VerticalOptions="CenterAndExpand" />
    ```

<span data-ttu-id="e87f7-168">O código completo para esta página é apresentado abaixo.</span><span class="sxs-lookup"><span data-stu-id="e87f7-168">The full code for this page is below.</span></span>

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

<span data-ttu-id="e87f7-169">Execute a aplicação para ver a nova IU.</span><span class="sxs-lookup"><span data-stu-id="e87f7-169">Run the app to see the new UI.</span></span> <span data-ttu-id="e87f7-170">Se quiser validar os enlaces neste momento, pode fazê-ao adicionar pontos de interrupção às propriedades ou ao método `SendLocation`.</span><span class="sxs-lookup"><span data-stu-id="e87f7-170">If you want to validate the bindings at this point, you can do so by adding breakpoints to the properties or the `SendLocation` method.</span></span>

![A nova IU da aplicação](../media/3-new-ui.png)

## <a name="summary"></a><span data-ttu-id="e87f7-172">Resumo</span><span class="sxs-lookup"><span data-stu-id="e87f7-172">Summary</span></span>

<span data-ttu-id="e87f7-173">Nesta unidade, aprendeu a criar a IU para a aplicação com XAML, juntamente com um ViewModel para processar a lógica das aplicações.</span><span class="sxs-lookup"><span data-stu-id="e87f7-173">In this unit, you learned how to create the UI for the app using XAML, along with a ViewModel to handle the applications logic.</span></span> <span data-ttu-id="e87f7-174">Também aprendeu a vincular o ViewModel à IU.</span><span class="sxs-lookup"><span data-stu-id="e87f7-174">You also learned how to bind the ViewModel to the UI.</span></span> <span data-ttu-id="e87f7-175">Na unidade seguinte, vai adicionar pesquisa de localização ao ViewModel.</span><span class="sxs-lookup"><span data-stu-id="e87f7-175">In the next unit, you add location lookup to the ViewModel.</span></span>