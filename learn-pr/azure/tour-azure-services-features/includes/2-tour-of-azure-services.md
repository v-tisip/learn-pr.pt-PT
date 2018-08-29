O Microsoft Azure é um conjunto de serviços cloud em contínua expansão que ajudam a sua organização a atender os desafios atuais e futuros de negócios. O Azure dá-lhe a liberdade de criar, gerir e implementar aplicações numa rede grande e global com as suas ferramentas e estruturas preferidas. Esta secção inclui uma apresentação de alto nível dos recursos que o Azure oferece.

## <a name="azure-services"></a>Serviços do Azure

O Microsoft Azure oferece uma enorme variedade de serviços baseados na cloud, com funcionalidades adicionadas e melhoradas todos os meses.

![Serviços do Azure](../images/image204.png)

Vamos ver com mais detalhe algumas das funcionalidades mais utilizadas: 

- Computação
- Redes 
- Armazenamento
- Telemóvel 
- Bases de Dados 
- Web

### <a name="compute"></a>Computação

Os serviços de computação são um dos principais motivos por que as empresas mudam para a plataforma do Azure. O Azure oferece uma variedade de opções para o alojamento de aplicações e serviços, incluindo:

- Infraestrutura como serviço (**IaaS**)
- Plataforma como serviço (**PaaS**)
- Funções como serviço (**FaaS**)

Os próprios serviços são os seguintes:

|  Nome do Serviço             | Função de Serviço                                                          |  Tipo     |
| -------------             | -------------                                                             | --------- |
| Virtual Machines          | VMs do Windows ou Linux alojadas no Azure                                      | IaaS      |
| Azure Container Service   | Permite a gestão de um cluster de VMs que executam serviços em contentores    | IaaS      |
| Service Fabric            | Plataforma de sistemas distribuídos. É executado no Azure ou no local                | PaaS      |
| Azure Batch               | Serviço gerido para aplicações de computação paralelas e de elevado desempenho  | PaaS      |
| Serviços Cloud            | Serviço gerido para executar aplicações na cloud                            | PaaS      |
| Azure Container Instances | Oferecer contentores sem exigir aprovisionamento de VM ou serviços superiores      | FaaS      |
| Funções do Azure           | Serviço FaaS Gerido                                                      | FaaS      |

### <a name="networking"></a>Redes

A ligação de recursos de computação e a cedência de acesso a aplicações é a função principal da rede do Azure. A funcionalidade de rede no Azure inclui uma variedade de opções para ligar o mundo exterior aos serviços e funcionalidades nos data centers globais do Microsoft Azure.

As instalações de rede do Azure têm as seguintes funcionalidades:

|  Nome do Serviço             | Função de Serviço                                                                      |
| -------------             | -------------                                                                         |
| Rede Virtual           | Ligar VMs a ligações de Rede Privada Virtual (VPN) de entrada                     |
| Load balancer             | Equilibrar ligações de entrada e de saída para aplicações ou pontos finais de serviço         |
| Gateway de Aplicação       | Otimizar a entrega de farm de servidor de aplicações e aumentar a segurança de aplicações               |
| Gateway de VPN               | Aceder a Redes Virtuais do Azure através de gateways de VPN de elevado desempenho                   |
| DNS do Azure                 | Dar respostas de DNS ultrarrápidas e disponibilidade de domínio ultraelevada                   |
| Rede de Entrega de Conteúdos  | Oferecer conteúdo de elevada largura de banda globalmente aos clientes                                  |
| Proteção contra DDoS do Azure     | Proteger as aplicações alojadas no Azure contra ataques Denial of Service Distribuídos (DDoS)   |
| Gestor de Tráfego           | Distribuir tráfego de rede entre regiões do Azure em todo o mundo                             |
| ExpressRoute              | Ligar ao Azure através de ligações seguras dedicadas de elevada largura de banda                     |
| Observador de Rede           | Monitorizar e diagnosticar problemas de rede através da análise baseada em cenários                     |
| Azure Firewall            | Implementar firewall de alta segurança, elevada disponibilidade com escalabilidade ilimitada         |
| WAN Virtual               | Criar uma rede unificada de longa distância (WAN), ao ligar a sites locais e remotos           |

### <a name="storage"></a>Armazenamento

O Azure oferece quatro tipos principais de serviços de armazenamento. Esses serviços são:

- **Armazenamento de Blobs do Azure** - oferece armazenamento para objetos muito grandes, como ficheiros de vídeo ou mapas de bits
- **Armazenamento de Ficheiros do Azure** - cria partilhas de ficheiros que pode aceder e gerir como um servidor de ficheiros
- **Armazenamento de Filas do Azure** - implementa um arquivo para a colocação em fila e entrega fiável de mensagens entre aplicações
- **Armazenamento de Tabelas do Azure** - consiste num arquivo de NoSLQ que aloja dados não estruturados, independentes de qualquer esquema

Cada um destes serviços partilha características comuns, que são:

- Duradouros e altamente disponíveis com redundância e replicação.
- Seguros através de encriptação automática e controlo de acesso baseado em funções.
- Dimensionáveis com armazenamento virtualmente ilimitado.
- Geridos ao lidar com a manutenção e todos os problemas críticos por si.
- Acessíveis a partir de qualquer local no mundo através de HTTP ou HTTPS.

### <a name="mobile"></a>Telemóvel

O Azure permite aos programadores criarem aplicações iOS, Android e Windows apelativas, rápida e facilmente, numa ampla variedade de idiomas, optando pelo ambiente de programação à sua escolha. As funcionalidades que anteriormente consumiam algum tempo e aumentavam o risco do projeto, como adicionar o início de sessão empresarial e, em seguida, ligar a recursos no local, como SAP, Oracle, SQL Server e SharePoint são agora simples de incluir.

Outras funcionalidades deste serviço incluem:

- Sincronização de dados offline.
- Conectividade a dados no local.
- Transmissão de notificações push.
- Dimensionamento automático para atender as necessidade de negócio.

### <a name="databases"></a>Bases de Dados

O Azure oferece vários serviços de base de dados para armazenar uma grande variedade de tipos de dados e volumes. E com a conectividade global, estes dados estão disponíveis para os utilizadores de forma instantânea.

|  Nome do Serviço             | Função de Serviço                                                                                |
| -------------             | -------------                                                                                   |
| Azure Cosmos DB           | Base de dados distribuída globalmente que suporta opções de NoSQL                                       |
| Base de Dados SQL do Azure        | Base de dados relacional totalmente gerida com dimensionamento automático, inteligência integral e segurança robusta    |
| Base de Dados do Azure para MySQL  | Base de dados relacional MySQL completamente gerida e dimensionável com elevada disponibilidade e segurança        |
| BD do Azure para PostgreSQL   | Base de dados relacional PostgreSQL completamente gerida e dimensionável com elevada disponibilidade e segurança   |
| SQL Server em VMs         | aloje as aplicações empresariais do SQL Server na cloud                                                  |
| SQL Data Warehouse        | Armazém de dados totalmente gerido com segurança integral em todos os níveis de dimensionamento sem encargos extra    |
| Serviço de Migração do Azure DB    | Migre as suas bases de dados para a cloud sem alterações de código de aplicação                            |
| Cache de Redis               | Coloque em cache dados utilizados com frequência e dados estáticos para reduzir a latência de dados e aplicações                    |
| BD do Azure para MariaDB      | Base de dados relacional MySQL completamente gerida e dimensionável com elevada disponibilidade e segurança        |

### <a name="web"></a>Web

Os serviços da Web no Azure incluem os seguintes recursos:

- Serviço de Aplicações - crie rapidamente poderosas aplicações Web e móveis na cloud
- Rede de Entrega de Conteúdos - garanta a entrega de conteúdos segura e fiável com ampla influência global
- Hubs de notificação - envie notificações push para qualquer plataforma em qualquer back-end
- Gestão de API - publique APIs para programadores, parceiros e empregados de forma segura e em escala
- Azure Search - pesquisa como serviço totalmente gerida
- Aplicações Web - crie e implemente rapidamente aplicações Web fundamentais à escala
- Serviço do Azure SignalR - adicione funcionalidades Web em tempo real facilmente

## <a name="summary"></a>Resumo

Obteve agora uma descrição geral dos serviços que o Azure oferece. Também identificou algumas das áreas mais importantes que iriam interessar a uma empresa que pretenda migrar para o Azure, para resolver problemas relacionados com escalabilidade e manipulação de picos de carga. Na unidade seguinte, irá registar uma conta gratuita do Azure e iniciar sessão no portal.