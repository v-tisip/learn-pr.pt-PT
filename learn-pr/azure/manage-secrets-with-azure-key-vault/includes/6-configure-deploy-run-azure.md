Agora está na altura de executar a nossa aplicação no Azure. Precisamos de criar uma aplicação do Serviço de Aplicações do Azure, configurá-la com um MSI e com a nossa configuração do cofre, e implementar o nosso código.

## <a name="exercise"></a>Exercício

### <a name="create-the-app-service-plan-and-app"></a>Criar a aplicação e o plano do Serviço de Aplicações

Criar uma aplicação do Serviço de Aplicações é um processo de dois passos: primeiro, crie o *plano*, depois a *aplicação*.

O nome do *plano* só precisa de ser exclusivo na sua subscrição, por isso pode utilizar o mesmo nome que utilizámos: **keyvault-exercise-plan**. No entanto, o nome da aplicação terá de ser globalmente exclusivo, por isso terá de escolher o seu.

No Azure Cloud Shell, execute o seguinte:

```azurecli
az appservice plan create --name keyvault-exercise-plan --resource-group keyvault-exercise-group
az webapp create --name <your-unique-app-name> --plan keyvault-exercise-plan --resource-group keyvault-exercise-group
```

### <a name="add-configuration-to-the-app"></a>Adicionar configuração à aplicação

Para implementar no Azure, vamos seguir a prática recomendada do Serviço de Aplicações de colocar a configuração nas Definições de Aplicações em vez de num ficheiro de configuração.

```azurecli
az webapp config appsettings set --name <your-unique-app-name> --resource-group keyvault-exercise-group --settings VaultName=<your-unique-vault-name>
```

### <a name="enable-msi"></a>Ativar MSI

Ativar o MSI numa aplicação é um processo simples:

```azurecli
az webapp identity assign --name <your-unique-app-name> --resource-group keyvault-exercise-group
```

No resultado JSON, copie o valor **principalId**. O PrincipalId é o ID exclusivo da nova identidade da aplicação no Azure Active Directory e vamos utilizá-lo no próximo passo.

### <a name="grant-access-to-the-vault"></a>Conceder acesso ao cofre

Agora, precisa de dar à sua aplicação permissões de identidade para obter e listar segredos do seu cofre de ambiente de produção. Utilize o valor **principalId** que copiou no passo anterior como o valor para **object-id** no comando abaixo.

```azurecli
az keyvault set-policy --name <your-unique-vault-name> --object-id <your-msi-principleid> --secret-permissions get list
```

### <a name="deploy-the-app-and-try-it-out"></a>Implementar e experimentar a aplicação

A sua configuração foi definida e está tudo pronto para implementar! Os comandos abaixo irão publicar o site na pasta `pub`, zipá-la para o ficheiro `site.zip` e implementar o zip no Serviço de Aplicações.

> [!NOTE]
> Terá de utilizar o comando `cd` para regressar ao diretório KeyVaultDemoApp, caso ainda não o tenha feito.

```console
dotnet publish -o pub
zip -j site.zip pub/*
az webapp deployment source config-zip --src site.zip --name <your-unique-app-name> --resource-group keyvault-exercise-group
```

Depois de obter um resultado que indique que o site foi implementado, abra `https://<your-unique-app-name>.azurewebsites.net/api/SecretTest` num browser. Deverá ver o valor de segredo, **reindeer_flotilla**.

A sua aplicação está concluída e implementada!