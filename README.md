# Cases para Comitê de Calibração

## Salvamentos de Contatos Pix de Forma Assíncrona

### Situação (Situation)
O fluxo de salvamento de contatos Pix apresentava alta latência, impactando negativamente a eficiência do sistema. Era necessário implementar uma solução que permitisse o salvamento de contatos de forma mais rápida e eficiente, sem bloquear outras operações do sistema.

### Tarefa (Task)
Minha responsabilidade era implementar um mecanismo assíncrono para o salvamento de contatos Pix, garantindo que o sistema pudesse continuar executando outras tarefas enquanto o salvamento ocorresse em segundo plano. Além disso, era necessário assegurar a robustez e segurança na comunicação entre serviços.

### Ação (Action)
Para realizar essa tarefa, tomei as seguintes ações:
- Padronizei e otimizei o processo de salvamento de contatos.
- Implementei um mecanismo assíncrono utilizando eventos SQS para postar os dados dos contatos Pix em uma fila.
- Atualizei as dependências do projeto, incluindo as versões do SpringBoot e do framework QuickCloud do Itaú.
- Atualizei a versão da JDK para Java 17, permitindo o uso de módulos do QuickCloud, como a comunicação entre serviços de mensageria SQS.
- Garanti que o mecanismo assíncrono fosse capaz de lidar com falhas de comunicação e assegurar a entrega dos dados de forma confiável.

### Resultado (Result)
Como resultado dessas ações, houve uma significativa redução na latência do fluxo de salvamento de contatos Pix. A implementação assíncrona aumentou a eficiência geral do sistema, permitindo que ele executasse outras tarefas enquanto o salvamento ocorria em segundo plano. Além disso, o aprendizado obtido incluiu:
- A importância de utilizar mecanismos assíncronos para melhorar a performance.
- A necessidade de garantir robustez e segurança na comunicação entre serviços.
- Saimos de uma media latencia de 7.74 s do efetiva para 5.09 segundos, o que representa uma redução de 34% na latência do fluxo de salvamento de contatos Pix.

---

## Perguntas e Respostas Técnicas

**Pergunta:** Qual foi o problema identificado no fluxo de salvamento de contatos Pix e como ele impactava o sistema?  
**Resposta:** O problema identificado foi a alta latência no fluxo de salvamento de contatos Pix, que impactava negativamente a eficiência do sistema ao bloquear outras operações. Isso tornava o sistema menos responsivo e dificultava a execução de tarefas simultâneas.

---

**Pergunta:** Qual foi a solução implementada para resolver o problema de latência no salvamento de contatos Pix?  
**Resposta:** A solução foi implementar um mecanismo assíncrono utilizando eventos SQS para postar os dados dos contatos Pix em uma fila. Isso permitiu que o salvamento ocorresse em segundo plano, sem bloquear outras operações do sistema.

---

**Pergunta:** Por que foi necessário atualizar as dependências do projeto e a versão da JDK?  
**Resposta:** A atualização das dependências do projeto e da JDK para a versão 17 foi necessária para utilizar módulos do framework QuickCloud, como a comunicação entre serviços de mensageria SQS. Isso garantiu compatibilidade e aproveitamento de recursos mais modernos.

---

**Pergunta:** Como foi garantida a robustez e segurança na comunicação entre serviços durante o salvamento assíncrono?  
**Resposta:** A robustez e segurança foram garantidas por meio de mecanismos de tratamento de falhas na comunicação, assegurando a entrega confiável dos dados na fila SQS. Isso incluiu retries automáticos e monitoramento de mensagens.

---

**Pergunta:** Quais foram os principais benefícios obtidos com a implementação do mecanismo assíncrono?  
**Resposta:** Os principais benefícios foram a redução significativa na latência do fluxo de salvamento de contatos Pix, aumento da eficiência geral do sistema e a possibilidade de executar outras tarefas enquanto o salvamento ocorria em segundo plano.

---

**Pergunta:** Quais aprendizados técnicos você obteve ao implementar essa solução?  
**Resposta:** Os aprendizados incluíram a importância de utilizar mecanismos assíncronos para melhorar a performance e a necessidade de garantir robustez e segurança na comunicação entre serviços.

---

**Pergunta:** Como o uso de SQS contribuiu para a solução do problema?  
**Resposta:** O uso de SQS permitiu o desacoplamento do processo de salvamento de contatos Pix, garantindo que os dados fossem armazenados em uma fila para processamento assíncrono. Isso reduziu a latência e aumentou a eficiência do sistema.

---

**Pergunta:** Quais cuidados foram tomados para lidar com falhas na comunicação entre serviços?  
**Resposta:** Foram implementados mecanismos de retries automáticos e monitoramento de mensagens para lidar com falhas na comunicação, garantindo que os dados fossem entregues de forma confiável.

---

**Pergunta:** Por que a escolha de Java 17 foi relevante para essa implementação?  
**Resposta:** A escolha de Java 17 foi relevante porque permitiu o uso de recursos modernos e compatibilidade com os módulos do framework QuickCloud, essenciais para a comunicação entre serviços de mensageria SQS.

---

**Pergunta:** Como você validou que a solução implementada atendia aos requisitos de eficiência e robustez?  
**Resposta:** A validação foi feita por meio de testes de performance e monitoramento do fluxo de salvamento, garantindo que a latência fosse reduzida e que o sistema continuasse executando outras tarefas sem interrupções.


**Pergunta:** Por que foi escolhido o serviço AWS SQS em vez de utilizar o Kafka?
**Resposta:** A escolha do AWS SQS em vez do Kafka foi baseada na simplicidade de integração com o ecossistema AWS, na facilidade de uso e na robustez do serviço para cenários de mensagens assíncronas. O SQS oferece uma solução gerenciada que reduz a complexidade operacional, permitindo foco no desenvolvimento de funcionalidades em vez de gerenciar a infraestrutura de mensageria.


## Arquitetura de eventos

A arquitetura de mensageria é um padrão de design usado para comunicação assíncrona entre sistemas ou componentes de software. Ela utiliza mensagens para transmitir dados ou eventos entre produtores e consumidores, permitindo o desacoplamento e maior escalabilidade. Os principais elementos dessa arquitetura incluem:

    Produtor (Producer): Responsável por enviar mensagens para o sistema de mensageria.

    Consumidor (Consumer): Recebe e processa as mensagens enviadas pelo produtor.

    Broker de Mensagens: Um intermediário que gerencia o envio, roteamento e armazenamento das mensagens. Exemplos incluem AWS SQS, Apache Kafka e RabbitMQ.

    Filas (Queues): Estruturas onde as mensagens são armazenadas até serem consumidas.

    Tópicos (Topics): Usados em sistemas de publicação/assinatura (pub/sub), onde múltiplos consumidores podem receber mensagens de um único produtor.

    Mensagens: Dados ou eventos transmitidos entre os componentes.

### Vantagens da Arquitetura de Mensageria
- **Desacoplamento**: Permite que os produtores e consumidores operem de forma independente, facilitando a manutenção e evolução dos sistemas.
- **Escalabilidade**: Suporta alta carga de mensagens e múltiplos consumidores, permitindo que o sistema cresça conforme necessário.
- **Resiliência**: Garante entrega confiável de mensagens, mesmo em caso de falhas temporárias, através de mecanismos como retries e persistência de mensagens.
- **Flexibilidade**: Facilita a integração de novos serviços e componentes, permitindo que diferentes partes do sistema se comuniquem de forma eficiente.
- **Assíncrono**: Permite que as operações sejam executadas em segundo plano, melhorando a performance e a responsividade do sistema.

### exemplo de uso: A arquitetura de mensageria é amplamente utilizada em sistemas distribuídos, microserviços e aplicações em nuvem, onde a comunicação assíncrona é essencial para garantir eficiência e escalabilidade. Um exemplo prático é o uso do AWS SQS para gerenciar filas de tarefas em uma aplicação web, onde as requisições dos usuários são processadas de forma assíncrona, melhorando a experiência do usuário e a performance do sistema.

### Desvantagens da Arquitetura de Mensageria
- **Complexidade**: A introdução de um sistema de mensageria pode aumentar a complexidade do sistema, exigindo mais configuração e monitoramento.