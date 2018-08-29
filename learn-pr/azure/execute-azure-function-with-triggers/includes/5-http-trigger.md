Um pedido HTTP é uma operação comum na maioria das plataformas e dispositivos. Quer se trate de um pedido para procurar uma palavra num dicionário ou obter a meteorologia local, enviamos constantemente pedidos HTTP. As Funções do Azure permitem criar rapidamente uma parte de lógica para ser executada quando for recebido um pedido HTTP.  

Aqui, aprenderá a criar e invocar uma função do Azure com um acionador HTTP. Vai também explorar algumas das opções de personalização disponíveis.

## <a name="what-is-an-http-trigger"></a>O que é um acionador HTTP?

Um acionador HTTP é um acionador que executa uma função quando recebe um pedido HTTP. Os acionadores HTTP têm muitas capacidades e personalizações, incluindo:

- Fornecer acesso autorizado através de chaves.
- Restringir os verbos HTTP que são suportados.
- Devolver os dados ao autor da chamada.
- Receber dados através de parâmetros de cadeia de carateres de consulta ou do corpo do pedido.
- Suportar modelos de rota de URL para modificar o URL da função.

Quando criar um acionador HTTP, selecione uma linguagem de programação, forneça um nome de acionador e selecione um nível de Autorização.

## <a name="what-is-an-http-trigger-authorization-level"></a>O que é um nível de Autorização de acionador HTTP?

Um nível de Autorização de acionador HTTP é um sinalizador que indica se um pedido HTTP recebido precisa de uma chave API para autenticação.

Existem três níveis de Autorização:

- Função
- Anónimo
- Administrador

Os níveis **Função** e **Administrador** baseiam-se na "chave". Para enviar um pedido HTTP, tem de fornecer uma chave para autenticação. Existem dois tipos de chaves: *função* e *anfitrião*. As diferenças entre as duas chaves são o respetivo âmbito. As chaves de *função* são específicas de uma função. As chaves de *anfitrião* aplicam-se a todas as funções em toda a aplicação Funções do Azure. Se o nível de Autorização estiver definido como **Função**, pode utilizar uma chave de *função* ou de *anfitrião*. Se o nível de Autorização estiver definido como **Administrador**, tem de fornecer uma chave de *anfitrião*.

O nível **Anónimo** significa que não é necessária nenhuma autenticação. Utilizamos este nível no nosso exercício.

## <a name="how-to-create-an-http-trigger"></a>Como criar um acionador HTTP

Tal como um acionador de temporizador, pode criar um acionador HTTP através do portal do Azure. Na sua função do Azure, selecione **Acionador HTTP** na lista de tipos de acionadores predefinidos. Em seguida, introduza a lógica que pretende executar e efetue todas as personalizações necessárias, como restringir a utilização de determinados verbos HTTP. 

Uma definição importante de compreender é o **Nome do parâmetro do pedido**. Esta definição é uma cadeia de carateres que representa o nome do parâmetro que contém as informações sobre um pedido HTTP recebido. Por predefinição, o nome do parâmetro é *req*.

## <a name="how-to-invoke-an-http-trigger"></a>Como invocar um acionador HTTP

Para invocar um acionador HTTP, envie um pedido HTTP para o URL da função. Para obter este URL, vá para a página de código da função e selecione a ligação **Obter URL da função**.

![Localizar o URL da função](../media/5-function-url.png)

Depois de obter o URL da função, pode enviar pedidos HTTP. Se a função receber dados, lembre-se de que pode utilizar qualquer um dos parâmetros de cadeia de carateres de consulta ou fornecer os dados através do corpo do pedido.

## <a name="summary"></a>Resumo

Um acionador HTTP invoca uma função do Azure quando recebe um pedido HTTP para o respetivo URL da função. Os acionadores HTTP permitem-lhe receber dados e devolvê-los ao autor da chamada.
