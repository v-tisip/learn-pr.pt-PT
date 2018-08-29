O Azure Key Vault utiliza o **Azure Active Directory** para autenticar os utilizadores e as aplicações que tentam aceder a um cofre. Para conceder acesso à aplicação Web ao cofre, primeiro é necessário registar a aplicação no Azure Active Directory. O registo cria uma identidade para a aplicação. Assim que existir uma identidade, podemos atribuir-lhe as permissões do cofre.

As aplicações e os utilizadores são autenticados no Key Vault com um token de autenticação do Azure Active Directory. Obter um token do Azure Active Directory requer um segredo ou certificado, uma vez que qualquer pessoa com um token pode utilizar a identidade da aplicação para aceder a todos os segredos existentes no cofre.

Os segredos da aplicação estão protegidos no cofre, mas ainda é necessário manter um segredo ou certificado fora do cofre para poder aceder-lhes! Este problema é denominado *problema de arranque*  e o Azure tem uma solução.

## <a name="managed-service-identity"></a>Identidade do Serviço Gerido

A *Identidade do Serviço Gerido* (MSI) é uma funcionalidade do Serviço de Aplicações do Azure que a aplicação pode utilizar para aceder ao Key Vault e outros serviços do Azure sem ter de gerir um único segredo. A utilização do MSI é mais simples e segura do que gerir um segredo por si.

Quando ativar o MSI, o Azure ativa um serviço REST de concessão de tokens separado para ser utilizado pela aplicação. Quando a aplicação solicita um token ao serviço de tokens do MSI, o serviço contacta o Azure Active Directory para obter um token para a identidade do MSI e devolve-o à aplicação para utilização no Key Vault. A parte mais importante deste fluxo de trabalho é a forma como a aplicação efetua a autenticação no serviço de tokens do MSI &mdash;. Em vez de exigir um segredo ou certificado que tem de gerir na sua configuração, a aplicação utiliza um segredo que o Azure injeta em segurança nas variáveis de ambiente durante o arranque. Não tem de gerir ou armazenar este valor do segredo em lado nenhum. Nada fora da aplicação pode aceder a este segredo ou ponto final do serviço de tokens do MSI.

O MSI também regista a aplicação no Azure Active Directory e eliminará o registo caso desative o MSI ou elimine a aplicação.

O MSI está disponível em todas as edições do Azure Active Directory, incluindo a edição Gratuita incluída numa subscrição do Azure. Utilizá-lo no Serviço de Aplicações não tem custos adicionais, não requer configurações e pode ser ativado ou desativado numa aplicação em qualquer altura.

> [!NOTE]
> O MSI não é atualmente suportado para aplicações Web do Linux ou do Contentor.

A ativação do MSI requer apenas um único comando da CLI do Azure sem qualquer configuração. Faremos isto na unidade 5 quando configurarmos uma aplicação do Serviço de Aplicações e a implementarmos no Azure. Antes disso, vamos aplicar os conhecimentos do MSI para escrever o código para a aplicação.