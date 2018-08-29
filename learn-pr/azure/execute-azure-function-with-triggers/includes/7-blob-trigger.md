Imagine que é um fotógrafo e tem um site em que mostra as suas imagens do dia. Porque está ocupado, não tem uma agenda de carregamento consistente, mas quer notificar os seus fãs quando carrega uma imagem. Decide criar uma função do Azure para enviar automaticamente um tweet sempre que carrega uma imagem para o seu contentor de blobs do Armazenamento do Azure.

Aqui, vai aprender a criar um acionador de blobs e instrui-lo a monitorizar uma determinada localização no seu contentor de blobs do Armazenamento do Azure.

## <a name="what-is-azure-storage"></a>O que é o Storage do Azure?

O Armazenamento do Azure é a solução de armazenamento na cloud da Microsoft que oferece suporte a todos os tipos de dados, incluindo: blobs, filas e NoSQL. O objetivo do Armazenamento do Azure consiste em fornecer armazenamento de dados que:

- Elevada disponibilidade
- Proteger
- Escalável
- Gerido

Não nos vamos focar muito no Armazenamento do Azure. Em vez disso, utilizamos para criar blobs que acionam a execução da nossa função.

## <a name="what-is-azure-blob-storage"></a>O que é o armazenamento de Blobs do Azure?

O armazenamento de Blobs do Azure é uma solução de armazenamento de objetos concebida para armazenar grandes quantidades de dados não estruturados. 

Por exemplo, o armazenamento de Blobs do Azure é melhor para fazer coisas como:

- A armazenar ficheiros.
- A servir ficheiros.
- Transmissão de áudio e vídeo.
- A registar dados.

Existem três tipos de blobs: **blobs de blocos**, **blobs de acréscimo** e **blobs de páginas**. Os blobs de blocos são o tipo mais frequentemente utilizado. Permitem-lhe armazenar texto ou dados binários de forma eficiente. Acrescentar blobs é como blobs de blocos, mas são concebidos para as operações de acrescento, como criar um ficheiro de registo que esteja a ser constantemente atualizado. Por fim, os blobs de páginas são constituídos por páginas e são concebidos para operações frequentes aleatórios de escrita e leitura.

## <a name="what-is-a-blob-trigger"></a>O que é um acionador de blob?

Um acionador de blob é um acionador que executa uma função quando um ficheiro é carregado ou atualizado no Armazenamento de blobs do Azure. Para criar um acionador de blob, cria uma conta do Armazenamento do Azure e fornece uma localização que o acionador monitoriza.

## <a name="how-to-create-a-blob-trigger"></a>Como criar um acionador de blobs

Tal como os outros acionadores que temos visto, vamos criar um acionador de blobs no portal do Azure. Dentro da sua função do Azure, selecione **acionador de Blob** na lista de tipos de acionadores predefinidos. Então introduza a lógica para executar quando é criado ou atualizado um blob.

Uma configuração que vai querer ver é o **Path**. O **Path** diz ao acionar de blob onde monitorizar para ver se um blob é carregado ou atualizado. Por predefinição, o valor **Path** é: 

> samples-workitems/{name}

Vamos dividir este conceito em duas partes: *samples-workitems* e *{name}*. A primeira parte *samples-workitems*, representa o contentor de blobs que o acionador monitoriza. A segunda parte, *{name}*, significa que cada tipo de ficheiro vai fazer com que o acionador invoque a função. A função é invocada porque não há filtro. Por exemplo, posso fazer o acionador invocar a função apenas quando um ficheiro PNG é adicionado, ao utilizar sintaxe como:

> samples-workitems/{nome}.png

A última parte significante das informações com este conceito é o texto *nome*. O *nome* representa um parâmetro na sua função do Azure que recebe o nome do ficheiro adicionado. Por exemplo, se eu carregar um ficheiro chamado *resume.txt*, a minha função do Azure recebe esse valor como uma cadeia de carateres através de um parâmetro chamado *nome*.

## <a name="summary"></a>Resumo

Um acionador de blob invoca uma função do Azure quando vê atividade numa determinada localização na sua conta do blob do Armazenamento do Azure. Define a localização para monitorizar ao modificar o valor **Path** no portal do Azure.
