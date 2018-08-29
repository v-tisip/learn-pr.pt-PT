Ao observar os benefícios do Armazenamento do Azure, compreenda que ele oferece as melhores opções para armazenar o seu portal de aprendizagem. Agora vamos explorar as vantagens e as opções disponíveis no armazenamento do Azure em detalhe para ver como se encaixa com as suas necessidades de negócio.

## <a name="how-azure-storage-can-meet-your-business-storage-needs"></a>Como o armazenamento do Azure pode satisfazer as suas necessidades de armazenamento de negócios

O armazenamento do Azure oferece várias opções que acomodam os tipos específicos de necessidades de armazenamento de dados.

### <a name="azure-sql-database"></a>Base de dados SQL do Azure

A **Base de Dados SQL do Azure** é uma base de dados robusta da cloud relacional completamente gerida que armazena todos os seus dados. Pode utilizar esta funcionalidade para armazenar dados que acede e atualiza frequentemente, como informações pessoais e de formação da sua equipa. Também pode migrar as suas bases de dados do SQL Server existentes sem alterar as suas aplicações.

![AzureSQL](../images/Azure_SQL.png)

### <a name="azure-cosmos-db"></a>Azure Cosmos DB

O Azure Cosmos DB é uma funcionalidade premiada do Azure que é um serviço de base de dados globalmente distribuído. Suporta dados sem esquema que oferecem a capacidade de criar aplicações *Always On* e de elevada capacidade de resposta, para suportar dados em constante mudança. Pode utilizar esta funcionalidade para armazenar dados que são atualizados e mantidos com base nas entradas de utilizadores em todo o mundo.

![CosmosDB](../images/Azure_cosmos_db.png)

### <a name="azure-blob-storage"></a>Armazenamento de Blobs do Azure

O armazenamento de Blobs do Azure oferece a capacidade de transmitir ficheiros grandes de vídeo ou áudio diretamente para o navegador do utilizador a partir de qualquer lugar do mundo. O armazenamento de blobs também serve para armazenar dados de cópia de segurança e restauro, recuperação após desastre e arquivo. O armazenamento de Blobs do Azure pode armazenar até 8 TB de dados para armazenar ficheiros para Máquinas Virtuais.

![AzureBlob](../images/Azure_blob.png)

### <a name="azure-data-lake-storage-gen2"></a>Armazenamento do Azure Data Lake Ger2

A funcionalidade do data lake do armazenamento do Azure permite-lhe realizar análises da sua utilização de dados e preparar relatórios em conformidade. Um data lake é um repositório grande que armazena dados estruturados e não estruturados.

O **Azure Data Lake Storage Gen2** combina a escalabilidade e os benefícios de custo do armazenamento de objetos com a fiabilidade e o desempenho dos recursos do sistema de ficheiros de Macrodados.

![Data_lake_Store_concept](../images/Data_lake_store_concept.png)

### <a name="azure-files"></a>Ficheiros do Azure

Os ficheiros do Azure oferecem partilhas de ficheiros completamente geridas na cloud. As aplicações em execução no Azure podem partilhar facilmente ficheiros entre VMs. Pode utilizar partilhas de ficheiros do Azure em simultâneo para implementações na cloud ou no local do Windows, Linux e macOS.

![Azure_Files](../images/Azure_Files.png)

### <a name="azure-queue"></a>Fila do Azure

O armazenamento de Filas do Azure é um serviço para armazenar um grande número de mensagens que podem ser acedidas a partir de qualquer local no mundo. Uma mensagem de fila única tem até 64 KB de tamanho, ao passo que as filas podem conter milhões de mensagens.

A fila serve principalmente:

- Para criar uma lista de pendências de trabalho e para passar mensagens entre servidores Web diferentes do Azure.
- Para balancear carga entre servidores/infraestrutura da Web diferentes e gerir picos de tráfego.
- Para criar resiliência contra falhas de componentes quando vários utilizadores acedem aos seus dados ao mesmo tempo

![Azure_Queue](../images/Azure_Queue.png)

### <a name="azure-standard-storage"></a>Armazenamento Standard do Azure

As máquinas virtuais no Azure utilizam discos para armazenar um sistema operativo, aplicações e dados. O Armazenamento Standard do Azure disponibiliza suporte de discos fiável e económico para VMs com cargas de trabalho que não são de missão crítica. Com o Armazenamento Standard, os dados são armazenados em unidades de disco rígido (HDDs).

Ao trabalhar com VMs, pode utilizar os discos SSD e HDD standard para cargas de trabalho menos críticas e os discos SSD premium para aplicações de produção de missão crítica. Os Discos do Azure proporcionaram consistentemente durabilidade de nível empresarial, com uma Taxa de Falhas Anual Líder do Setor de ZERO %.

![Azure_disk](../images/Azure_disks.png)

### <a name="storage-tiers"></a>Camadas de armazenamento

O armazenamento do Azure oferece três camadas de armazenamento para Armazenamento de objeto de blob:

1. **Camada de armazenamento de acesso frequente** - a camada de armazenamento de acesso frequente do Azure está otimizada para armazenar dados que são acedidos com frequência. 
1. **Camada de armazenamento de acesso esporádico** - a camada de armazenamento de acesso esporádico do Azure está otimizada para armazenar dados que são acedidos com pouca frequência e armazenados durante 30 dias, pelo menos.
1. **Camada de armazenamento de arquivos** - a camada de armazenamento de arquivos do Azure está otimizada para armazenar dados que são raramente acedidos e armazenados durante, pelo menos, 180 dias, com requisitos de latência flexíveis. O armazenamento de arquivos no Azure é ideal para armazenar as versões mais antigas dos seus dados, para que possa obtê-los como e quando for preciso para auditorias ou outras atividades pouco frequentes.

![Archive_Tier](../images/Archive_Storage_Tier.png)

### <a name="azure-storage-encryptionreplication"></a>Encriptação/replicação de armazenamento do Azure

O armazenamento do Azure oferece segurança e elevada disponibilidade aos seus dados através de funcionalidades de encriptação e replicação.

#### <a name="encryption-for-storage-services"></a>Encriptação dos serviços de armazenamento

Os seguintes tipos de encriptação estão disponíveis para os seus recursos:

1. A **Encriptação do Serviço de Armazenamento do Azure (SSE)** ajuda a proteger os seus dados para cumprir a conformidade regulamentar e a segurança da sua organização. O Azure SSE encripta os dados antes de os armazenar e desencripta antes de os recuperar. A encriptação e a desencriptação são transparentes ao utilizador.
1. **Encriptação do lado do cliente**, onde os dados já são encriptados pelas bibliotecas de cliente. O Azure armazena os dados no estado encriptado em inatividade e, em seguida, são desencriptados durante a recuperação.

    Esta funcionalidade de encriptação garante que os dados atendem os padrões de proteção global. É adequado armazenar informações confidenciais, como dados pessoais e financeiros.

#### <a name="replication-for-storage-availability"></a>Replicação para disponibilidade de armazenamento

É configurado um tipo de replicação ao criar uma conta de armazenamento. A funcionalidade de replicação garante que os seus dados são duradouros e estão sempre disponíveis. O armazenamento do Azure permite replicações regionais e geográficas para proteger os dados contra desastres naturais e outras catástrofes locais, como incêndios ou inundações.
