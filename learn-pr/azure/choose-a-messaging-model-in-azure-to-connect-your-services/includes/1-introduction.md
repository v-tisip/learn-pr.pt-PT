Muitas aplicações são compostas por programas que são executados em vários computadores ou dispositivos diferentes. Nestas aplicações distribuídas, têm de ser enviadas mensagens entre os componentes em várias redes e longas distâncias. Até no mesmo servidor ou no mesmo centro de dados, arquiteturas relativamente acopladas exigem mecanismos para comunicação entre os componentes. Um sistema de mensagens fiável é, muitas vezes, um problema crítico.

Suponha que trabalha numa empresa de software que desenvolve uma aplicação de partilha de música. Os músicos podem carregar a música que criam na sua plataforma através de uma aplicação Web front-end ou móvel. Podem ouvir e comentar o trabalho dos outros membros. A aplicação consiste num site que é executado no seu ISP, uma aplicação móvel que é executada nos dispositivos móveis dos utilizadores, uma API Web que é executada no Azure e uma Base de Dados SQL do Azure onde os dados são armazenados.

Já observou que, em alturas de procura elevada, alguns ficheiros de música não são carregados com êxito e alguns comentários não são publicados. O teste mostra que estes problemas são causados por mensagens ignoradas entre componentes front-end e a API Web. Procura resolver estes problemas ao utilizar uma ou mais das seguintes tecnologias do Azure: Filas de Armazenamento, Hubs de Eventos, Grelhas de Eventos e Bus de Serviço.

Aqui, aprenderá a escolher a tecnologia de mensagens certa no Azure para cada tarefa de comunicação numa aplicação distribuída.

## <a name="learning-objectives"></a>Objetivos de Aprendizagem

- Descreva os eventos e mensagens, e os desafios em que pode utilizá-los para resolver problemas numa aplicação distribuída.
- Identifique os cenários nos quais uma Fila de Armazenamento do Azure é a melhor tecnologia de mensagens para uma aplicação.
- Identifique os cenários nos quais uma Grelha de Eventos do Azure é a melhor tecnologia de mensagens para uma aplicação.
- Identifique os cenários nos quais um Hub de Eventos do Azure é a melhor tecnologia de mensagens para uma aplicação.
- Identifique os cenários nos quais um Bus de Serviço do Azure é a melhor tecnologia de mensagens para uma aplicação.
