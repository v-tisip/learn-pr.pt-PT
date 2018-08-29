Assim que tivermos uma referência para um blob, podemos carregar e transferir dados. Os objetos `ICloudBlob` têm métodos `Upload` e `Download` que oferecem suporte a matrizes de bytes, fluxos e arquivos como origens e destinos. Os tipos específicos têm métodos adicionais para a sua conveniência &mdash; por exemplo, `CloudBlockBlob` suporta o carregamento e a transferência de cadeias de caracteres com `UploadTextAsync` e `DownloadTextAsync`.

## <a name="creating-new-blobs"></a>Criar novos blobs

Para criar um blob novo, chama um dos métodos `Upload` num blob que não existe. Isso faz duas coisas: cria o blob e carrega os dados. 

## <a name="moving-data-to-and-from-blobs"></a>Mover dados de e para blobs

Mover dados de e para um blob é uma operação de rede que demora algum tempo. No SDK de Armazenamento do Azure para .NET Core, todos os métodos que requeiram a atividade de rede devolvem `Task`s, portanto, certifique-se de que os seus métodos do controlador estão `async` conforme adequado e que está a `await` chamadas de método e não a `Wait` nas mesmas.

Uma recomendação comum ao trabalhar com objetos de dados de grandes dimensões é utilizar fluxos em vez de estruturas na memória, como matrizes de bytes ou cadeias de carateres. Isso evita a colocação em memória intermédia do conteúdo completo na memória antes de o enviar para o destino. O ASP.NET Core suporta a leitura e gravação de fluxos de solicitações e de respostas.

## <a name="concurrent-access"></a>Acesso simultâneo

É possível que os outros processos podem adicionar, alterar ou eliminar blobs à medida que a nossa aplicação as utiliza. Programe de forma defensiva e pense nos problemas potencialmente causados pela simultaneidade, como blobs eliminados logo a seguir a tentar transferi-los ou blobs cujos conteúdos mudam quando não espera. Veja a secção de Recursos Adicionais no fim deste módulo para mais informações sobre as AccessConditions e concessões de blobs para gerir o acesso simultâneo de blobs.

## <a name="exercise"></a>Exercício

Vamos terminar a nossa aplicação ao adicionar código de carregamento e transferência e, então, implementar no Serviço de Aplicações do Azure para efeitos de teste.

### <a name="upload"></a>Carregar

Para carregar um blob, vamos implementar o método `BlobStorage.Save` ao utilizar `GetBlockBlobReference` para obter `CloudBlockBlob` do contentor. `FilesController.Upload` passa a transmissão de ficheiros para `Save`, para podermos utilizar `UploadFromStreamAsync` para realizar o carregamento e maximizar a eficiência.

Abra o `BlobStorage.cs` no editor e preencha `Save` na implementação com o seguinte código:

```csharp
public Task Save(Stream fileStream, string name)
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    CloudBlockBlob blockBlob = container.GetBlockBlobReference(name);
    return blockBlob.UploadFromStreamAsync(fileStream);
}
```

> [!NOTE]
> O código de carregamento com base na transmissão que aparece aqui é mais eficiente que ler o ficheiro numa matriz de bytes antes de enviar para o armazenamento de Blobs do Azure. No entanto, a técnica `IFormFile` que utilizamos para obter o ficheiro do cliente não é uma implementação de transmissão verdadeira de ponta a ponta, sendo apenas adequada para processar carregamentos de ficheiros pequenos. Veja a secção Recursos Adicionais no final deste módulo para obter informações sobre regras o carregamento de ficheiros completamente transmitidos.

### <a name="download"></a>Transferência

`BlobStorage.Load` devolve um `Stream`, que significa que o nosso código não precisa de mover fisicamente os bytes de armazenamento dos Blobs em todos os &mdash;, apenas precisamos de devolver uma referência ao fluxo de blobs. Pode fazê-lo com `OpenReadAsync`. O ASP.NET Core vai processar a leitura e fechar o fluxo quando ele cria a resposta do cliente.

Preencha `Load` com este código:

```csharp
public Task<Stream> Load(string name)
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    return container.GetBlobReference(name).OpenReadAsync();
}
```

### <a name="deploy-and-run-in-azure"></a>Publicar e executar no Azure

A nossa aplicação está terminada &mdash; vamos implementá-la e ver como funciona. Execute o seguinte código no terminal do Azure Cloud Shell para criar o nosso código e implementá-lo numa nova instância do Serviço de Aplicações. Também podemos adicionar a nossa cadeia de ligação de conta de armazenamento para configuração.

```console

```

...

Carregue e transfira alguns dos ficheiros para testar a aplicação, então execute o seguinte no shell para ver os blobs que foram carregados:

```console

```

**Imagem LISTA DE TAREFAS do portal**