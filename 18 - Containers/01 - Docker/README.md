# Docker

O Docker foi projetado para garantir que o ambiente no qual os desenvolvedores escrevem o código corresponda aos ambientes em que seus aplicativos são implantados.

É uma alternativa da virtualização quando o kernel da máquina host é compartilhado com a máquina virtualizada ou software em operação. 

A criação de contêineres independentes para executar dentro de uma única instância do sistema operacional, evita a sobrecarga de manter máquinas virtuais.

O docker é uma ferramenta que pode empacotar um aplicativo e suas dependências em um recipiente virtual que pode ser executado em qualquer servidor Linux. Isso ajuda a permitir flexibilidade e portabilidade de onde o aplicativo pode ser executado, quer nas instalações, nuvem pública, nuvem privada, entre outros.

## Principais conceitos

|Conceito| Descrição |
|--|--|
| Master |a máquina que controla os nós do Kubernetes. É nela que todas as atribuições de tarefas se originam.  |
|Nó|são máquinas que realizam as tarefas solicitadas e atribuídas. A máquina mestre do Kubernetes controla os nós.
|Pod| Grupo de um ou mais containers implantados em um único nó. Todos os containers em um pod compartilham o mesmo endereço IP, IPC, nome do host e outros recursos. Os pods separam a rede e o armazenamento do container subjacente. Isso facilita a movimentação dos containers pelo cluster.
|Controlador de replicações |controla quantas cópias idênticas de um pod devem ser executadas em um determinado local do cluster.
|Serviço| desacopla as definições de trabalho dos pods. Os proxies de serviço do Kubernetes automaticamente levam as solicitações de serviço para o pod correto, independentemente do local do pod no cluster ou se foi substituído.
|Kubelet|um serviço executado nos nós que lê os manifestos do container e garante que os containers definidos foram iniciados e estão em execução.
|kubectl|a ferramenta de configuração da linha de comando do Kubernetes.

## Dockerfile

Este documento é a principal ferramenta para buildar um container docker, inserindo uma sequência de comandos para que o container rode com sucesso. 

## Docker-compose

Caso você deseje subir um container e haja a interligação entre um ou mais contianers, o ideal é que seja utilizado o Docker-compose
