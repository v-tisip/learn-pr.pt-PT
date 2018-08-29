Os recursos de informática na cloud são fornecidos através de três modelos de serviço diferentes.

- A **Infraestrutura como um serviço (IaaS)** fornece uma infraestrutura de computação instantânea que pode aprovisionar e gerir através da Internet.
- A **Plataforma como um serviço (PaaS)** fornece ambientes de desenvolvimento e implementação prontos a utilizar com os quais pode fornecer os seus próprios serviços cloud.
- O **Software como um serviço (SaaS)** fornece aplicações através da Internet como um serviço baseado na Web.

Ao escolher um modelo de serviço, considere quem deverá ficar responsável pelo recurso de computação. Com base no seu cenário, pode decidir o grau de responsabilidade de gestão partilhada que pretende.

![Modelo de responsabilidade partilhada](../media/3-shared-responsibility.png)

## <a name="iaas"></a>IaaS

A infraestrutura como um serviço é uma infraestrutura de computação instantânea, aprovisionada e gerida através da Internet. A IaaS permite-lhe dimensionar rapidamente os recursos de modo a satisfazer a procura e pagar apenas aquilo que utiliza. A IaaS evita a despesa e a complexidade inerentes à aquisição e gestão dos seus próprios servidores físicos e de outras infraestruturas de datacenters. Cada recurso é disponibilizado como um componente de serviço separado e o utilizador *aluga* o recurso pelo tempo que for necessário. Daqui se depreende que a IaaS é muito flexível. Pode aprovisionar uma infraestrutura comum, como as VMs, o armazenamento, as sub-redes virtuais, as firewalls e as VPNs, de modo a criar uma solução. Não precisa de gerir as aplicações e os servidores físicos. No entanto, é responsável pela gestão direta, ou seja, pela configuração e gestão dos componentes. Por exemplo, tem de configurar as firewalls, atualizar os SOs das VMs e atualizar o DBMS e os runtimes.

### <a name="common-scenarios"></a>Cenários comuns 

Vamos imaginar que a sua empresa de cuidados de saúde precisa de executar uma versão especial de software de ambiente de trabalho. O software só é suportado numa versão específica de um sistema operativo e só são necessários um utilizador e uma licença. Pode criar uma máquina virtual com o software necessário. O utilizador pode utilizar o ambiente de trabalho remoto para ligar à máquina virtual de modo a utilizar o software.

Vamos imaginar outro cenário. As suas equipas de desenvolvimento precisam de vários ambientes de desenvolvimento exclusivos. Isto porque precisam de testar várias versões do produto ao longo do ciclo de desenvolvimento. Os programadores podem aprovisionar os ambientes quando tal for necessário. Quando um determinado ambiente cessar a sua utilidade, pode ser facilmente eliminado.

Alguns outros cenários comuns incluem:

**Alojamento de sites:** se quiser exercer um maior controlo sobre o alojamento de um site, a execução de sites com a IaaS pode constituir uma opção melhor do que o tradicional alojamento na Web.

**Aplicações Web:** a IaaS fornece toda a infraestrutura necessária ao suporte de aplicações Web, incluindo servidores de aplicações, Web e de armazenamento, bem como recursos de rede. As organizações podem implementar rapidamente as aplicações Web na IaaS e aumentar ou reduzir verticalmente a infraestrutura com facilidade quando a procura das aplicações se mostrar imprevisível.

**Armazenamento, cópia de segurança e recuperação:** a gestão do armazenamento pode revelar-se uma questão complexa, que requer um grande investimento de capital e uma equipa qualificada para gerir os dados e cumprir os requisitos legais e de conformidade. A IaaS pode ajudar a simplificar o planeamento, a gestão, a procura imprevisível e o crescimento constante das necessidades de armazenamento.

**Computação de alto desempenho:** se tiver uma carga de trabalho que precisa de computação de alto desempenho pode executá-la na cloud, evitando assim os custos iniciais de hardware e pagando pela utilização apenas quando tal for necessário. 

**Análise de macrodados:** se tiver grandes conjuntos de dados que contêm padrões, tendências e associações potencialmente valiosos, a IaaS fornece a capacidade de processamento que permite explorar os conjuntos de dados de modo localizar os padrões.

### <a name="advantages"></a>Vantagens

**Elimina a despesa de capital e reduz os custos fixos:** a IaaS evita a despesa inicial inerente à configuração e gestão de um datacenter no local, o que faz dela uma opção económica para as empresas em início de atividade e empresas que testam novas ideias. Assim que toma a decisão de lançar um novo produto ou iniciativa, a infraestrutura de computação necessária pode ficar pronta numa questão de minutos ou horas, em vez dos dias ou semanas, por vezes meses até, que seriam necessários para estabelecer o processo internamente.

**Melhora a continuidade do negócio e a recuperação após desastre:** alcançar um nível de elevada disponibilidade, continuidade do negócio e recuperação após desastre é um processo dispendioso, uma vez que envolve um leque significativo de tecnologias e recursos humanos. No entanto, com o contrato de nível de serviço (SLA) certo em vigor, a IaaS pode reduzir este custo e permitir o acesso às aplicações e aos dados como habitualmente durante um desastre ou uma falha grave.

**Responder de forma mais rápida às mudanças das condições de negócio:** a IaaS permite-lhe aumentar verticalmente os recursos sem demora para acomodar picos de procura da sua aplicação (durante as férias, por exemplo) e, em seguida, voltar a reduzi-los verticalmente quando a atividade decresce a fim de poupar dinheiro. Tendo em conta que não precisa de configurar a infraestrutura primeiro para desenvolver e disponibilizar as suas aplicações, a IaaS permite-lhe fornecê-las aos utilizadores de forma mais rápida.

**Aumentar a estabilidade, a fiabilidade e a capacidade de suporte:** com a IaaS não é necessário manter e atualizar o software e o hardware nem resolver problemas de equipamento. Com o contrato adequado em vigor, o fornecedor de serviços garante que a sua infraestrutura é fiável e cumpre os SLAs.

## <a name="paas"></a>PaaS

A plataforma como um serviço é um ambiente de desenvolvimento e implementação completo na cloud. A PaaS permite-lhe criar e implementar seja o que for, desde aplicações simples com base na cloud a aplicações empresariais sofisticadas com capacidades da cloud. Os recursos são comprados junto de um fornecedor de serviços cloud segundo a modalidade pay as you go e o acesso aos mesmos é feito através de uma ligação segura à Internet. À semelhança da IaaS, a PaaS inclui uma infraestrutura, como servidores, armazenamento e rede. Além disso, também inclui middleware, ferramentas de desenvolvimento e outros serviços. A PaaS suporta o ciclo de vida completo das aplicações Web: criação, teste, implementação, gestão e atualização. Com a PaaS, não precisa de gerir as licenças de software, o middleware e a infraestrutura dos serviços. A si cabe-lhe a tarefa de gerir as aplicações e os serviços que desenvolve, o fornecedor de serviços cloud fará a gestão de tudo o resto.

### <a name="common-scenarios"></a>Cenários comuns

Vamos imaginar que a sua empresa de cuidados de saúde precisa de um site para descrever um produto. Os programadores querem utilizar o PHP. Com a PaaS, os programadores têm a opção de *criar uma aplicação Web*. Os detalhes da infraestrutura, como a criação de uma máquina virtual, a instalação de um servidor Web e a instalação do middleware são removidos. Não precisa de se preocupar com o sistema operativo utilizado nem com o hardware físico necessário. Os programadores implementam os ficheiros do site na cloud e o site fica disponível na Internet.

Vamos imaginar outro cenário. A sua empresa precisa de uma base de dados SQL para dar suporte a analistas de dados para um projeto especial. Porém, não tem a infraestrutura necessária para acomodar o pedido. Pode aprovisionar rapidamente um SQL Server na cloud que cumpra as necessidades do projeto. Deste modo, os analistas de dados pode ligar-se ao servidor. A base de dados do SQL Server é fornecida como um serviço. Deste modo, não tem de se preocupar com atualizações, patches de segurança ou com a otimização do armazenamento físico para operações de leitura e escrita.

Alguns outros cenários comuns incluem:

**Estrutura de desenvolvimento:** a PaaS fornece uma estrutura que pode servir de ponto de partida para o desenvolvimento ou personalização de aplicações com base na cloud por parte dos programadores. Muito à semelhança da forma como cria uma macro do Excel, a PaaS permite que os programadores criem as aplicações com base em componentes de software incorporados. Há certas funcionalidades da cloud que estão incluídas, como a escalabilidade, a elevada disponibilidade e a capacidade multi-inquilino, o que reduz a quantidade de codificação que os programadores têm de levar a cabo.

**Análise ou business intelligence:** as ferramentas de análise fornecidas como um serviço permitem-lhe analisar e extrair dados. As organizações podem encontrar informações e padrões que lhes permitem prever os resultados para melhorar a previsão, as decisões ao nível do design de produtos, os retornos sobre o investimento e outras decisões de negócio.

### <a name="advantages"></a>Vantagens

Ao fornecer a infraestrutura como um serviço, a PaaS oferece vantagens semelhantes às proporcionadas pela IaaS. No entanto, as funcionalidades adicionais que a acompanham, incluindo o middleware, as ferramentas de desenvolvimento e outras ferramentas empresariais, proporcionam ainda outras vantagens:

**Tempo de desenvolvimento reduzido:** as ferramentas de desenvolvimento de PaaS podem reduzir o tempo de desenvolvimento das novas aplicações. Os programadores podem utilizar componentes de aplicações pré-codificados incorporados na plataforma, como o fluxo de trabalho, os serviços de diretório, as funcionalidades de segurança e a pesquisa. Os componentes da plataforma como um serviço proporcionam novas capacidades à sua equipa de desenvolvimento sem que tenha de adicionar outros elementos com as competências necessárias à equipa.

**Desenvolver para várias plataformas:** alguns fornecedores de serviços disponibilizam opções de desenvolvimento para várias plataformas, como o ambiente de trabalho, dispositivos móveis e browsers, o que simplifica e agiliza o desenvolvimento de aplicações multiplataforma.

**Utilizar ferramentas sofisticadas a baixo custo:** com a modalidade pay as you go, tanto as pessoas a título individual como as organizações têm a possibilidade de utilizar software de desenvolvimento sofisticado e ferramentas de business intelligence e análise que, de outro modo, não poderiam adquirir.

**Suporte a equipas de desenvolvimento dispersas geograficamente:** uma vez que o ambiente de desenvolvimento é acedido através da Internet, as equipas de desenvolvimento podem trabalhar em conjunto nos projetos, mesmo quando os respetivos membros se encontram em localizações remotas.

**Gerir o ciclo de vida da aplicação de forma eficiente:** a PaaS fornece todas as capacidades de que precisa para suportar o ciclo de vida da aplicação Web completo: criação, teste, implementação, gestão e atualização, tudo dentro do mesmo ambiente integrado.

## <a name="saas"></a>SaaS

O software como um serviço permite que os utilizadores estabeleçam ligação e utilizem aplicações com base na cloud através da Internet. Entre os exemplos comuns contam-se as ferramentas de e-mail, de calendário e de produtividade como o Microsoft Office 365. O SaaS fornece uma solução de software completa que pode comprar segundo a modalidade pay as you go a um fornecedor de serviços cloud. O utilizador *aluga* a utilização de uma aplicação para a respetiva organização. Por sua vez, os utilizadores ligam-se ao serviço através da Internet, normalmente com um browser. Toda a infraestrutura subjacente, o middleware, o software da aplicação e os dados da aplicação estão localizados no datacenter do fornecedor de serviços. O fornecedor de serviços gere o hardware e o software e, com o contrato de serviços adequado, garante a disponibilidade e a segurança da aplicação e dos dados. Com o SaaS, a sua organização obtém uma aplicação prontamente operacional com custos iniciais mínimos.

Se já utilizou um serviço de e-mail baseado na Web antes, como o Outlook, o Hotmail ou o Yahoo! Mail, então já utilizou algo de parecido com SaaS. Com estes serviços, o utilizador inicia sessão na respetiva conta através da Internet, muitas vezes a partir de um browser. O software do e-mail está localizado na rede do fornecedor de serviços e as mensagens do utilizador também estão armazenadas aí. O utilizador pode aceder ao respetivo e-mail e às mensagens armazenadas a partir de um browser em qualquer computador ou dispositivo ligado à Internet.

### <a name="common-scenarios"></a>Cenários comuns

Vamos imaginar que a sua empresa de cuidados de saúde precisa de uma solução de CRM (gestão das relações com os clientes) para a equipa de vendas. A equipa está dispersa por todo o mundo. Pode utilizar um fornecedor de CRM com SaaS para implementar rapidamente uma solução para a equipa de vendas da sua organização.

Para fins de utilização por parte da organização, pode alugar aplicações de produtividade, como aplicações de e-mail, colaboração e calendário, bem como aplicações empresariais sofisticadas, como o CRM (gestão das relações com os clientes), o ERP (planeamento de recursos empresariais) e a gestão de documentos. A utilização destas aplicações é paga com base numa subscrição ou de acordo com o nível de utilização.

### <a name="advantages"></a>Vantagens

**Obter acesso a aplicações sofisticadas:** para fornecer aplicações SaaS aos utilizadores, não precisa de comprar, instalar, atualizar ou manter qualquer hardware, middleware ou software. O SaaS até permite o acesso a aplicações empresariais sofisticadas, como o ERP e CRM, a baixo custo às organizações que não dispõem dos recursos financeiros para comprar, implementar e gerir a infraestrutura e o software necessários.
Pague apenas por aquilo que utiliza. Também poupa dinheiro uma vez que o serviço SaaS permite aumentar e reduzir verticalmente a respetiva dimensão de forma automática, de acordo com o nível de utilização.

**Utilizar software de cliente gratuito:** os utilizadores podem executar a maioria das aplicações SaaS diretamente a partir do respetivo browser sem precisar de transferir e instalar qualquer software. Não precisa de comprar ou implementar o software de cliente para os seus utilizadores.

**Mobilizar facilmente a força de trabalho:** os utilizadores podem aceder aos dados e às aplicações SaaS a partir de qualquer dispositivo móvel ou computador ligado à Internet. Os esforços do fornecedor de serviços incidem sobre o fornecimento do serviço aos dispositivos.

**Aceder aos dados da aplicação a partir de qualquer lugar:** com os dados armazenados na cloud, os utilizadores podem aceder às respetivas informações a partir de qualquer dispositivo móvel ou computador ligado à Internet. Além disso, quando os dados da aplicação estão armazenados na cloud, não há o risco de perda de dados em caso de falha do dispositivo ou computador de um utilizador.