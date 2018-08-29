Neste módulo, protegeu a configuração secreta de uma aplicação no Azure Key Vault. O nosso código de aplicação faz a autenticação no cofre com a Identidade do Serviço Gerido e carrega automaticamente os segredos do cofre para o sistema de configuração do ASP.NET Core no arranque.

## <a name="cleanup"></a>Limpeza

Para limpar a sua subscrição do Azure, execute o seguinte no Azure Cloud Shell para eliminar o grupo de recursos que contém todos os recursos criados neste módulo.

```console
az group delete --name keyvault-exercise-group
```

Para limpar o armazenamento do Cloud Shell, elimine o diretório `KeyVaultDemoApp`.

## <a name="next-steps"></a>Passos seguintes

Caso se tratasse de uma aplicação real, o que se seguiria?

* Guarde todos os segredos da sua aplicação nos cofres! Já não se justifica tê-los em ficheiros de configuração.
* Continue a desenvolver a aplicação. O seu ambiente de produção está totalmente configurado, por isso não precisa de repetir todo o processo de configuração em futuras implementações.
* Para suportar o desenvolvimento, crie um cofre de ambiente de desenvolvimento que contenha segredos com os mesmos nomes mas com valores diferentes. Conceda permissões à equipa de desenvolvimento e configure o nome do cofre no ficheiro de configuração do ambiente de desenvolvimento da aplicação. Quando os programadores executam a aplicação localmente, `AddAzureKeyVault` deteta automaticamente instalações locais do Visual Studio e a CLI do Azure, bem como utiliza as credenciais do Azure configuradas nessas aplicações para iniciar sessão e aceder ao cofre.
* Crie outros ambientes para, por exemplo, testar a aceitação do utilizador.
* Separe cofres em diferentes subscrições e/ou grupos de recursos para os isolar.
* Autorize as pessoas certas a aceder a outros cofres de ambiente.

## <a name="further-reading"></a>Leitura adicional

* [Documentação do Key Vault](https://docs.microsoft.com/azure/key-vault/)
* [Mais informações sobre AddAzureKeyVault e respetivas opções avançadas](https://docs.microsoft.com/aspnet/core/security/key-vault-configuration?view=aspnetcore-2.1&tabs=aspnetcore2x)
* [Este tutorial](https://docs.microsoft.com/azure/key-vault/key-vault-use-from-web-application) explica como utilizar `KeyVaultClient`, incluindo a sua autenticação manual no Azure Active Directory com um segredo do cliente em vez de um MSI.
* [Documentação do serviço de token de MSI](https://docs.microsoft.com/azure/app-service/app-service-managed-service-identity#using-the-rest-protocol) para implementar o fluxo de trabalho de autenticação de forma autónoma