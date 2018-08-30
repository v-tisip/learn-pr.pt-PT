O Azure Key Vault é um *arquivo de segredos*: um serviço cloud centralizado para armazenar os segredos da aplicação. O Key Vault ajuda a impedir os cenários acima ao manter os segredos da aplicação numa única localização central e ao fornecer acesso seguro, controlo de permissões e registo de acesso.

Um cofre individual é um recurso do Azure com a sua própria configuração e política de segurança, que pode ser criado com qualquer uma das ferramentas de gestão padrão do Azure, como o portal do Azure ou a CLI do Azure. A gestão do cofre e do acesso secreto é realizada por meio de uma API REST. Cada cofre tem um URL exclusivo onde está alojada a API.

> [!IMPORTANT]
> **O Key Vault foi concebido para armazenar os segredos de configuração das aplicações de servidor.** Não é adequado para armazenar dados pertencentes aos utilizadores da sua aplicação e não deve ser usado no lado do cliente de uma aplicação. Tal reflete-se nas suas características de desempenho, na API e no modelo de custos.
>
> Os dados de utilizador devem ser armazenados noutro local, por exemplo, numa base de dados SQL do Azure com Encriptação de Dados Transparente ou numa conta de armazenamento com Encriptação do Serviço de Armazenamento. Os segredos utilizados pela aplicação para aceder a esses arquivos de dados podem ser mantidos no Key Vault.

## <a name="what-is-a-secret-in-key-vault"></a>O que é um segredo no Key Vault?

No Key Vault, um segredo é um par nome/valor de cadeias de caracteres. Os nomes secretos têm de ter entre 1 e 127 carateres, conter apenas carateres alfanuméricos e travessões e serem exclusivos no interior do cofre. Um valor secreto pode ser qualquer cadeia de caracteres UTF-8 com um tamanho máximo de 25 KB.

> [!TIP]
> Os nomes secretos não precisam de ser considerados especialmente secretos em si mesmos. Poderá armazená-los na configuração da aplicação se a sua implementação assim o exigir. O mesmo também é válido para os nomes de cofre e os URLs.

> [!NOTE]
> O Key Vault suporta dois tipos adicionais de segredos além das cadeias de caracteres &mdash; *chaves* e *certificados* &mdash; e fornece uma funcionalidade útil específica para os respetivos casos de utilização. Este módulo não aborda esses recursos e concentra-se nas cadeias de segredos como as palavras-passe e as cadeias de ligação.
