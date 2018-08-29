## <a name="module-summary"></a>Resumo do módulo
Neste módulo, utilizou os comandos da CLI do Azure para criar um grupo de recursos e implementar uma aplicação Web com um pequeno conjunto de comandos. Estes comandos podem ser combinados num script de shell como parte da solução de automatização.

A CLI do Azure é uma boa opção para todas as pessoas não familiarizadas com a linha de comandos e a criação de scripts do Azure. A sintaxe simples e a compatibilidade entre plataformas ajudam a reduzir o risco de erros ao executar tarefas repetitivas e regulares.

## <a name="cleanup"></a>Limpeza
A execução de aplicações Web tem um custo em relação à sua subscrição. Remova os recursos de que não precisa para evitar custos desnecessários. A forma mais fácil de limpar a sua subscrição do Azure é remover o grupo de recursos. Esta ação também eliminará todos os recursos no grupo. Quando tiver terminado este módulo, execute o seguinte cmdlet do Azure PowerShell:

    ```azurecli
    az group delete --resource-group popupResGroup
    ```

Quando lhe for pedido que confirme a eliminação, responda **Sim**. Este comando pode demorar vários minutos a concluir à medida que os recursos são eliminados. 