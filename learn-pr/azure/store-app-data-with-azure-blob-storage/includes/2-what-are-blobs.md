## <a name="what-are-blobs-and-how-are-they-used"></a>O que são blobs e como são utilizados?

Os blobs são "ficheiros para a cloud". As aplicações trabalham com blobs exatamente da mesma forma que trabalhariam com ficheiros num disco, ao ler e escrever dados. No entanto, ao contrário de um ficheiro local, os blobs podem ser contactados a partir de qualquer lugar com uma ligação à internet. 

O armazenamento de Blobs do Azure *não está estruturado*, o que significa que não há restrições sobre os tipos de dados que podem deter. Por exemplo, um blob pode possuir um documento PDF, uma imagem JPG, um ficheiro JSON, conteúdo vídeo, etc. Os blobs não estão limitados aos formatos comuns de ficheiros, &mdash; um blob pode conter gigabytes de dados binários transmitidos a partir de um instrumento científico, uma mensagem encriptada para outra aplicação ou dados num formato personalizado para uma aplicação que está a desenvolver.

Os blobs normalmente não são adequados para dados estruturados que precisem de ser consultados com frequência. Têm uma maior latência que a memória e o disco local e não têm as funcionalidades de indexação que tornam as bases de dados eficientes na execução de consultas. No entanto, os blobs são frequentemente utilizados em *combinação* com as bases de dados para armazenar dados não consultáveis. Por exemplo, uma aplicação com uma base de dados de perfis de utilizadores pode armazenar imagens de perfis em blobs. Cada registo de utilizador na base de dados incluiria o nome ou URL do blob que contém a imagem do utilizador.

Os blobs são utilizados para armazenamento de dados de várias formas diferentes por todos os tipos de aplicações e arquiteturas:

* As aplicações que precisam de comunicar grandes quantidades de dados através de um sistema de mensagens que suporta apenas mensagens pequenas podem armazenar dados em blobs e enviar URLs de blobs nas mensagens.
* O armazenamento de blobs pode ser utilizado como um sistema de ficheiros par armazenar e partilhar documentos e outros dados pessoais.
* Os recursos web estáticos como imagens podem ser armazenadas em blobs e disponibilizadas para transferência pública como se fossem ficheiros num servidor web.
* Vários componentes do Azure utilizam blobs em segundo plano. Por exemplo, o Azure Cloud Shell armazena os seus ficheiros e configuração em blobs, as Máquinas Virtuais do Azure utiliza blobs para armazenamento em disco rígido.

Algumas aplicações criam, atualizam e eliminam blobs consistentemente como parte do seu trabalho. Outros utilizam um conjunto mais pequeno de blobs e raramente os alteram.

## <a name="storage-accounts-containers-and-metadata"></a>Contas de armazenamento, contentores e metadados

No armazenamento de Blobs, cada blob encontra-se dentro de um *contentor de blobs*. Pode armazenar um número ilimitado de blobs num contentor e um número ilimitado de contentores numa conta de armazenamento. Os contentores são "simples" &mdash; eles apenas podem armazenar blobs, não outros contentores.

**LISTA DE TAREFAS substituir esta imagem por algo melhor**

![Contas, contentores e blobs](../media-drafts/2-storage-container-blob.png)

Os blobs e contentores suportam metadados no formato de pares de cadeia de carateres nome-valor. As suas aplicações podem utilizar metadados para tudo o que quiser: uma descrição legível por humanos dos conteúdos de um blob a ser exibido pela aplicação, uma cadeia de carateres que a sua aplicação utiliza para determinar como processar os dados do blob, etc.

> [!TIP]
> O armazenamento de blobs não fornece nenhum mecanismo para pesquisar ou ordenar blobs por metadados. Veja a secção de Recursos Adicionais no final deste módulo para mais informações sobre como utilizar o Azure Search para conseguir.

## <a name="the-blob-storage-api-and-client-libraries"></a>A API de armazenamento de blobs e bibliotecas de cliente

A API de armazenamento de Blobs é baseada em REST e suportada por bibliotecas de clientes em várias linguagens populares. Permite-lhe escrever aplicações que criam e eliminam blobs e contentores, carregar e transferir dados de blob e listar os blobs num contentor.