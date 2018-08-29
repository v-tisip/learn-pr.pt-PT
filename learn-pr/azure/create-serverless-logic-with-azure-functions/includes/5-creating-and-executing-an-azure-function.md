Agora que temos uma aplicação de funções criada, vamos aprender a criar, configurar e executar uma Função do Azure.

### <a name="triggers"></a>Acionadores
As funções do Azure são orientadas por eventos e executam em resposta a um evento, como receber um pedido HTTP ou uma mensagem ser adicionada a uma fila. 

O tipo de evento que inicia a função é denominado acionador. As funções do Azure requerem, pelo menos, a configuração de um acionador. Caso contrário, não seria possível executar a função.

 O Azure suporta uma vasta gama de acionadores, incluindo:
* HTTPTrigger
* TimerTrigger
* Webhook do GitHub
* CosmosDBTrigger
* BlobTrigger
* QueueTrigger
* EventHubTrigger
* ServiceBusQueueTrigger
* ServiceBusTopicTrigger

### <a name="bindings"></a>Enlaces
Os enlaces de funções do Azure são uma forma declarativa de ligar dados à sua função programaticamente.

Os enlaces são a ligação aos seus serviços de dados. Uma função do Azure com nenhum, um ou mais enlaces permite-lhe aceder a várias origens de dados. Também os define como enlaces de entrada ou saída, ou pode considerá-los enlaces de leitura ou escrita.

Suponha que tem um QueueTrigger que inicia uma função quando é adicionado um blob a uma fila. Seria utilizado um enlace de blob de entrada para ligar ao armazenamento de Blobs do Azure. 

Os enlaces de saída são utilizados para armazenar dados. Por exemplo, enviam o valor de retorno da função para o armazenamento de Tabelas do Azure.

Está disponível uma lista de enlaces completa na [documentação do Azure](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings#supported-bindings).

### <a name="a-sample-trigger-and-binding-functionjson"></a>Um acionador e um enlace de exemplo (function.json)
Trata-se de uma definição de exemplo de um acionador e um enlace para uma função. Vai reparar que, consoante o tipo de enlace que estiver a descrever, existem diferentes valores de propriedade que têm de ser definidos. Cada enlace tem também uma direção que define se é um enlace de entrada ou de saída. Os acionadores são sempre enlaces de entrada. Este exemplo mostra uma função acionada por uma mensagem a ser adicionada a uma fila com o nome **myqueue-items**. Em seguida, envia o valor de retorno da função para a tabela **outTable** no armazenamento de Tabelas do Azure.

```javascript
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "myqueue-items",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    },
    {
      "name": "$return",
      "type": "table",
      "direction": "out",
      "tableName": "outTable",
      "connection": "MY_TABLE_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```
## <a name="premade-functions-and-templates"></a>Funções e modelos pré-criados
O Azure fornece modelos pré-configurados para cenários de função comuns do Azure.

### <a name="quickstart-templates"></a>Modelos de início rápido
Para adicionar uma função do Azure, tem de selecionar uma aplicação de funções. A aplicação de funções pode ser identificada pelo relâmpago no ícone de parênteses pontiagudo.  
![Ícone de função](../images/5-function-icon.png)

Ao adicionar a sua primeira função do Azure, é apresentado o ecrã de Início Rápido. Este ecrã permite-lhe fazer uma seleção do tipo de acionador e linguagem de programação desejados. Em seguida, com base nas suas seleções, o Azure vai gerar o código de função e a configuração para si.  
![Início Rápido de Função](../images/5-quickstart-form.png)

### <a name="function-templates"></a>Modelos de função
A seleção de modelos não está limitada aos disponíveis no Início Rápido. Tem também a opção de escolher de entre mais de 30 modelos diferentes. Pode aceder ao ecrã de lista de modelos durante a criação de funções subsequentes ou ao selecionar a opção **Função personalizada** no ecrã de Início Rápido.  
![Modelos de função](../images/5-template-list.png)

## <a name="navigating-to-your-function-and-files"></a>Navegar para a sua função e ficheiros
Depois de criar uma função a partir de um modelo, são criados vários ficheiros. Suponha que optou por utilizar o Início Rápido Webhook + API com JavaScript. Os ficheiros gerados seriam um ficheiro de configuração **function.json** e um ficheiro de código de origem, **index.js**. Quando aceder à aplicação de funções, será apresentada uma árvore de menu com as funções criadas na aplicação. É também neste item de menu **Funções** que é possível adicionar mais funções à aplicação de funções (será apresentado um ícone de sinal de adição quando pairar o rato sobre o item de menu).  
![Botão Adicionar Função](../images/5-function-add-button.png) 

No caso do Início Rápido mencionado acima, ao expandir **Funções** na vista de árvore, verá uma função com o nome predefinido **HttpTriggerJS1** (indicado pelo ícone de função f). Selecionar esta função vai abrir uma janela de código e apresentar o ficheiro de origem **index.js**. No lado direito da janela de código, existe um submenu que inclui um separador para **Ver ficheiros**. Selecionar este separador mostrará a estrutura de ficheiros (reproduzida no armazenamento) que compõe a sua função.  
![Modelos de função](../images/5-file-navigation.png)

## <a name="execution-options-for-testing-your-azure-function"></a>Opções de execução para testar a sua função do Azure
Depois de criar uma função do Azure, tem de saber como testá-la. Existem duas abordagens: execução manual e teste a partir do próprio portal do Azure.

### <a name="manual-execution-of-a-function"></a>Execução manual de uma função
Pode iniciar a execução de uma função ao acionar manualmente o acionador configurado. Por exemplo, se estiver a utilizar um HttpTrigger, pode utilizar uma ferramenta como o Postman ou o cURL para iniciar um pedido HTTP para o URL de ponto final de função.  
![Execução do Postman de uma função](../images/5-postman-execution.png) Pode obter o URL de ponto final ao selecionar o Acionador HTTP no painel de navegação esquerdo e, em seguida, ao selecionar o botão **Obter URL de função**.  
![Obter URL de função](../images/5-get-function-url.png)

### <a name="testing-a-function-in-the-azure-portal"></a>Testar uma função no portal do Azure
Em alternativa, o portal do Azure também fornece uma forma prática de testar as suas funções. No lado direito da janela de código, existe um submenu de navegação com separadores. Este menu contém um item **Teste**. Expandir o menu e selecionar este separador permite executar a função e ver o resultado de outra forma. Para manter o cenário de HttpTrigger, pode definir o método HTTP e adicionar parâmetros querystring e cabeçalhos HTTP ao pedido. Também pode alterar o corpo do pedido para testar cenários adicionais. A janela de saída mostra o resultado da função.  
![Execução do portal de uma função](../images/5-portal-execution.png)

## <a name="monitoring-an-azure-function"></a>Monitorizar uma função do Azure
Durante o desenvolvimento de funções do Azure, a capacidade de registar mensagens e determinar cenários de exceção é fundamental para garantir que está a preparar as suas funções para produção. Isto é igualmente importante num cenário de produção, quando monitorizar a origem de um defeito. O portal do Azure fornece uma interface de utilizador que fornece um dashboard de monitorização, bem como uma forma de rever os registos de execução e as exceções obtidas a partir das funções do Azure.

### <a name="monitoring-dashboard"></a>Dashboard de monitorização
No menu de navegação da aplicação de funções, depois de expandir o nó de função, verá o item de menu **Monitorizar**. O dashboard de monitorização é uma forma rápida de ver o histórico de execuções de funções. Esta vista apresenta o carimbo de data/hora, o código de resultado, a duração e o ID da operação, bem como se foi concluída com êxito. Os dados são preenchidos através do Azure Application Insights.  
![Monitorização de funções](../images/5-monitor-function.png)

### <a name="log-window"></a>Janela de registo
Também é possível adicionar declarações de registo à função. Estas declarações serão apresentadas na janela de registo da função. A janela de registo está localizada num submenu com separadores localizado na parte inferior da janela de código. Quando utilizar uma função baseada em JavaScript, adicionará uma declaração de registo com a seguinte sintaxe:
```javascript
  context.log('Enter your logging statement here');
```  
![Janela de registo](../images/5-log-window.png)

### <a name="errors-and-warnings-window"></a>Erros e janela de avisos
Pode localizar o separador de erros e da janela de avisos no mesmo submenu da janela de registo. Esta janela vai mostrar erros de compilação e avisos no seu código. Como o JavaScript é uma linguagem dinâmica e interpretada, a imagem seguinte mostra um erro de compilação numa função C#.  
![Erros e janela de avisos](../images/5-errors-window.png)
