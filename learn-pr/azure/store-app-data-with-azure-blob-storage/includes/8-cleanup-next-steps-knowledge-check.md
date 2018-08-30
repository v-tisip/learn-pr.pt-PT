Neste módulo, aprendeu como utilizar o Armazenamento de blobs do Azure para armazenar dados da aplicação Web. Apresentámos sugestões para criar uma estratégia para utilizar o Armazenamento de blobs numa aplicação Web e como utilizar o SDK do Armazenamento do Azure para .NET Core para gravar e ler a partir de blobs. A aplicação criada aceita os ficheiros carregados pelos utilizadores, armazena-os no Armazenamento de blobs e disponibiliza-os para transferência.

## <a name="cleanup"></a>Limpeza

Para limpar a subscrição do Azure, execute o seguinte no Azure Cloud Shell para eliminar o grupo de recursos que contém todos os recursos criados neste módulo.

```console
az group delete --name blob-exercise-group
```

Para limpar o armazenamento do Cloud Shell, elimine o diretório `TODO` com `rm -rf TODO`.

## <a name="additional-resources"></a>Recursos adicionais

**Ligações cross-docset TODO?**

* **Armazenar as chaves da conta de armazenamento de forma segura**: o Azure Key Vault é a solução ponto a ponto mais robusta para armazenar os valores de configuração secretos. Veja [aqui](https://docs.microsoft.com/aspnet/core/security/key-vault-configuration?view=aspnetcore-2.1&tabs=aspnetcore2x) para obter informações sobre como utilizar o Key Vault numa aplicação ASP.NET Core. Em alternativa, pode armazenar com segurança cadeias de ligação nas definições de aplicação do Serviço de Aplicações e utilizar a [ferramenta Secret Manager do ASP.NET Core](https://docs.microsoft.com/aspnet/core/security/app-secrets?view=aspnetcore-2.1&tabs=windows) para suportar ambientes de programação.
* [Carregar ficheiros grandes com transmissão em fluxo no ASP.NET Core](https://docs.microsoft.com/aspnet/core/mvc/models/file-uploads?view=aspnetcore-2.1#uploading-large-files-with-streaming)
* [Simultaneidade de blobs: AccessConditions e concessões de blobs](https://azure.microsoft.com/blog/managing-concurrency-in-microsoft-azure-storage-2/)
* [Conceder acesso limitado ao objeto do Armazenamento do Azure com assinaturas de acesso partilhado](https://docs.microsoft.com/azure/storage/common/storage-dotnet-shared-access-signature-part-1)
* [Indexar o Armazenamento de blobs com o Azure Search](https://docs.microsoft.com/azure/search/search-howto-indexing-azure-blob-storage)
* [Restrições de nome de contentor e de blob](https://docs.microsoft.com/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata#resource-names)