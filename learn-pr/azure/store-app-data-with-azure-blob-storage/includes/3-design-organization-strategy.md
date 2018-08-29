Ao criar uma aplicação que precisa de armazenar dados, é importante pensar sobre como a aplicação vai organizar e armazenar os dados em contas de armazenamento, contentores e blobs.

## <a name="storage-accounts"></a>Contas de armazenamento

Uma conta de armazenamento única é flexível o suficiente para organizar os blobs à sua maneira, mas deve utilizar contas de armazenamento adicionais conforme preciso para separar os custos logicamente e controlar o acesso aos dados.

## <a name="containers-and-blobs"></a>Contentores e blobs

A natureza da sua aplicação e os dados armazenados devem orientar a sua estratégia de nomenclatura e organização dos contentores e dos blobs.

As aplicações que utilizam blobs como parte de um esquema de armazenamento que inclui uma base de dados, muitas vezes, não precisam de depender intensivamente da organização, da nomenclatura ou dos metadados para indicarem qualquer coisa sobre os seus dados. Essas aplicações normalmente utilizam identificadores, como GUIDs como nomes de blobs, e referenciam estes identificadores nos registos da base de dados. A aplicação irá utilizar a base de dados para determinar onde os blobs são armazenados e o tipo de dados que contêm.

Outras aplicações podem utilizar o armazenamento de Blobs do Azure mais como um sistema de ficheiros pessoais, onde os nomes de contentores e de blobs servem para indicar o significado e a estrutura. Os nomes de blobs nestes tipos de aplicações irão parecer, muitas vezes, nomes de ficheiros tradicionais e incluir extensões de nome de ficheiro, como `.jpg` para indicar que tipo de dados contêm. Eles irão utilizar diretórios virtuais (ver abaixo) para organizar os blobs e irão utilizar frequentemente etiquetas de metadados para armazenar informações sobre contentores e blobs.

Existem alguns aspetos importantes a ter em consideração ao decidir como organizar e armazenar blobs e contentores.

### <a name="naming-limitations"></a>Limitações de nomenclatura

Os nomes de contentor e blob têm de estar em conformidade com um conjunto de regras, incluindo as limitações de comprimento e as restrições de carateres. Veja a secção Recursos Adicionais no final deste módulo para obter informações mais específicas sobre regras de nomenclatura.

### <a name="public-access-and-containers-as-security-boundaries"></a>Acesso público e contentores como limites de segurança

Por predefinição, todos os blobs exigem autenticação para aceder. No entanto, os contentores individuais podem ser configurados para permitir a transferência pública dos respetivos blobs sem autenticação. Esta funcionalidade suporta muitos casos de utilização, como o alojamento ativo de site estático e a partilha de ficheiros. Isto acontece porque a transferência de conteúdos de blob funciona da mesma forma como ler qualquer outro tipo de dados na Web: basta apontar um navegador ou qualquer coisa que possa fazer um pedido GET no URL do blob.

**Imagem de contentor público da lista de tarefas que mostra o URL de acesso direto**

Ativar o acesso público é importante para a escalabilidade porque os dados transferidos diretamente do armazenamento de Blobs não geram qualquer tráfego na sua aplicação do lado do servidor. Mesmo que não tire partido imediatamente do acesso público ou se utilizar uma base de dados para controlar o acesso dos dados através da sua aplicação, utilize contentores separados para os dados que pretende disponibilizar publicamente.

> [!CAUTION]
> Os blobs num contentor configurado para acesso público podem ser transferidos sem qualquer tipo de autenticação ou auditoria por qualquer pessoa que conheça os seus URLs de armazenamento. Nunca coloque dados de blobs num contentor público que não pretenda partilhar publicamente.

Além do acesso público, o Azure tem uma funcionalidade de assinatura de acesso partilhado que permite o controlo refinado de permissões em contentores. O controlo de acesso de precisão permite cenários que melhoram ainda mais a escalabilidade, por isso pensar em contentores como limites de segurança em geral é uma diretriz útil.

### <a name="blob-name-prefixes-virtual-directories"></a>Prefixos de nome de blob (diretórios virtuais)

Tecnicamente, os contentores são "simples" e não suportam qualquer tipo de aninhamento ou hierarquia. Mas se der nomes hierárquicos aos seus blobs que se pareçam com caminhos de ficheiro (por exemplo, `finance/budgets/2017/q1.xls`), a operação de listagem da API pode filtrar os resultados para prefixos específicos. Isto permite-lhe navegar na lista como se fosse um sistema hierárquico de ficheiros e pastas.

Esta funcionalidade é frequentemente designada de *diretórios virtuais* porque é utilizada por algumas ferramentas e bibliotecas de cliente para visualizar e navegar em armazenamento de Blobs como se fosse um sistema de ficheiros. A navegação de cada pasta aciona uma chamada separada para listar os blobs nessa pasta.

**Imagem da lista de tarefas do explorador de armazenamento e/ou portal com pastas**

Utilizar nomes que são como os nomes dos blobs é uma técnica comum para organizar e navegar em dados de blobs complexos.

### <a name="blob-types"></a>Tipos de blobs

Existem três tipos diferentes de blobs onde pode armazenar os dados:

- Os **Blobs de blocos** são compostos por blocos de tamanhos diferentes que podem ser carregados e transferidos de forma independente e em paralelo. Escrever para um blob de blocos envolve o carregamento de dados para blocos e consolidá-los nas bibliotecas de cliente &mdash; de blob irá cuidar disto por si.
- Os **Blobs de acréscimo** são blobs de blocos especializados que suportam apenas o acréscimo de novos dados (não atualizam ou eliminam dados existentes), mas são muito eficientes a fazê-lo. Os blobs de acréscimo são ótimos para cenários como armazenar registos ou transmitir dados.
- Os **Blobs de páginas** foram criados para cenários que envolvem leituras e gravações de acesso aleatório. Os blobs de páginas servem para armazenar os ficheiros de disco rígido virtual (VHD) utilizados pelas Máquinas Virtuais do Azure, mas são ótimos para qualquer cenário que envolva o acesso aleatório.

Os blobs de blocos são a melhor opção para a maioria dos cenários que não chamam especificamente blobs de acréscimo ou de página.