Se quiser saber o que pode correr mal ao gerir os segredos de configuração de uma aplicação, veja a história de Steve, programador sénior.

Steve trabalhava há algumas semanas numa empresa de entrega de alimentos para animais de estimação. Estava a ver informações sobre a aplicação Web da empresa, uma aplicação Web .NET Core que utiliza uma base de dados Azure SQL para armazenar informações de encomendas e APIs de terceiros para faturação de cartões de crédito e mapeamento de endereços de clientes, quando colou acidentalmente a cadeia de ligação para a base de dados de encomendas num fórum público.

Alguns dias mais tarde, o departamento de contabilidade reparou que a empresa estava a entregar muitos alimentos para animais que ninguém pagava. Alguém utilizou a cadeia de ligação para aceder à base de dados, efetuou engenharia reversa no esquema e fez encomendas sem recurso ao site.

Quando se apercebeu do erro, Steve apressou-se a mudar a palavra-passe da base de dados para expulsar o atacante e quebrou o site. Iniciou sessão diretamente no servidor da aplicação e mudou a configuração da aplicação em vez de voltar a implementar, mas o servidor continuava a mostrar pedidos falhados.

Steve esqueceu-se de que havia múltiplas instâncias da aplicação em diferentes servidores e que só tinha alterado a configuração de uma. Foi necessário voltar a implementar tudo, causando mais 30 minutos de inatividade.

A divulgação de uma cadeia de ligação de base de dados, chave de API ou palavra-passe de serviço pode ser catastrófica. Os dados roubados ou eliminados, os danos financeiros, o tempo de inatividade das aplicações e danos irreparáveis aos ativos empresariais são alguns dos potenciais resultados. Infelizmente, é frequente ter de se implementar valores secretos em múltiplos locais e em simultâneo, e alterá-los em alturas inoportunas. E têm de ser armazenados em *algum* lado! Vejamos como podemos proteger todos estes dados com o Azure KeyVault.

## <a name="learning-objectives"></a>Objetivos de Aprendizagem
> [!div class="checklist"]
> * Entender os tipos de informações que podem ser armazenados no Azure KeyVault
> * Criar um arquivo do Azure KeyVault
> * Autenticar com o Azure KeyVault
> * Aceder a segredos num Azure KeyVault