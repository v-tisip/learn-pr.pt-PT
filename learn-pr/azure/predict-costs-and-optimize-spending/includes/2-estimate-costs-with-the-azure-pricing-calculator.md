Imagine que lhe foi pedido para criar um sistema no Azure e tem de dar uma estimativa do custo de execução nos próximos 12 meses. Já sabe que os preços do Azure são totalmente transparentes e é cobrado mensalmente apenas os serviços que utilizar. Como fará essa estimativa sem implementar e executar esses serviços ou sem estipular preços manualmente para cada serviço na página de preços de serviços do Azure? 

## <a name="introducing-the-azure-pricing-calculator"></a>Introdução à calculadora de preços do Azure

Para facilitar a criação de estimativas para os clientes, a Microsoft desenvolveu a **calculadora de preços do Azure**. A calculadora de preços do Azure é uma ferramenta baseada na Web gratuita que lhe permite introduzir serviços do Azure e modificar as propriedades e opções dos serviços. Produz os custos por serviço e o custo total da estimativa completa.

Noutra janela do browser ou separador, aceda à [calculadora de preços do Azure](https://azure.microsoft.com/pricing/calculator/). Na página da calculadora de preços, verá três separadores:

1. **Produtos.** Este separador é onde fará a maior parte da sua atividade. Este separador tem todos os serviços do Azure listados e é onde vai adicionar ou remover serviços para formular a sua estimativa.
2. **Estimativas.** Este separador tem todas as estimativas guardadas anteriormente. Explicaremos este processo daqui a pouco.
3. **FAQ.** Tal como o nome indica, este separador tem respostas a algumas perguntas mais frequentes.

Vamos começar pelo separador **Produtos**. Verá a lista completa das categorias de serviço na parte inferior esquerda. Clicar em qualquer uma das categorias apresentará os serviços nessa categoria. Existe também uma caixa de pesquisa onde pode procurar o serviço que deseja em todos os serviços. Clicar no serviço vai adicioná-lo à estimativa. Pode adicionar apenas um serviço ou quantos forem necessários, incluindo múltiplos do mesmo serviço (por exemplo, várias máquinas virtuais). 

Depois de adicionar os serviços, vai querer definir um preço. Desloque-se para baixo na página para ver detalhes personalizáveis desse serviço aplicáveis aos preços. Por exemplo, nas máquinas virtuais, pode selecionar detalhes como a região, o sistema operativo e o tamanho de instância, os quais afetarão os preços da VM. Verá um subtotal do serviço. Se deslocar ainda mais para baixo, verá o total de todos os serviços incluídos na estimativa. Juntamente com o total, verá botões onde pode exportar, guardar e partilhar a estimativa.

## <a name="estimate-a-solution"></a>Estimar uma solução

No nosso cenário original, vamos imaginar que este sistema será executado em duas VMs do Azure e vai ligar a uma instância da Base de Dados SQL do Azure. Queremos também uma firewall de 7 camadas para assegurar as seguintes capacidades de balanceamento de carga melhoradas:

![Diagrama da arquitetura do sistema](../images/estimate-costs-architecture.png)

Podemos utilizar a calculadora de preços do Azure para descobrir quanto custará a solução e exportar a estimativa para partilhar com a equipa.

> [!NOTE]
> Certifique-se de que tem uma calculadora sem nada indicado na estimativa. Se tiver algum dado na estimativa, clique no ícone de lixo em cada item para repor a estimativa.

Na calculadora de preços do Azure, no separador **Produtos**, adicione os seguintes serviços à estimativa ao clicar nos mesmos:

- Virtual Machines
- Base de Dados SQL do Azure
- Gateway de Aplicação

Podemos configurar os detalhes de cada um, no separador **Estimativas**, para obter uma estimativa sólida dos custos. Utilize a região **EUA Oeste** para todos os recursos.

* **Máquinas Virtuais.** Trata-se de uma aplicação ASP.NET, pelo que vamos ter de utilizar uma VM com o **SO Windows**. Esta aplicação não requer uma quantidade enorme de poder de computação, por isso, selecione o tamanho de instância **D2v3**. Vamos precisar de duas máquinas virtuais que serão executadas continuamente (730 horas/mês). Vamos utilizar o armazenamento SSD premium para estas VM e precisar apenas de um disco por VM do tamanho **E10**, num total de dois discos. 

* **Base de Dados SQL.** Para a base de dados, vamos aprovisionar um **único tipo de base de dados** com o modelo **vCore**. Queremos para uma base de dados de Fins Gerais de Ger 4 com 4 vCores. Vamos precisar de 32 GB de armazenamento com uma média de 16 GB de armazenamento. A nossa política de retenção será de oito semanas, 12 meses e cinco anos. 

* **Gateway de Aplicação.** Para o Gateway de Aplicação, vamos utilizar o escalão Firewall de Aplicação Web, para termos alguma proteção para o nosso ambiente. Vamos ficar com apenas duas instâncias e um tamanho médio, uma vez que a nossa carga não será elevada. Esperamos processar 1 TB de dados por mês.

Ao analisar a estimativa, deverá ver um resumo do custo para cada serviço que adicionou e um total para toda a estimativa. Neste caso, a estimativa deve ser de aproximadamente **1 400,00 $ por mês**. Pode experimentar algumas das opções para ver a estimativa subir e descer.

## <a name="share-and-save-your-estimate"></a>Partilhar e guardar a estimativa

Temos agora uma estimativa para a nossa solução. Podemos guardá-la, para podermos analisá-la mais tarde e fazer ajustes, se necessário, exportá-la para o Excel para análise adicional e partilhá-la através de um URL. 

Para exportar a estimativa, clique em `Export` na parte inferior da estimativa. Isto vai transferir a estimativa no formato do Excel (**.xlsx**) e incluir todos os serviços que adicionou à estimativa.

Podemos partilhar a folha de cálculo do Excel ou clicar no botão `Share` na calculadora. Isto gera um URL que pode utilizar para partilhar a estimativa. Qualquer pessoa com esta ligação poderá aceder à mesma, o que facilita a partilha com a sua equipa.

Se tiver iniciado sessão com a sua conta do Azure, pode guardar a estimativa de forma a poder analisá-la mais tarde. Clique no botão **Guardar**. Se tem sessão iniciada, deverá ver uma notificação de que a estimativa foi guardada. Se não tiver sessão iniciada, verá uma mensagem para iniciar sessão para guardar a estimativa. Depois de guardar a estimativa, desloque-se até ao topo da página e selecione o separador **Estimativas**. Verá a estimativa aí. Em seguida, pode selecioná-la para efetuar uma cópia de segurança ou eliminá-la, se já não precisar dela.

## <a name="summary"></a>Resumo

Chegámos a uma estimativa de custos para um conjunto de serviços do Azure sem gastar dinheiro. Não criámos nada e temos uma estimativa totalmente partilhável que podemos analisar melhor ou fazer modificações no futuro. Pode utilizar este procedimento não só para criar estimativas para sistemas com serviços específicos que planeia utilizar, mas também para comparar a forma como os diferentes serviços podem afetar os custos globais. Um exemplo é o Microsoft SQL Server numa VM vs. Base de Dados SQL do Azure. Agora, vamos ver como podemos obter informações sobre os custos dos serviços já implementados.