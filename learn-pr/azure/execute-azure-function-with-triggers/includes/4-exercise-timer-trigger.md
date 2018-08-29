<span data-ttu-id="55532-101">Neste exercício, iremos criar uma função do Azure que é invocada a cada 20 segundos através de um acionador de temporizador.</span><span class="sxs-lookup"><span data-stu-id="55532-101">In this exercise, we create an Azure function that's invoked every 20 seconds using a timer trigger.</span></span>

> [!NOTE] 
> <span data-ttu-id="55532-102">Para concluir este exercício, certifique-se de que tem sessão iniciada no [portal do Azure](https://portal.azure.com/) com uma conta válida.</span><span class="sxs-lookup"><span data-stu-id="55532-102">To complete this exercise, make sure you're logged into the [Azure portal](https://portal.azure.com/) with a valid account.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="55532-103">Criar uma função do Azure</span><span class="sxs-lookup"><span data-stu-id="55532-103">Create an Azure function</span></span>

<span data-ttu-id="55532-104">Vamos começar por criar uma função do Azure no portal.</span><span class="sxs-lookup"><span data-stu-id="55532-104">Let’s start by creating an Azure function in the portal.</span></span>

1. <span data-ttu-id="55532-105">Na navegação à esquerda, selecione **Criar um recurso**.</span><span class="sxs-lookup"><span data-stu-id="55532-105">In the left navigation, select **Create a resource**.</span></span>

1. <span data-ttu-id="55532-106">Selecione **Computação**.</span><span class="sxs-lookup"><span data-stu-id="55532-106">Select **Compute**.</span></span>

1. <span data-ttu-id="55532-107">Localize e selecione **Aplicação de Funções**.</span><span class="sxs-lookup"><span data-stu-id="55532-107">Locate and select **Function App**.</span></span> <span data-ttu-id="55532-108">Opcionalmente, também pode utilizar a barra de pesquisa para localizar o modelo.</span><span class="sxs-lookup"><span data-stu-id="55532-108">You can also optionally use the search bar to locate the template.</span></span>

    ![Selecione Aplicação de Funções](../media/4-click-function-app.png)

1. <span data-ttu-id="55532-110">Introduza um **Nome de aplicação** exclusivo.</span><span class="sxs-lookup"><span data-stu-id="55532-110">Enter a unique **App name**.</span></span>

1. <span data-ttu-id="55532-111">Selecione uma **Subscrição**.</span><span class="sxs-lookup"><span data-stu-id="55532-111">Select a **Subscription**.</span></span>

1. <span data-ttu-id="55532-112">Crie um novo **Grupo de Recursos**.</span><span class="sxs-lookup"><span data-stu-id="55532-112">Create a new **Resource Group**.</span></span>

1. <span data-ttu-id="55532-113">Selecione **Windows** como o seu **SO**.</span><span class="sxs-lookup"><span data-stu-id="55532-113">Choose **Windows** as your **OS**.</span></span>

1. <span data-ttu-id="55532-114">Selecione **Plano de Consumo** para o **Plano de Alojamento**.</span><span class="sxs-lookup"><span data-stu-id="55532-114">Choose **Consumption Plan** for your **Hosting Plan**.</span></span> <span data-ttu-id="55532-115">É-lhe cobrada cada execução da sua função.</span><span class="sxs-lookup"><span data-stu-id="55532-115">You're charged for each execution of your function.</span></span> <span data-ttu-id="55532-116">Os recursos são automaticamente atribuídos com base na carga de trabalho da aplicação.</span><span class="sxs-lookup"><span data-stu-id="55532-116">Resources are automatically allocated based on your application workload.</span></span>

1. <span data-ttu-id="55532-117">Selecione uma **Localização**.</span><span class="sxs-lookup"><span data-stu-id="55532-117">Select a **Location**.</span></span>

1. <span data-ttu-id="55532-118">Crie uma nova conta de **Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="55532-118">Create a new **Storage** account.</span></span> <span data-ttu-id="55532-119">(Este valor é obrigatório, mas não vamos utilizá-lo.)</span><span class="sxs-lookup"><span data-stu-id="55532-119">(This value is required, but we're not going to use it.)</span></span>

1. <span data-ttu-id="55532-120">Desative o **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="55532-120">Turn off **Application Insights**.</span></span>

1. <span data-ttu-id="55532-121">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="55532-121">Select **Create**.</span></span>

## <a name="create-a-timer-trigger"></a><span data-ttu-id="55532-122">Criar um acionador de temporizador</span><span class="sxs-lookup"><span data-stu-id="55532-122">Create a timer trigger</span></span>

<span data-ttu-id="55532-123">Agora vamos criar um acionador de temporizador dentro da nossa função do Azure.</span><span class="sxs-lookup"><span data-stu-id="55532-123">Now we're going to create a timer trigger inside our Azure function.</span></span>

1. <span data-ttu-id="55532-124">Depois de criar a função do Azure, selecione **Todos os recursos** no painel de navegação esquerdo.</span><span class="sxs-lookup"><span data-stu-id="55532-124">After the Azure function is created, select **All resources** from the left navigation.</span></span>

1. <span data-ttu-id="55532-125">Localize e selecione a função do Azure.</span><span class="sxs-lookup"><span data-stu-id="55532-125">Locate and select your Azure function.</span></span>

1. <span data-ttu-id="55532-126">No novo painel, aponte para **Funções** e selecione o ícone de sinal de adição (+).</span><span class="sxs-lookup"><span data-stu-id="55532-126">On the new blade, point to **Functions** and select the plus (+) icon.</span></span>

    ![Aponte para Funções e selecione o sinal de adição](../media/4-hover-function.png)

1. <span data-ttu-id="55532-128">Selecione **Temporizador**.</span><span class="sxs-lookup"><span data-stu-id="55532-128">Select **Timer**.</span></span>

1. <span data-ttu-id="55532-129">Selecione **CSharp** como a linguagem.</span><span class="sxs-lookup"><span data-stu-id="55532-129">Select **CSharp** as the language.</span></span>

1. <span data-ttu-id="55532-130">Selecione **Criar esta função**.</span><span class="sxs-lookup"><span data-stu-id="55532-130">Select **Create this function**.</span></span>

## <a name="configure-the-timer-trigger"></a><span data-ttu-id="55532-131">Configurar o acionador de temporizador</span><span class="sxs-lookup"><span data-stu-id="55532-131">Configure the timer trigger</span></span>

<span data-ttu-id="55532-132">Temos uma função do Azure com a lógica para imprimir uma mensagem na janela de registo.</span><span class="sxs-lookup"><span data-stu-id="55532-132">We have an Azure function with logic to print a message to the log window.</span></span> <span data-ttu-id="55532-133">Vamos definir a agenda do temporizador para executar a cada 20 segundos.</span><span class="sxs-lookup"><span data-stu-id="55532-133">We're going to set the schedule of the timer to execute every 20 seconds.</span></span>

1. <span data-ttu-id="55532-134">Selecione **Integrar**.</span><span class="sxs-lookup"><span data-stu-id="55532-134">Select **Integrate**.</span></span>

1. <span data-ttu-id="55532-135">Introduza o seguinte valor na caixa **Agenda**:</span><span class="sxs-lookup"><span data-stu-id="55532-135">Enter the following value into the **Schedule** box:</span></span>

    ```
    */20 * * * * *
    ```

1. <span data-ttu-id="55532-136">Selecione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="55532-136">Select **Save**.</span></span>

## <a name="start-the-timer"></a><span data-ttu-id="55532-137">Iniciar o temporizador</span><span class="sxs-lookup"><span data-stu-id="55532-137">Start the timer</span></span>

<span data-ttu-id="55532-138">Agora que configurámos o temporizador, estamos prontos para iniciá-lo.</span><span class="sxs-lookup"><span data-stu-id="55532-138">Now that we've configured the timer, we're ready to start it.</span></span>

1. <span data-ttu-id="55532-139">Selecione **TimerTriggerCSharp1**.</span><span class="sxs-lookup"><span data-stu-id="55532-139">Select **TimerTriggerCSharp1**.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="55532-140">**TimerTriggerCSharp1** é um nome predefinido.</span><span class="sxs-lookup"><span data-stu-id="55532-140">**TimerTriggerCSharp1** is a default name.</span></span> <span data-ttu-id="55532-141">É selecionado automaticamente quando cria o acionador.</span><span class="sxs-lookup"><span data-stu-id="55532-141">It's automatically selected when you create the trigger.</span></span>

1. <span data-ttu-id="55532-142">Selecione **Executar**.</span><span class="sxs-lookup"><span data-stu-id="55532-142">Select **Run**.</span></span> 

<span data-ttu-id="55532-143">Agora deverá ver uma mensagem a cada 20 segundos na janela de registo.</span><span class="sxs-lookup"><span data-stu-id="55532-143">At this point, you should see a message every 20 seconds in the log window.</span></span>

## <a name="clean-up"></a><span data-ttu-id="55532-144">Limpeza</span><span class="sxs-lookup"><span data-stu-id="55532-144">Clean up</span></span>

<span data-ttu-id="55532-145">Para garantir que esta função não lhe é cobrada, acima da janela de registo, selecione **Colocar em pausa** para parar o temporizador.</span><span class="sxs-lookup"><span data-stu-id="55532-145">To ensure that you aren't charged for this function, above the log window, select **Pause** to stop the timer.</span></span>

![Colocar em pausa](../media/4-pause-timer.png)


