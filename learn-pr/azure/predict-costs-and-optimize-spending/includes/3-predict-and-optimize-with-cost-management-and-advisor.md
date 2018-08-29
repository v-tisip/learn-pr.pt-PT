Aprendemos a estimar os custos antes de implementar serviços no Azure, mas e se já tiver recursos implementados? Como obter visibilidade sobre os custos que já está a acumular? Se tivermos implementado a nossa solução anterior no Azure e agora queremos ter a certeza de que dimensionámos adequadamente as máquinas virtuais e prevermos quanto seria a conta, como podemos fazê-lo? Vamos ver algumas ferramentas no Azure que pode utilizar para ajudar a resolver este problema.

## <a name="what-is-azure-advisor"></a>O que é o Assistente do Azure? 

**O Assistente do Azure** é um serviço gratuito integrado no Azure que oferece recomendações sobre elevada disponibilidade, segurança, desempenho e custo. O Assistente analisa os serviços implementados e procura formas de melhorar o seu ambiente entre essas quatro áreas. Vamos concentrar-nos nas recomendações de custos, mas também irá precisar de rever as outras recomendações.

O Assistente faz recomendações de custos nas seguintes áreas: 

1. **Reduza os custos ao eliminar circuitos não aprovisionados do Azure ExpressRoute.** 
    Isto identifica os circuitos do ExpressRoute que já estão no estado de fornecedor *Não Aprovisionado* ha mais de um mês e recomenda eliminar o circuito se não estiver a planear aprovisioná-lo com a conectividade fornecedor.

2. **Compre instâncias reservadas para poupar dinheiro em pay as you go.** 
    Isto irá rever a utilização da máquina virtual durante os últimos 30 dias e determinar se poderia poupar dinheiro no futuro ao comprar instâncias reservadas. O Assistente irá mostrar as regiões e os tamanhos em que potencialmente tem a maioria das poupanças e irá mostrar a poupança estimada que poderá obter na compra de instâncias reservadas.
    
3. **Dimensionamento correto ou encerramento de máquinas virtuais subutilizadas.** 
    Isto monitoriza a utilização da máquina virtual durante 14 dias e, em seguida, identifica as máquinas virtuais de baixa utilização. As máquinas virtuais cuja utilização média da CPU é de 5 por cento ou menos e a utilização de rede é de 7 MB ou menos para quatro ou mais dias são consideradas máquinas virtuais de baixa utilização. O limiar de utilização média da CPU é ajustável até 20 por cento. Ao identificar estas máquinas virtuais subutilizadas, pode optar por redimensioná-las para um tipo de instância mais pequena e reduzir os custos.

Vamos ver onde pode encontrar o Assistente do Azure no portal. Primeiro, inicie sessão no portal do Azure em [https://portal.azure.com](https://portal.azure.com). Clique em **Todos os Serviços** e, na categoria **Ferramentas de Gestão**, verá o **Assistente**. Também pode escrever **Assistente** na caixa de filtro para filtrar apenas esse serviço. 

Clique no Assistente e será direcionado para o dashboard de recomendações do Assistente em que pode ver todas as recomendações da sua subscrição. Verá uma caixa para cada categoria de recomendações. 

> [!NOTE]
> Poderá não ter quaisquer recomendações de custos no Assistente. Isto pode acontecer porque as avaliações ainda não foram concluídas ou simplesmente porque não existem recomendações no Assistente.

![Recomendações do Assistente](../images/advisor-recommendations.png)

Clicar na caixa **Custo** irá levá-lo para as recomendações detalhadas, onde pode ver as recomendações que se encontram no Assistente.

![Recomendações de custos do Assistente](../images/advisor-cost-recommendations.png)

Clicar em qualquer recomendação irá levá-lo para os detalhes dessa recomendação específica. Em seguida, poderá tomar medidas específicas, como redimensionar máquinas virtuais para reduzir os gastos.

![Recomendação de redimensionamento de VM do Assistente](../images/advisor-resize-vm.png)

Estas recomendações são todos os lugares onde pode gastar dinheiro de forma ineficiente. São um ótimo lugar para começar e continuar a rever ao procurar locais para reduzir os custos. No nosso exemplo, há uma oportunidade para pouparmos aproximadamente $ 700 por mês, se seguirmos estas recomendações. Esta poupança aumenta, portanto não se esqueça de a rever periodicamente para obter recomendações nas quatro áreas.

## <a name="azure-cost-management"></a>Gestão de Custos do Azure

O Azure Cost Management é outra ferramenta gratuita e interna do Azure que pode servir para obter mais informações sobre onde irá o seu dinheiro na cloud. Pode ver o histórico de quebras dos serviços em que está a gastar o seu dinheiro e como ele está a acompanhar face aos orçamentos definidos. Pode definir orçamentos, agendar relatórios e analisar as suas áreas de custo.

![Gestão de Custos](../images/cost-management.png)

## <a name="cloudyn"></a>Cloudyn 

A Cloudyn, uma subsidiária da Microsoft, permite-lhe controlar a utilização da cloud e as despesas dos seus recursos do Azure e outros fornecedores de cloud, incluindo a Amazon Web Services e a Google. Os relatórios do dashboard fáceis de compreender também ajudam na alocação de custos e showbacks ou estornos. O Cost Management ajuda a otimizar os gastos da cloud ao identificar recursos subutilizados que possa gerir e ajustar. A utilização do Azure é gratuita, e existem opções pagas para o suporte premium e para ver os dados a partir de outras clouds. 

![Dashboard de gestão da Cloudyn](../images/cloudyn-mgt-dash.png)

## <a name="summary"></a>Resumo

Como pode ver, existem várias ferramentas disponíveis gratuitas no Azure que pode utilizar para controlar e prever os gastos da sua cloud, e identificar onde o seu ambiente pode ser ineficiente de uma perspetiva de custo. Deverá certificar-se de que é uma prática comum rever os relatórios e as recomendações que estas ferramentas disponibilizam, para que possa desbloquear as poupanças nos seus requisitos de espaço na cloud. Agora vamos ver algumas das melhores práticas para reduzir os custos de infraestrutura.
