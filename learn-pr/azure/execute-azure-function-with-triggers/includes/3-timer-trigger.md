É comum executar uma parte lógica num intervalo definido. Imagine que tem um blogue e nota que os seus subscritores não estão a ler as publicações mais recentes. Decide que a melhor ação é enviar um e-mail uma vez por semana para lembrá-los de irem ao seu blogue. Implemente esta lógica com uma função do Azure com um acionador de temporizador para invocar a função semanalmente.

Aqui, irá aprender a criar um acionador de temporizador e instruir o acionador para ser executado num intervalo consistente.

## <a name="what-is-a-timer-trigger"></a>O que é um acionador de temporizador?

Um acionador de temporizador é um acionador que executa uma função num intervalo consistente. Para criar um acionador de temporizador, terá de conceder dois conjuntos de informações. O primeiro requisito é um *Nome do parâmetro do carimbo de data/hora*, que é simplesmente um identificador para aceder ao acionador no código. O segundo requisito é uma *Agenda*, que é uma *expressão CRON* que define o intervalo para o temporizador.

## <a name="what-is-a-cron-expression"></a>O que é uma expressão CRON?

Uma *expressão CRON* é uma cadeia de carateres que consiste em seis campos que representam um conjunto de horas.

A ordem dos seis campos no Azure é: {segundo} {minuto} {hora} {dia} {mês} {dia da semana}.

Por exemplo, uma *expressão CRON* para criar um acionador que é executado a cada cinco minutos é semelhante a:

```
0 */5 * * * *
```

Em primeiro lugar, esta cadeia de carateres pode parecer confusa. Vamos voltar atrás e dividir estes conceitos quando tivermos uma análise mais profunda sobre as *expressões CRON*.

Para criar uma *expressão CRON*, tem de ter um entendimento básico de alguns dos carateres especiais.

| Caráter especial | Significado | Exemplo |
| ------------- | ------------- | ------------- |
| *      | Seleciona todos os valores num campo | Um asterisco "*" no campo do dia da semana significa *todos os* dias. |
| ,      | Separa os itens numa lista | Uma vírgula "1,3" no campo do dia da semana significa apenas Segundas-feiras (dia 1) e Quartas-feiras (dia 3). |
| -      | Especifica um intervalo | Um hífen "10-12" no campo de hora significa um intervalo que inclui as horas 10, 11 e 12. |
| /      | Especifica um incremento | Uma barra "*/10" no campo dos minutos significa um incremento de cada 10 minutos. |

Agora iremos voltar para o exemplo de expressão CRON original. Vamos tentar compreender melhor ao segmentar campo por campo.

```
0 */5 * * * *
```

O **primeiro campo** representa segundos. Este campo suporta os valores 0-59. Como o campo contém um zero, seleciona o primeiro valor possível, que é um segundo.

O **segundo campo** representa minutos. O valor "*/5" contém dois carateres especiais. Primeiro, o asterisco (*) significa "selecione cada valor dentro do campo." Uma vez que este campo representa minutos, os valores possíveis são 0-59. O segundo caráter especial é a barra (/), que representa um incremento. Quando combina estes carateres em conjunto, significa que para todos os valores 0-59, selecione cada quinto valor. Uma forma mais fácil de dizer que é simplesmente "a cada cinco minutos."

Os **quatro campos restantes** representam a hora, o dia, o mês e o dia da semana. Um asterisco para estes campos significa para selecionar todos os valores possíveis. Neste exemplo, selecionamos "cada hora de cada dia do mês."

Quando colocar todos os campos em conjunto, a expressão é lida como "no primeiro segundo, de cada quinto minuto de cada hora, de cada dia, de cada mês".

## <a name="how-to-create-a-timer-trigger"></a>Como criar um acionador de temporizador

Um acionador de temporizador pode ser criado completamente no portal do Azure. Na sua função do Azure, selecione **acionador de temporizador** na lista de tipos de acionadores predefinidos. Introduza a lógica que pretende executar. Indique um **Nome do parâmetro do carimbo de data/hora** e a **expressão CRON**.

## <a name="summary"></a>Resumo

Um acionador de temporizador invoca uma função do Azure com base numa agenda consistente. Para definir a agenda para um acionador de temporizador, criamos uma *expressão CRON*, que é uma cadeia de carateres que representa um conjunto de horas.

