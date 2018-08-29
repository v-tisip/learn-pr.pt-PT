<span data-ttu-id="2c34c-101">Neste exercício, iremos criar uma função do Azure que aceita um pedido HTTP com uma única cadeia.</span><span class="sxs-lookup"><span data-stu-id="2c34c-101">In this exercise, we're going to create an Azure function that accepts an HTTP request with a single string.</span></span> <span data-ttu-id="2c34c-102">A função devolve uma cadeia ao chamador para representar sucesso ou falha.</span><span class="sxs-lookup"><span data-stu-id="2c34c-102">The function returns a string back to the caller to represent success or failure.</span></span>

> [!NOTE]
> <span data-ttu-id="2c34c-103">Para concluir este exercício, certifique-se de que tem sessão iniciada no [portal do Azure](https://portal.azure.com/) com uma conta válida.</span><span class="sxs-lookup"><span data-stu-id="2c34c-103">To complete this exercise, make sure you're signed in to the [Azure portal](https://portal.azure.com/) with a valid account.</span></span>

## <a name="create-an-http-trigger"></a><span data-ttu-id="2c34c-104">Criar um acionador HTTP</span><span class="sxs-lookup"><span data-stu-id="2c34c-104">Create an HTTP trigger</span></span>

<span data-ttu-id="2c34c-105">Vamos continuar a utilizar a nossa Aplicação de funções do Azure existente e adicionar um acionador HTTP.</span><span class="sxs-lookup"><span data-stu-id="2c34c-105">Let's continue using our existing Azure Functions application and add an HTTP trigger.</span></span>

1. <span data-ttu-id="2c34c-106">Aponte para **Funções** e selecione o ícone de sinal de adição (+).</span><span class="sxs-lookup"><span data-stu-id="2c34c-106">Point to **Functions** and select the plus (+) icon.</span></span>

    ![Aponte para Funções e selecione o sinal de adição](../media/4-hover-function.png)

1. <span data-ttu-id="2c34c-108">Selecione **Acionador HTTP**.</span><span class="sxs-lookup"><span data-stu-id="2c34c-108">Select **HTTP trigger**.</span></span>

1. <span data-ttu-id="2c34c-109">Selecione **C#** como linguagem.</span><span class="sxs-lookup"><span data-stu-id="2c34c-109">Select **C#** as the language.</span></span> 

1. <span data-ttu-id="2c34c-110">Deixe o **Nome** definido no valor predefinido.</span><span class="sxs-lookup"><span data-stu-id="2c34c-110">Leave the **Name** set to the default value.</span></span>

1. <span data-ttu-id="2c34c-111">Defina o **Nível de autorização** para **Anónimo**.</span><span class="sxs-lookup"><span data-stu-id="2c34c-111">Set the **Authorization level** to **Anonymous**.</span></span>

1. <span data-ttu-id="2c34c-112">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2c34c-112">Select **Create**.</span></span>

1. <span data-ttu-id="2c34c-113">Dê uma breve vista de olhos no código gerado automaticamente para ter uma ideia do que se está a passar.</span><span class="sxs-lookup"><span data-stu-id="2c34c-113">Take a quick look at the auto-generated code to get an idea about what's going on.</span></span> <span data-ttu-id="2c34c-114">O parâmetro *req* representa o pedido de entrada e contém um parâmetro de *nome*.</span><span class="sxs-lookup"><span data-stu-id="2c34c-114">The *req* parameter represents the incoming request and contains a *name* parameter.</span></span> <span data-ttu-id="2c34c-115">Vemos se *nome* tem um valor.</span><span class="sxs-lookup"><span data-stu-id="2c34c-115">We check to see if *name* has a value.</span></span> <span data-ttu-id="2c34c-116">Se tiver, devolvemos uma saudação.</span><span class="sxs-lookup"><span data-stu-id="2c34c-116">If it does, we return a greeting.</span></span> <span data-ttu-id="2c34c-117">Se não, devolvemos uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="2c34c-117">Otherwise, we return an error message.</span></span>

## <a name="get-your-function-url"></a><span data-ttu-id="2c34c-118">Obter o URL de função</span><span class="sxs-lookup"><span data-stu-id="2c34c-118">Get your function URL</span></span>

<span data-ttu-id="2c34c-119">Agora que criámos o acionador HTTP, vamos obter o URL de função para iniciar um pedido.</span><span class="sxs-lookup"><span data-stu-id="2c34c-119">Now that we've created the HTTP trigger, let's get the function URL so we can begin to make a request.</span></span>

1. <span data-ttu-id="2c34c-120">Selecione o acionador HTTP para abrir o ecrã de código.</span><span class="sxs-lookup"><span data-stu-id="2c34c-120">Select your HTTP trigger to open the code screen.</span></span>

1. <span data-ttu-id="2c34c-121">À direita de **Executar**, selecione **Obter URL de função**.</span><span class="sxs-lookup"><span data-stu-id="2c34c-121">To the right of **Run**, select **Get function URL**.</span></span>

1. <span data-ttu-id="2c34c-122">Selecione **Copiar**.</span><span class="sxs-lookup"><span data-stu-id="2c34c-122">Select **Copy**.</span></span>

1. <span data-ttu-id="2c34c-123">Selecione **Executar** para iniciar a sua função.</span><span class="sxs-lookup"><span data-stu-id="2c34c-123">Select **Run** to start your function.</span></span>

## <a name="issue-a-get-request-to-your-http-trigger"></a><span data-ttu-id="2c34c-124">Emitir um pedido GET para o acionador HTTP</span><span class="sxs-lookup"><span data-stu-id="2c34c-124">Issue a GET request to your HTTP trigger</span></span>

<span data-ttu-id="2c34c-125">Temos agora o URL de função copiado para a área de transferência.</span><span class="sxs-lookup"><span data-stu-id="2c34c-125">We now have our function URL copied to our clipboard.</span></span> <span data-ttu-id="2c34c-126">Vamos emitir um pedido GET para ver se obtemos uma resposta.</span><span class="sxs-lookup"><span data-stu-id="2c34c-126">Let's issue a GET request to see if we get a response.</span></span>

1. <span data-ttu-id="2c34c-127">Abra um novo separador no browser.</span><span class="sxs-lookup"><span data-stu-id="2c34c-127">Open a new tab in your web browser.</span></span>

1. <span data-ttu-id="2c34c-128">Cole o URL na barra de endereço.</span><span class="sxs-lookup"><span data-stu-id="2c34c-128">Paste the URL into the address bar.</span></span>

1. <span data-ttu-id="2c34c-129">Adicione um parâmetro de cadeia de consulta chamado *nome* com o seu nome, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="2c34c-129">Add a query string parameter called *name* with your name for example:</span></span>

    ```
    .../api/HttpTriggerCSharp1?name=Jesse
    ```

1. <span data-ttu-id="2c34c-130">Selecione ENTER para submeter o pedido.</span><span class="sxs-lookup"><span data-stu-id="2c34c-130">Select ENTER to submit the request.</span></span>

## <a name="clean-up"></a><span data-ttu-id="2c34c-131">Limpeza</span><span class="sxs-lookup"><span data-stu-id="2c34c-131">Clean up</span></span>

<span data-ttu-id="2c34c-132">Para garantir que esta função não lhe é cobrada, selecione **Colocar em pausa** por cima da janela de registo.</span><span class="sxs-lookup"><span data-stu-id="2c34c-132">To ensure that you aren't charged for this function, select **Pause** above the log window.</span></span>

![Colocar em pausa](../media/4-pause-timer.png)


