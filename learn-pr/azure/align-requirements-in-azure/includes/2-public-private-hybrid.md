Imagine que trabalha numa empresa de cuidados de saúde. Tem sistemas legados, sistemas de linha de negócio e planos para novos sistemas no futuro. Ouviu falar das vantagens em utilizar a informática na cloud. Que critérios deve utilizar para escolher o melhor modelo de implementação das diferentes soluções de cloud pública, privada e híbrida?

## <a name="what-is-cloud-computing"></a>O que é a informática na cloud?

A informática na cloud é o aprovisionamento de serviços e aplicações a pedido através da Internet. Servidores, aplicações, dados e outros recursos são fornecidos como um serviço. 

Os detalhes dos serviços são removidos no que se refere ao utilizador. Pode aprovisionar rapidamente os recursos de computação e utilizar o serviço com um nível mínimo de gestão. Não deve encarar a informática na cloud como um datacenter disponível através da Internet. A informática na cloud utiliza virtualização, hardware de baixo custo e processos automatizados para proporcionar uma experiência de utilizador personalizada aos clientes semelhante à de um utilitário público. 

Existem três modelos de implementação para a informática na cloud: cloud pública, cloud privada e cloud híbrida.

![Modelos de implementação da cloud](../media/2-cloud-deployment.png)

## <a name="public-cloud"></a>Cloud pública

As clouds públicas são a forma mais comum de implementar a informática na cloud. Os serviços são oferecidos através da Internet pública e estão disponíveis para todos aqueles que os queiram comprar. Os recursos da cloud, como os servidores e o armazenamento, além de pertencem a um fornecedor de serviços cloud de terceiros são geridos pelo mesmo e fornecidos através da Internet. Os serviços podem ser gratuitos ou vendidos a pedido, o que permite que os clientes paguem apenas pela utilização dos ciclos de CPU, armazenamento ou largura de banda que consomem. O Microsoft Azure é um exemplo de cloud pública. 

Vamos imaginar que a sua empresa de cuidados de saúde precisa de um site de inscrição. O site tem de contemplar o dimensionamento e ter capacidade de resposta durante os picos de inscrição várias vezes ao longo do ano. Os clientes acedem ao site a partir de localizações em todo o mundo. Pode utilizar a cloud pública para aumentar verticalmente de forma automática a fim de satisfazer a procura durante os picos de inscrição. Quando o tráfego do site é baixo, o site pode reduzir verticalmente para poupar nos custos. O site tem capacidade de resposta durante os picos de procura e só paga um maior número de recursos quando necessário. Também pode implementar o seu site em várias regiões geográficas para aumentar a fiabilidade e a capacidade de resposta.

No decorrer do desenvolvimento do site, convém que os programadores criem vários ambientes de desenvolvimento para acelerar o processo de desenvolvimento. Os programadores podem utilizar a cloud pública para aprovisionar rapidamente as máquinas virtuais para ambientes em sandbox de modo a desenvolverem uma solução. Quando um ambiente cessar a sua utilidade, os programadores podem eliminá-lo.

### <a name="why-public-cloud"></a>Porquê considerar a cloud pública?

As clouds públicas permitem uma implementação mais rápida do que as infraestruturas no local e com uma plataforma quase infinitamente dimensionável. Todos os empregados de uma empresa podem utilizar a mesma aplicação em qualquer escritório ou sucursal com o seu próprio dispositivo de eleição, desde que possam aceder à Internet. 

Exemplos que explicam as vantagens de utilizar a cloud pública:

- **Consumo do serviço a pedido conforme necessário ou através de uma subscrição:** o modelo a pedido ou de subscrição permite-lhe pagar a fração da CPU, armazenamento e outros recursos que utiliza ou reserva.
- **Sem investimento inicial de hardware:** não existem requisitos para comprar, gerir e manter o hardware no local e a infraestrutura da aplicação. O fornecedor de serviços cloud é responsável por toda a gestão e manutenção do sistema. 
- **Automatização:** aprovisione rapidamente os recursos da infraestrutura através um portal Web, de scripts ou de forma automática. 
- **Dispersão geográfica:** a localização de dados nas proximidades é necessária, sem ter muitos dos seus próprios datacenters.
- **Manutenção de hardware reduzida:** o fornecedor de serviços é responsável pela manutenção do hardware.

## <a name="private-cloud"></a>Cloud privada

Uma cloud privada consiste nos recursos de computação utilizados exclusivamente por utilizadores selecionados de uma empresa ou organização. Pode estar localizada fisicamente no datacenter no local da sua organização ou pode estar alojada por um fornecedor de serviços de terceiros. O termo cloud privada não deve ser encarado como uma mudança de nome dos datacenters no local tradicionais. Uma cloud privada utiliza serviços e uma infraestrutura no local para fornecer benefícios semelhantes aos da cloud pública. A cloud privada utiliza uma plataforma de abstração para fornecer serviços *segundo os parâmetros da cloud*, como os clusters de Kubernetes, ou um ambiente na cloud completo, como o Azure Stack. A organização é responsável pela compra, configuração e manutenção do hardware. A comunicação entre os sistemas processa-se normalmente na infraestrutura da rede que pertence à empresa e que esta mantém. Por exemplo, uma rede interna privada ou uma ligação de fibra ótica dedicada entre edifícios.

Imagine que trabalha numa empresa de cuidados de saúde e que tem uma aplicação que está a ser utilizada num dos seus datacenters. O ambiente operativo não pode ser replicado na cloud pública. Há um novo requisito para aceder aos dados que se encontram noutro datacenter. A base de dados que contém os dados tem de permanecer no outro site devido a questões de conformidade regulamentar. Este cenário é uma cloud privada. Tem dois datacenters de que a sua organização é proprietária. Poderia utilizar uma VPN de cloud pública na Internet para ligar os datacenters. No entanto, o cenário seria considerado uma cloud privada, uma vez que a solução é privada e pertence à organização.

### <a name="why-private-cloud"></a>Porquê considerar a cloud privada?

Uma cloud privada pode proporcionar maior flexibilidade a uma organização. A sua organização pode personalizar o respetivo ambiente na cloud para dar resposta a necessidades de negócio específicas. Uma vez que os recursos não são partilhados com outras pessoas, é possível alcançar níveis de controlo e segurança mais elevados. Além disso, as clouds privadas podem proporcionar um certo nível de escalabilidade e eficiência.

Exemplos que explicam as vantagens de utilizar a cloud privada:

- **Ambiente pré-existente:** um ambiente operativo existente que não pode ser replicado na cloud pública. Um amplo investimento em hardware e empregados com conhecimentos especializados da solução. Uma organização de grande dimensão pode optar por comercializar os respetivos recursos de computação a baixo custo.
- **Aplicações legadas:** aplicações empresariais legadas essenciais que não podem ser transferidas fisicamente com facilidade.
- **Segurança e soberania dos dados:** a localização física dos dados por ser ditada por fronteiras políticas e requisitos legais.
- **Conformidade regulamentar/certificação:** conformidade PCI ou HIPAA. Datacenter no local certificado.

## <a name="hybrid-cloud"></a>Nuvem híbrida

Uma cloud híbrida é um ambiente informático que combina uma cloud pública e uma cloud privada, permitindo a partilha de dados e aplicações entre elas. Quando há uma flutuação na procura de computação e de processamento, a informática na cloud híbrida proporciona às empresas a capacidade de aumentarem verticalmente a respetiva infraestrutura no local para a cloud pública, de forma totalmente integrada, de modo a lidarem com qualquer capacidade excedida, sem que seja concedido aos datacenters de terceiros acesso à totalidade dos seus dados. As organizações ficam a ganhar com a flexibilidade e a capacidade de computação da cloud pública para as tarefas de computação básicas e não confidenciais, ao mesmo tempo que mantêm as aplicações críticas para o negócio e os dados no local em segurança e protegidos por uma firewall da empresa.

A utilização de uma cloud híbrida ajuda a eliminar a necessidade de incorrer em despesas de investimento iniciais para fazer face a picos de procura temporários. A sua flexibilidade também permite gerir os recursos que são locais na cloud. As empresas pagam apenas pelos recursos que utilizam temporariamente, em vez de terem de comprar, programar e manter recursos e equipamentos adicionais que podem permanecer inativos durante longos períodos de tempo. Regra geral, a integração é feita por meio de uma VPN segura entre o fornecedor de cloud, como o Azure, e o datacenter no local.

Imagine que trabalha numa empresa de cuidados de saúde e que tem uma aplicação através da qual os clientes podem aceder às respetivas informações de cuidados de saúde. Um regulamento estabelece que os dados têm de permanecer numa localização física. O site do cliente tem de ter capacidade de resposta para os seus muitos utilizadores dispersos pelo mundo.  A solução pode passar pelo alojamento da base de dados num datacenter no local e o alojamento do site na cloud pública. Por sua vez, é utilizada uma VPN entre o datacenter no local e a cloud pública. Este cenário pode ser considerado uma cloud híbrida.

### <a name="why-hybrid-cloud"></a>Porquê considerar a cloud híbrida?

A cloud híbrida permite à sua organização controlar e manter uma infraestrutura privada para recursos confidenciais. Também lhe proporciona a flexibilidade de tirar partido dos recursos adicionais existentes na cloud pública quando precisar deles. Com a capacidade de dimensionar para a cloud pública, paga pelo poder de computação adicional apenas quando tal for necessário. Isto também pode facilitar a transição para a cloud. Pode migrar de forma gradual, implementando lentamente as cargas de trabalho ao longo do tempo.

Exemplos que explicam as vantagens de utilizar a cloud híbrida:

- **Investimento em hardware existente:** imperativos de ordem empresarial ditam a necessidade de utilizar o ambiente operativo e hardware existentes.
- **Requisitos de regulamentação:** a regulamentação estabelece que os dados têm de permanecer numa localização física.
- **Ambiente operativo exclusivo:** a cloud pública não consegue replicar o ambiente operativo legado.
- **Migração:**: mover as cargas de trabalho para a cloud ao longo do tempo.
