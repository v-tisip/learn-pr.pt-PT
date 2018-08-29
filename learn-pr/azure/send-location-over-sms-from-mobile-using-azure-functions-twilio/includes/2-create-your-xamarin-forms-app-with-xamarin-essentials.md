A aplicação que estiver a criar é uma aplicação móvel para várias plataformas, que se comunica com uma função do Azure para partilhar a sua localização. É nesta unidade, que vai criar a aplicação móvel em branco, utilizando o Visual Studio, e instalar um pacote NuGet que tem uma API para obter a localização do utilizador.

## <a name="create-the-xamarinforms-project"></a>Criar o projeto Xamarin.Forms

1. No Visual Studio, selecione *Ficheiro->Novo->Projeto...*

2. A partir da vista de árvore apresentada à esquerda, selecione *Visual C#->Para várias plataformas* e, em seguida, selecione *Aplicação Móvel (Xamarin.Forms)* a partir do painel do centro.

3. Atribua o nome "EstouAqui"à solução.

4. Escolha uma localização adequada para a solução.

    > Se estiver a executar este módulo localmente no Windows e estiver a planear a criação para Android, certifique-se de que o caminho é o mais curto possível. Existem limitações para o comprimento do caminho com o SDK Android e o caminho de raiz deve ser o mais curto possível.

5. Clique em **OK**.

    ![Caixa de diálogo Nova Solução](../media/2-new-solution-dialog.png)

6. Na caixa de diálogo da**Aplicação Móvel Para Várias Plataformas**, selecione o modelo de *Aplicação em Branco*.

7. Para este módulo vai criar uma aplicação UWP. Assim, desmarque as opções iOS e Android e deixe UWP marcada.

    > Se estiver a executar localmente, pode deixar Android marcado, uma vez que o Android SDK é instalado como parte da carga de trabalho *Mobile Development With .NET* dentro do Visual Studio. Se também pretender criar para iOS, terá da emparelhar com um agente de compilação do macOS. Pode ler mais sobre este tema nos [documentos do Xamarin iOS](https://docs.microsoft.com/xamarin/ios/get-started/installation/windows/connecting-to-mac/).

8. Para a *Estratégia de Partilha do Código*, selecione **.NET Standard**.

9. Clique em **OK**.

    ![Caixa de diálogo para configurar a nova solução](../media/2-configure-solution-dialog.png)

O Visual Studio criará dois projetos para si: uma aplicação UWP denominada `ImHere.UWP` e uma biblioteca padrão .NET, `ImHere`. As aplicações Xamarin.Forms são constituídas por duas partes, um ou mais projetos de aplicação específicos da plataforma e uma (ou mais) bibliotecas padrão .NET. Os projetos de aplicação específicos da plataforma contêm o código específico da plataforma necessário para executar uma aplicação na plataforma relevante. Estes projetos iniciam, em seguida, uma aplicação Xamarin.Forms, que é definida numa biblioteca de padrão .NET para várias plataformas. A aplicação é criada utilizando um código para várias plataformas e, durante o tempo de execução, qualquer interface de utilizador que criar é convertida nos componentes relevantes de interface de utilizador específicos da plataforma.

## <a name="adding-xamarinessentials"></a>Adicionar Xamarin.Essentials

As plataformas UWP, Android e iOS fornecem várias capacidades semelhantes que tiram proveito do sistema operativo e hardware. Apesar destas semelhanças, as APIs são muito diferentes. Utilizar estas APIs, a partir do código para várias plataformas, requer a criação de código específico da plataforma nos seus projetos de aplicação que vai expor para as suas bibliotecas padrão .NET. [Xamarin.Essentials](https://docs.microsoft.com/xamarin/essentials/) é um pacote NuGet que fornece uma abstração para várias plataformas de várias APIs, incluindo APIs de geolocalização que vai utilizar na sua aplicação para obter a localização do utilizador.

1. Clique com o botão direito do rato na solução `ImHere` do Explorador de Soluções do Visual Studio e selecione  *Gerir Pacotes NuGet para a Solução...*

2. Selecione o separador **Procurar** e procure "Xamarin.Essentials". Este pacote está atualmente disponível como uma versão de pré-lançamento do pacote NuGet. Consulte a *caixa de pré-lançamento* incluída.

3. Selecione o pacote NuGet do **Xamarin.Essentials**.

4. Marque todos os seus projetos na lista de projeto, no lado direito.

5. Clique no botão **Instalar** para instalar o pacote NuGet. Terá de aceitar a licença para continuar.

    ![Adicionar o pacote NuGet do Xamarin.Essentials a todos os projetos na solução](../media/2-add-essentials-nuget.png)

    > Se estiver a executar este módulo localmente e o seu objetivo for Android, terá de fazer alguma configuração adicional. Para mais informações, consulte os [documentos de Introdução do Xamarin.Essentials](https://docs.microsoft.com/xamarin/essentials/get-started?context=xamarin%2Fios&tabs=windows%2Candroid).

## <a name="building-and-running-the-app"></a>Criar e executar a aplicação

1. Clique com o botão direito no projeto `ImHere.UWP` no Explorador de Soluções e selecione *Configurar como Projeto de Arranque*.

2. Defina a configuração de compilação para **Depurar**, a plataforma para **x86**e a execução do dispositivo para **Máquina Local**.

    ![Definir a configuração Depuração x86 para executar no dispositivo local](../media/2-debug-configuration.png)

3. Comece a depuração da aplicação.

    ![Aplicação em execução](../media/2-debuging-app.png)

## <a name="summary"></a>Resumo

Nesta unidade, criou uma nova aplicação móvel Xamarin.Form para várias plataformas e adicionou o pacote NuGet do Xamarin.Essentials. Em seguida, vai aprender a criar a interface de utilizador e a lógica da aplicação móvel.