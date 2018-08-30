Criou com êxito uma aplicação móvel de várias plataformas com o Xamarin e uma função do Azure com uma vinculação Twilio.

## <a name="clean-up-resources"></a>Limpar recursos

Quando terminar o seu trabalho nesta aplicação das Funções do Azure, poderá eliminar todos os recursos criados durante o tutorial no portal do Azure.

1. No Visual Studio, selecione *Visualizar->Cloud Explorer*.

2. Na lista pendente na parte superior deste painel, selecione *Grupos de Recursos*.

3. Expanda a subscrição que utilizou para criar o grupo de recursos. Com o botão direito do rato no grupo de recursos “ImHere” e selecione *Abrir no Portal*.

    ![Abra o grupo de recursos no portal a partir da janela do Cloud Explorer](../media/9-open-resource-group-in-portal.png)

4. Inicie sessão no portal do Azure no seu browser, se necessário.

5. O portal abrirá no grupo de recursos “ImHere”. Clique no botão **Eliminar Grupo de Recursos**.

    ![Eliminar o grupo de recursos](../media/9-delete-resource-group.png)

6. Introduza o nome do grupo de recursos para confirmar a eliminação e clique em **Eliminar**.

    ![Introduzir o nome do grupo de recursos para confirmar a eliminação](../media/9-confirm-delete-resource-group.png)

## <a name="summary"></a>Resumo

Neste tutorial, ficou a saber como:
> [!div class="checklist"]
> * Criar uma aplicação Xamarin.Forms de várias plataformas que utiliza o Xamarin.Essentials.
> * Criar uma interface de utilizador de várias plataformas através de XAML com a lógica de aplicação num ViewModel, bem como associar propriedades de um ViewModel à interface de utilizador.
> * Detetar a localização do utilizador.
> * Criar uma função do Azure com um acionador HTTP e executá-lo localmente.
> * Chamar uma função do Azure a partir de uma aplicação móvel, passando dados como JSON.
> * Vincular a função do Azure ao Twilio para enviar uma mensagem SMS.
> * Publicar uma função no Azure.
