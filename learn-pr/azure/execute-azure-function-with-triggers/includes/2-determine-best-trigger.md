Uma função do Azure não funciona até que algo a informe de que deve executar. Por exemplo, poderíamos criar uma função do Azure para enviar uma mensagem de texto de lembrete aos nossos clientes antes de um compromisso. Se não dissermos à função quando deve executar, os nossos clientes nunca receberão a mensagem. 

Aqui, irá examinar acionadores num alto nível e explorar os tipos mais comuns de acionadores.

## <a name="what-is-a-trigger"></a>O que é um acionador?

Um acionador é um serviço que define a forma como uma função do Azure é invocada. Por exemplo, se pretender que uma função seja executada a cada 10 minutos, pode utilizar um acionador de temporizador.

Cada função tem de ter exatamente um acionador associado a si. Se quiser executar uma parte de lógica em várias condições, tem de criar múltiplas funções.

## <a name="what-is-a-binding"></a>O que é um enlace?

Um enlace é uma ligação aos dados da sua função. Os enlaces são opcionais e tanto podem ser enlaces de entrada como de saída. Um enlace de entrada corresponde aos dados que a sua função recebe. Um enlace de saída corresponde aos dados que a sua função envia.

Ao contrário de um acionador, uma função pode ter múltiplos enlaces de entrada e de saída.

## <a name="types-of-triggers"></a>Tipos de acionadores

As Funções do Azure suportam um vasto leque de tipos de acionador. Aqui estão alguns dos tipos mais comuns:

| Tipo | Objetivo | 
| --- | --- | 
| **Temporizador** | Execute uma função num intervalo definido. | 
| **HTTP** | Execute uma função quando é recebido um pedido HTTP. |  
| **Blob** | Execute uma função quando um ficheiro é carregado ou atualizado no Armazenamento de blobs do Azure. | 
| **Fila** | Execute uma função quando uma mensagem é adicionada a uma fila do Armazenamento do Azure. | 
| **Cosmos DB** | Execute uma função quando um documento é alterado numa coleção. | 
| **Hub de Eventos** | Execute uma função quando um hub de eventos recebe um novo evento. | 

Neste módulo, vamos concentrar-nos no **temporizador**, **HTTP** e tipos de **blob**.

## <a name="summary"></a>Resumo

Para executar uma função do Azure, temos de utilizar um acionador. Os acionadores de temporizador, HTTP e blob são três dos tipos de acionador mais comuns que utilizará para executar a lógica sem servidor.
