# Kubernetes

O Kubernetes, k8s (k + 8 caracteres + s, entendeu?) ou “kube” é uma plataforma open source que automatiza as operações dos containers Linux. 

Essa plataforma elimina grande parte dos processos manuais necessários para implantar e escalar as aplicações em containers. Em outras palavras, se você desejar agrupar em clusters os hosts executados nos containers Linux, o Kubernetes ajudará a gerenciar esses clusters com facilidade e eficiência.
 
Com a orquestração do Kubernetes, é possível criar serviços de aplicações que abrangem múltiplos containers, programar o uso deles no cluster, escalá-los e gerenciar a integridade deles com o passar do tempo.

O Kubernetes corrige vários problemas comuns que ocorrem com a proliferação de containers, organizando-os em "pods". 

Estes pods adicionam uma camada de abstração aos containers agrupados. Assim, é mais fácil programar as cargas de trabalho e fornecer os serviços necessários a esses containers, como rede e armazenamento. 

Outros componentes do Kubernetes são úteis no balanceamento de carga entre os pods. Com isso, é possível garantir que o número de containers em execução seja suficiente para oferecer suporte às cargas de trabalho.

# 1. O que o Kubernetes faz 

O Kubernetes possibilita:

* Orquestrar containers em vários hosts.
* Aproveitar melhor o hardware para maximizar os recursos necessários na execução das aplicações corporativas.
* Controlar e automatizar as implantações e atualizações de aplicações.
* Montar e adicionar armazenamento para executar aplicações com monitoração de estado.
* Escalar rapidamente as aplicações em containers e recursos relacionados.
* Gerenciar serviços de forma declarativa, garantindo que as aplicações sejam executadas sempre da mesma maneira como foram implantadas.
* Verificar a integridade e autorrecuperação das aplicações com posicionamento, reinício, replicação e escalonamento automáticos.

A tecnologia do docker ainda realiza as mesmas tarefas do seu objetivo original. 

1. O Kubernetes programa um pod para um nó, então o kubelet no nó instruirá o docker a iniciar os containers especificados. 
2. O kubelet, então, continuamente coleta do docker os status desses containers e agrega as informações no master. 3. O docker insere os containers nesse nó e os inicia e interrompe normalmente. 

A diferença é que um sistema automatizado solicita que o Docker realize essas tarefas em todos os nós de todos os containers, em vez do administrador fazer essas solicitações manualmente.

> Cluster: 

## 2. O que o Kubernetes NÃO faz

1. Não limita os tipos de aplicativos suportados. O Kubernetes tem como objetivo oferecer suporte a uma variedade extremamente diversificada de cargas de trabalho, incluindo cargas de trabalho sem estado, com estado e de processamento de dados. Se um aplicativo pode ser executado em um contêiner, ele deve funcionar muito bem no Kubernetes.
2. Não implanta código fonte e não cria seu aplicativo. Os fluxos de trabalho de integração, entrega e implantação contínuos (CI / CD) são determinados pelas culturas e preferências da organização, bem como pelos requisitos técnicos.
3. Não fornece serviços no nível do aplicativo, como middleware (por exemplo, barramentos de mensagens), estruturas de processamento de dados (por exemplo, Spark), bancos de dados (por exemplo, MySQL), caches ou sistemas de armazenamento em cluster (por exemplo, Ceph) como serviços internos. Esses componentes podem ser executados no Kubernetes e / ou podem ser acessados ​​por aplicativos executados no Kubernetes por meio de mecanismos portáteis, como o Open Service Broker .
4. Não determina soluções de log, monitoramento ou alerta. Ele fornece algumas integrações como prova de conceito e mecanismos para coletar e exportar métricas.
5. Não fornece nem exige um idioma / sistema de configuração (por exemplo, Jsonnet). Ele fornece uma API declarativa que pode ser direcionada por formas arbitrárias de especificações declarativas.
Não fornece nem adota nenhum sistema abrangente de configuração, manutenção, gerenciamento ou autocorreção da máquina.
6. Além disso, o Kubernetes não é um mero sistema de orquestração. De fato, elimina a necessidade de orquestração. A definição técnica de orquestração é a execução de um fluxo de trabalho definido: primeiro faça A, depois B e depois C. Por outro lado, o Kubernetes compreende um conjunto de processos de controle composíveis e independentes que conduzem continuamente o estado atual para o estado desejado fornecido. Não importa como você vai de A a C.

## 3. PODs

Os pods são usados como a unidade de replicação no Kubernetes. Se seu aplicativo se tornar muito popular e uma única instância de um pod não puder carregar, o Kubernetes poderá ser configurado para implantar novas réplicas de seu pod no cluster, conforme necessário. 

> Cluster (ou clustering) é o nome dado a um sistema que relaciona dois ou mais computadores para que estes trabalhem de maneira conjunta no intuito de processar uma tarefa. Estas máquinas dividem entre si as atividades de processamento e executam este trabalho de maneira simultânea.

Mesmo quando não está sob carga pesada, é padrão ter várias cópias de um pod em execução a qualquer momento em um sistema de produção para permitir o balanceamento de carga e a resistência a falhas.

Os pods podem conter vários containers, mas você deve se limitar quando possível. 

Como os pods são dimensionados para cima e para baixo como uma unidade, todos os containers de um pod devem ser dimensionados juntos, independentemente de suas necessidades individuais. 

Isso leva a recursos desperdiçados e uma conta cara. 

Para resolver isso, os pods devem permanecer o menor possível, geralmente contendo apenas um processo principal e seus containers auxiliares fortemente acoplados (esses containers auxiliares são geralmente chamados de “carros laterais”).
