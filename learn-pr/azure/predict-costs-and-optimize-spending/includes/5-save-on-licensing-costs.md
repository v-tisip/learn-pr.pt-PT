O licenciamento é outra área que pode afetar consideravelmente os seus gastos na cloud. Vamos analisar algumas formas de reduzir os custos de licenciamento.

## <a name="azure-hybrid-benefit-for-windows-server"></a>Benefício Híbrido do Azure para o Windows Server

Muitos clientes fizeram um investimento em licenças do Windows Server e gostariam de reutilizar esse investimento no Azure. O Benefício Híbrido do Azure permite aos clientes utilizar estas licenças para as máquinas virtuais no Azure. Isto significa que não lhe será cobrada a licença do Windows Server e, em vez disso, será cobrada a taxa do Linux. 

Para ser elegível para este benefício, as suas licenças do Windows têm de estar abrangidas pelo Software Assurance. Também serão aplicadas as seguintes diretrizes:

- Cada licença de dois processadores ou cada conjunto de licenças de 16 núcleos tem direito a duas instâncias de até 8 núcleos ou uma instância de até 16 núcleos. 
- As licenças da Standard Edition só podem ser utilizadas uma vez no local ou no Azure. Isto significa que não pode utilizar a mesma licença para uma VM do Azure e um computador local.
- Os benefícios da Datacenter Edition permitem a utilização simultânea no local e no Azure, pelo que a licença abrangerá duas máquinas do Windows em execução. 

> [!NOTE]
> Normalmente, a maioria dos clientes estão licenciados por núcleo, pelo que utilizará esse modelo para o cálculo. Se tiver dúvidas sobre as licenças que possui, contacte o seu revendedor de licenças ou a equipa de contas da Microsoft.

Aplicar o benefício é fácil. Pode ser ativado e desativado em qualquer altura nas VMs existentes ou aplicado no momento da implementação de novas VMs. O Benefício Híbrido (sobretudo quando combinado com instâncias reservadas) pode permitir uma poupança substancial em termos de licenças.

## <a name="azure-hybrid-benefit-for-sql-server"></a>Benefício Híbrido do Azure para o SQL Server

O Benefício Híbrido do Azure para o SQL Server ajuda-o a maximizar o valor dos seus investimentos de licenciamento atuais e acelerar a sua migração para a cloud. O Benefício Híbrido do Azure para o SQL Server é um benefício baseado no Azure que lhe permite utilizar as suas licenças do SQL Server com o Software Assurance ativo para pagar uma taxa reduzida.

Pode aplicar este benefício mesmo se o recurso do Azure estiver ativo, mas será aplicada a taxa reduzida desde que for selecionado no portal. Não será emitido nenhum crédito retroativamente.

### <a name="azure-sql-database-vcore-based-options"></a>Opções baseadas em vCore da Base de Dados SQL do Azure

![Troca de licenças do SQL Server](../images/sql-tradein-value.jpg)

Para a Base de Dados SQL do Azure, o Benefício Híbrido do Azure funciona da seguinte forma:

- Se tiver a Standard Edition por licenças de núcleo com o Software Assurance ativo, pode obter um vCore no escalão de serviço Fins Gerais para cada núcleo de uma licença que tiver no local.
- Se tiver a Enterprise Edition por licenças de núcleo com o Software Assurance ativo, pode obter um vCore no escalão de serviço Crítico para a Empresa para cada núcleo de uma licença que tiver no local. Tenha em atenção que o Benefício Híbrido do Azure para o SQL Server para o escalão de serviço Crítico para a Empresa está disponível apenas para clientes com licenças da Enterprise Edition.
- Se tiver a Enterprise Edition altamente virtualizada por licenças de núcleo com o Software Assurance ativo, pode obter quatro vCores no escalão de serviço Fins Gerais para cada núcleo de uma licença que tiver no local. Este é um benefício de virtualização exclusivo disponível apenas para a Base de Dados SQL do Azure.

Para o SQL Server em Máquinas Virtuais do Azure, o Benefício Híbrido do Azure funciona da seguinte forma:

- Se tiver a Enterprise Edition por licenças de núcleo com o Software Assurance ativo, pode obter um núcleo da Enterprise Edition do SQL Server em Máquinas Virtuais do Azure para cada núcleo de uma licença que tiver no local.
- Se tiver a Standard Edition por licenças de núcleo com o Software Assurance ativo, pode obter um núcleo da Standard Edition do SQL Server em Máquinas Virtuais do Azure para cada núcleo de uma licença que tiver no local.

Isto pode ter um impacto dramático nos gastos do Azure com cargas de trabalho do SQL Server.

## <a name="use-devtest-subscription-offers"></a>Utilizar ofertas de subscrição Dev/Test

As ofertas [Dev/Test Enterprise](https://azure.microsoft.com/offers/ms-azr-0148p/) e [Dev/Test Pay As You Go](https://azure.microsoft.com/offers/ms-azr-0023p/) são um benefício que pode aproveitar para reduzir os custos nos seus ambientes de não produção. Este benefício dá-lhe vários descontos, nomeadamente para cargas de trabalho do Windows, o que permite eliminar cobranças de licenças e faturar apenas à taxa do Linux para máquinas virtuais. Isto aplica-se também ao SQL Server e qualquer outro software da Microsoft abrangido por uma subscrição do Visual Studio (anteriormente conhecido como MSDN). Existem alguns requisitos para este benefício como, por exemplo, ser apenas para cargas de trabalho de não produção e todos os utilizadores destes ambientes (excluindo os testadores) terem de ser abrangidos por uma subscrição do Visual Studio. Em resumo, para cargas de trabalho de não produção, isto permite-lhe poupar dinheiro nas cargas de trabalho de máquinas virtuais do Windows, SQL Server e Microsoft.
Seguem-se todos os detalhes de cada oferta. Se for um cliente num Contrato Enterprise, pode tirar partido da oferta Dev/Test Enterprise. Se for um cliente sem um Contrato Enterprise e estiver a utilizar contas PAYG, pode aproveitar a oferta Dev/Test Pay As You Go.

## <a name="bring-your-own-sql-server-license"></a>Traga a sua própria licença do SQL Server

Se for um cliente num Contrato Enterprise e já tiver um investimento em licenças do SQL Server, e estas tiverem sido libertadas como parte da movimentação dos recursos para o Azure, pode aprovisionar imagens **traga a sua própria licença** (BYOL) no Azure Marketplace, o que lhe permite tirar partido destas licenças não utilizadas e reduzir o custo de VMs do Azure. Sempre foi possível fazer isto ao aprovisionar uma VM do Windows e ao instalar manualmente o SQL Server, mas isto simplifica o processo de criação ao tirar partido de imagens certificadas pela Microsoft. Procure **BYOL** no Marketplace para encontrar essas imagens.

![BYOL para o SQL Server no Azure](../images/byol-sql-server.png)

> [!IMPORTANT]
> É necessária uma subscrição do Contrato Enterprise para utilizar imagens BYOL certificadas.

## <a name="use-sql-server-developer-edition"></a>Utilizar o SQL Server Developer Edition

Muitas pessoas não estão cientes de que o SQL Server Developer Edition é um produto gratuito para **utilização de não produção**. A Developer Edition tem as mesmas funcionalidades da Enterprise Edition. No entanto, para cargas de trabalho de não produção, pode reduzir drasticamente os custos de licenciamento.

Procure as imagens do SQL Server para a Developer Edition no Azure Marketplace e utilize-as para fins de desenvolvimento ou teste para eliminar o custo adicional para o SQL Server nestes casos. 

> [!NOTE]
> Para obter informações de licenciamento completas, veja a [documentação de orientação sobre preços](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-pricing-guidance).

## <a name="use-constrained-instance-sizes-for-database-workloads"></a>Utilizar tamanhos de instância restringidos para cargas de trabalho de base de dados 

Muitos clientes têm requisitos de memória, armazenamento ou largura de banda de E/S elevados, mas um baixo número de núcleos de CPU. Com base neste pedido popular, a Microsoft disponibilizou os tamanhos de VM mais populares (DS, ES, GS e MS) em novos tamanhos que restringem o número de vCPUs para metade ou um terço do tamanho de VM original, o que permite manter a mesma memória, armazenamento e largura de banda de E/S.

| Tamanho da VM | vCPUs | Memória | Máximo de discos | Débito máximo de E/S | Custo de licenciamento do SQL Server Enterprise por ano | Custo total por ano (computação + licenciamento) |
|---------|-------|--------|-----------|--------------------|-----------------------------------------------|---------------------------|
| Standard_DS14v2   | 16 | 112 GB | 32 | 51 200 IOPS ou 768 MB/s |           |           |
| Standard_DS14-4v2 | **4**  | 112 GB | 32 | 51 200 IOPS ou 768 MB/s | Menos 75% | Menos 57% |
| Standard_GS5      | 32 | 448    | 64 | 80 000 IOPS ou 2 GB/s   |           |           |
| Standard_GS5-8    | **8**  | 448    | 64 | 80 000 IOPS ou 2 GB/s   | Menos 75% | Menos 42% |

Uma vez que os produtos de base de dados, como o SQL Server e Oracle, são licenciados por CPU, isto permite aos clientes reduzir o custo de licenciamento até 75%, mas continuar a manter o elevado desempenho necessário para a base de dados. 
