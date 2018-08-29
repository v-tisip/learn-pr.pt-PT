<span data-ttu-id="445df-101">A aplicação e a função do Azure estão agora concluídas e em execução localmente.</span><span class="sxs-lookup"><span data-stu-id="445df-101">The app and Azure function are now complete and running locally.</span></span> <span data-ttu-id="445df-102">Nesta unidade, publica a função do Azure para o Azure ser executado na cloud.</span><span class="sxs-lookup"><span data-stu-id="445df-102">In this unit, you publish the Azure function to Azure to run in the cloud.</span></span>

> <span data-ttu-id="445df-103">Nesta unidade, irá publicar a sua função a partir do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="445df-103">In this unit, you will publish your function from Visual Studio.</span></span> <span data-ttu-id="445df-104">Esta é uma ótima forma de começar a utilizar as provas de conceito, os protótipos e a aprendizagem, mas para uma aplicação de qualidade de produção **não** deve utilizar este método.</span><span class="sxs-lookup"><span data-stu-id="445df-104">This is a great way to get started for proof-of-concepts, prototypes, and learning, but for a production-quality app you should **not** use this method.</span></span> <span data-ttu-id="445df-105">Deve utilizar alguma forma de implementação baseada em CI.</span><span class="sxs-lookup"><span data-stu-id="445df-105">You should use some form of CI-based deployment.</span></span> <span data-ttu-id="445df-106">Pode ler mais sobre como fazê-lo nos [documentos de Implementação de Funções do Azure](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment).</span><span class="sxs-lookup"><span data-stu-id="445df-106">You can read more about doing this in the [Azure Functions Deployment docs](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment).</span></span>
>
> <span data-ttu-id="445df-107">[![Os amigos não deixam os amigos publicarem com o botão direito do rato](../media/8-friends-dont-let-friends-publish.png)](https://damianbrady.com.au/2018/02/01/friends-dont-let-friends-right-click-publish/)</span><span class="sxs-lookup"><span data-stu-id="445df-107">[![Friends don't let friends right-click publish](../media/8-friends-dont-let-friends-publish.png)](https://damianbrady.com.au/2018/02/01/friends-dont-let-friends-right-click-publish/)</span></span>

## <a name="publishing-your-app-to-azure"></a><span data-ttu-id="445df-108">Publicar a sua aplicação no Azure</span><span class="sxs-lookup"><span data-stu-id="445df-108">Publishing your app to Azure</span></span>

<span data-ttu-id="445df-109">As funções do Azure podem ser publicadas no Azure a partir do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="445df-109">Azure functions can be published to Azure from inside Visual Studio.</span></span>

1. <span data-ttu-id="445df-110">Pare o runtime das funções do Azure local se ainda estiverem em execução na unidade anterior.</span><span class="sxs-lookup"><span data-stu-id="445df-110">Stop the local Azure Functions runtime if it's still running from the previous unit.</span></span>

2. <span data-ttu-id="445df-111">Clique com o botão direito do rato na aplicação `ImHere.Functions` no explorador e selecione *Publicar...*.</span><span class="sxs-lookup"><span data-stu-id="445df-111">Right-click on the `ImHere.Functions` app in the solution explorer and select *Publish...*.</span></span>

    ![Clique com o botão direito na aplicação de Funções](../media/8-right-click-publish.png)

3. <span data-ttu-id="445df-113">Na caixa de diálogo **Escolher um destino da publicação**, selecione *Aplicação de Funções do Azure* e no **Serviço de Aplicações do Azure**, selecione *Criar Novo*.</span><span class="sxs-lookup"><span data-stu-id="445df-113">From the **Pick a publish target** dialog, select *Azure Function App*, and for **Azure App Service**, select *Create New*.</span></span> <span data-ttu-id="445df-114">Clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="445df-114">Click **Publish**.</span></span>

    ![Criar um novo Serviço de Aplicações do Azure para publicar](../media/8-pick-publish-target.png)

4. <span data-ttu-id="445df-116">Selecione a sua conta do Azure na lista suspensa no canto superior direito se tiver mais de uma conta do Azure e não estiver selecionada a correta.</span><span class="sxs-lookup"><span data-stu-id="445df-116">Select your Azure account from the drop-down in the top-right corner if you have more than one Azure accounts and the right one isn't selected.</span></span>

5. <span data-ttu-id="445df-117">Dê um nome à sua aplicação de Funções.</span><span class="sxs-lookup"><span data-stu-id="445df-117">Give your Functions app a name.</span></span> <span data-ttu-id="445df-118">Este nome tem de ser globalmente exclusivo em todas as aplicações de Funções em todo o Azure, por isso utilize algo como "ImHere-\<YourName\>".</span><span class="sxs-lookup"><span data-stu-id="445df-118">This name needs to be globally unique across all the Functions apps in the whole of Azure, so use something like "ImHere-\<YourName\>".</span></span>

6. <span data-ttu-id="445df-119">Selecione a subscrição com a qual pretende criar a aplicação de Funções.</span><span class="sxs-lookup"><span data-stu-id="445df-119">Select the subscription you want to create this Functions app under.</span></span>

7. <span data-ttu-id="445df-120">Crie um novo grupo de recursos para esta aplicação de Funções, ao clicar no botão **Novo...** junto à lista pendente **Grupo de Recursos** e atribua um nome como "ImHere".</span><span class="sxs-lookup"><span data-stu-id="445df-120">Create a new resource group for this Functions app by clicking the **New...** button next to the **Resource Group** drop-down and giving it a name such as "ImHere".</span></span> <span data-ttu-id="445df-121">Os nomes de grupo de recursos têm de ser exclusivos na sua subscrição, não globalmente exclusivos em todo o Azure.</span><span class="sxs-lookup"><span data-stu-id="445df-121">Resource group names need to be unique to your subscription, not globally unique across Azure.</span></span> <span data-ttu-id="445df-122">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="445df-122">Then, click **OK**.</span></span>

    ![Criar um novo grupo de recursos](../media/8-create-new-resource-group.png)

   <span data-ttu-id="445df-124">Criar um novo grupo de recursos facilita a limpeza posterior.</span><span class="sxs-lookup"><span data-stu-id="445df-124">Creating a new resource group makes it easier to clean up later.</span></span> <span data-ttu-id="445df-125">Pode eliminar o grupo de recursos e saber que tudo o que criou para esta aplicação de Funções será eliminado ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="445df-125">You can delete the resource group and know that everything you've created for this Functions app will all be deleted at the same time.</span></span>

8. <span data-ttu-id="445df-126">Crie um novo plano de alojamento ao clicar em **Novo...** junto à lista pendente **Plano de Alojamento**.</span><span class="sxs-lookup"><span data-stu-id="445df-126">Create a new hosting plan by clicking the **New...** button next to the **Hosting Plan** drop-down.</span></span> <span data-ttu-id="445df-127">O nome do plano do Serviço de Aplicações será predefinido para o nome da sua aplicação com "Plano" no final.</span><span class="sxs-lookup"><span data-stu-id="445df-127">The App Service plan name will default to your app name with "Plan" on the end.</span></span> <span data-ttu-id="445df-128">Defina a **Localização** para a localização mais próxima para si e certifique-se de que o **Tamanho** está definido para consumo.</span><span class="sxs-lookup"><span data-stu-id="445df-128">Set the **Location** to the closest location to you and make sure **Size** is set to consumption.</span></span> <span data-ttu-id="445df-129">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="445df-129">Then, click **OK**.</span></span>

    ![Configurar o plano de alojamento](../media/8-configure-hosting-plan.png)

9. <span data-ttu-id="445df-131">Crie uma nova conta de armazenamento ao clicar no botão **Novo...** junto à lista pendente **Conta de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="445df-131">Create a new storage account by clicking the **New...** button next to the **Storage Account** drop-down.</span></span> <span data-ttu-id="445df-132">Será indicado um nome predefinido, pelo que deve manter todos os valores predefinidos e clicar em **OK**.</span><span class="sxs-lookup"><span data-stu-id="445df-132">A default name will be provided, so keep all the default values and click **OK**.</span></span>

    ![Criar uma conta de armazenamento](../media/8-create-storage-account.png)

10. <span data-ttu-id="445df-134">Clique em **Criar** para aprovisionar todos os recursos no Azure e publicar a sua aplicação de Funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="445df-134">Click **Create** to provision all the resources on Azure and publish your Azure Functions app.</span></span>

    ![Criar o Serviço de Aplicações](../media/8-create-app-service.png)

<span data-ttu-id="445df-136">O aprovisionamento irá demorar alguns minutos a executar.</span><span class="sxs-lookup"><span data-stu-id="445df-136">Provisioning will take a couple of minutes or so to run.</span></span> <span data-ttu-id="445df-137">Serão aprovisionados os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="445df-137">The following resources will be provisioned:</span></span>

* <span data-ttu-id="445df-138">Uma conta de armazenamento para armazenar os ficheiros exigidos para a aplicação de Funções do Azure</span><span class="sxs-lookup"><span data-stu-id="445df-138">A storage account to store the files needed for the Azure Functions app</span></span>
* <span data-ttu-id="445df-139">Um plano do Serviço de Aplicações para gerir os recursos de computação exigidos pela aplicação de Funções do Azure</span><span class="sxs-lookup"><span data-stu-id="445df-139">An App Service plan to manage the compute resources needed by the Azure Functions app</span></span>
* <span data-ttu-id="445df-140">O Serviço de Aplicações que executa a função do Azure</span><span class="sxs-lookup"><span data-stu-id="445df-140">The App Service that runs the Azure function</span></span>

<span data-ttu-id="445df-141">A função será agora publicada e está disponível para chamar em https://<nome-da-sua-aplicação>.azurewebsites.net/api/SendLocation.</span><span class="sxs-lookup"><span data-stu-id="445df-141">The function will now be published and available to call at https://<your-app-name>.azurewebsites.net/api/SendLocation.</span></span>

## <a name="configuring-your-app"></a><span data-ttu-id="445df-142">Configurar a sua aplicação</span><span class="sxs-lookup"><span data-stu-id="445df-142">Configuring your app</span></span>

<span data-ttu-id="445df-143">Quando a função do Azure estava a ser executada localmente, estava a utilizar credenciais do Twilio que estavam armazenadas num ficheiro `local.settings.json`.</span><span class="sxs-lookup"><span data-stu-id="445df-143">When the Azure function was running locally, it was using Twilio credentials that were stored in a `local.settings.json` file.</span></span> <span data-ttu-id="445df-144">Como o nome sugere, este ficheiro destina-se a configurações locais, e não definições do Azure.</span><span class="sxs-lookup"><span data-stu-id="445df-144">As the name suggests, this file is for local settings, not Azure settings.</span></span> <span data-ttu-id="445df-145">Antes de a função do Azure poder ser chamada no Azure, as definições `TwilioAccountSid` e `TwilioAuthToken` têm de ser configuradas.</span><span class="sxs-lookup"><span data-stu-id="445df-145">Before the Azure function can be called inside Azure, the `TwilioAccountSid` and `TwilioAuthToken` settings need to be configured.</span></span>

1. <span data-ttu-id="445df-146">No separador Publicar, clique na opção **Gerir Definições da Aplicação**.</span><span class="sxs-lookup"><span data-stu-id="445df-146">From the Publish tab, click the **Manage Application Settings** option.</span></span>

    ![A opção Gerir Definições da Aplicação](../media/8-application-settings-option.png)

2. <span data-ttu-id="445df-148">Clique no botão **Adicionar** para adicionar uma nova definição.</span><span class="sxs-lookup"><span data-stu-id="445df-148">Click the **Add** button to add a new setting.</span></span> <span data-ttu-id="445df-149">Dê-lhe o nome "TwilioAccountSid" e defina o valor para o seu SID da conta do Twilio.</span><span class="sxs-lookup"><span data-stu-id="445df-149">Name it "TwilioAccountSid" and set the value to your Twilio account SID.</span></span> <span data-ttu-id="445df-150">Repita este passo para o Token de Autenticação que utiliza o nome "TwilioAuthToken".</span><span class="sxs-lookup"><span data-stu-id="445df-150">Repeat this step for your Auth Token using the name "TwilioAuthToken".</span></span>

    ![Definir as credenciais do Twilio nas definições da aplicação](../media/8-set-creds-in-app-settings.png)

3. <span data-ttu-id="445df-152">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="445df-152">Click **OK**.</span></span>

4. <span data-ttu-id="445df-153">Clique em **Publicar** para voltar a publicar a aplicação de Funções do Azure com as novas definições de aplicação.</span><span class="sxs-lookup"><span data-stu-id="445df-153">Click **Publish** to republish the Azure Functions app with the new application settings.</span></span>

    ![O botão de publicação](../media/8-publish-application-button.png)

## <a name="pointing-the-mobile-app-to-azure"></a><span data-ttu-id="445df-155">Apontar a aplicação móvel para o Azure</span><span class="sxs-lookup"><span data-stu-id="445df-155">Pointing the mobile app to Azure</span></span>

1. <span data-ttu-id="445df-156">No separador Publicar, copie o **URL do Site** com o botão de cópia junto ao valor.</span><span class="sxs-lookup"><span data-stu-id="445df-156">From the Publish tab, copy the **Site URL** using the copy button next to the value.</span></span>

    ![Copie o URL do site no separador de publicação](../media/8-copy-site-url.png)

2. <span data-ttu-id="445df-158">Abra o `MainViewModel` a partir do projeto `ImHere`.</span><span class="sxs-lookup"><span data-stu-id="445df-158">Open the `MainViewModel` from the `ImHere` project.</span></span>

3. <span data-ttu-id="445df-159">Atualize o valor do campo `baseUrl` para ser o URL do site copiado do separador Publicar.</span><span class="sxs-lookup"><span data-stu-id="445df-159">Update the value of the `baseUrl` field to be the site URL copied from the Publish tab.</span></span>

4. <span data-ttu-id="445df-160">Altere o protocolo para este valor de `http` para `https`.</span><span class="sxs-lookup"><span data-stu-id="445df-160">Change the protocol for this value from `http` to `https`.</span></span> <span data-ttu-id="445df-161">O URL do site é sempre dado com HTTP, mas tem de utilizar HTTPS para chamar uma função do Azure.</span><span class="sxs-lookup"><span data-stu-id="445df-161">The site URL is always given using HTTP, but you have to use HTTPS to call an Azure function.</span></span>

## <a name="test-it-out"></a><span data-ttu-id="445df-162">Teste</span><span class="sxs-lookup"><span data-stu-id="445df-162">Test it out</span></span>

1. <span data-ttu-id="445df-163">Defina a aplicação `ImHere.UWP` como a aplicação de arranque e execute-a.</span><span class="sxs-lookup"><span data-stu-id="445df-163">Set the `ImHere.UWP` app as the startup app and run it.</span></span>

2. <span data-ttu-id="445df-164">Introduza um número de telefone e clique no botão **Enviar Localização**.</span><span class="sxs-lookup"><span data-stu-id="445df-164">Enter a phone number and click the **Send Location** button.</span></span>

3. <span data-ttu-id="445df-165">Deverá receber a localização como uma mensagem SMS.</span><span class="sxs-lookup"><span data-stu-id="445df-165">You should receive the location as an SMS message.</span></span>

## <a name="summary"></a><span data-ttu-id="445df-166">Resumo</span><span class="sxs-lookup"><span data-stu-id="445df-166">Summary</span></span>

<span data-ttu-id="445df-167">Nesta unidade aprendeu a publicar um projeto de Funções do Azure para o Azure a partir do Visual Studio e a configurar as definições da aplicação.</span><span class="sxs-lookup"><span data-stu-id="445df-167">In this unit, you learned how to publish an Azure Functions project to Azure from inside Visual Studio and configure application settings.</span></span>