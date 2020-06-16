# Gerenciamento de processos

O sistema operacional multitarefa é preparado para dar ao usuário a ilusão que o número de processos em execução 
simultânea no computador é maior que o número de processadores instalados. 

Cada processo recebe uma fatia do tempo e a alternância entre vários processos é tão rápida que o usuário pensa 
que sua execução é simultânea.

São utilizados algoritmos de escalonamento para determinar qual processo será executado em determinado momento e por 
quanto tempo.

Os processos podem comunicar-se, isto é conhecido como IPC (Inter-Process Communication). 

Os mecanismos geralmente utilizados são:

- pipes;
- named pipes;
- memória compartilhada;
- soquetes (sockets);
- trocas de mensagens.

O sistema operacional, normalmente, deve possibilitar o multiprocessamento (SMP ou NUMA). Neste caso, processos diferentes e threads podem ser executados em diferentes processadores. 

Para essa tarefa, ele deve ser reentrante e interrompível, o que significa que pode ser interrompido no meio da 
execução de uma tarefa.

## Pipes (Comunicação entre processos)

Em geral,pipes são empregados para estabelecer comunicação entre processos pai e filho. Um pipe é um canal unidirecional de comunicação, isto é, a informação flui em uma única direção. 

Para estabelecer-se comunicação bidirecional, são necessários dois pipes.

Uma vez estabelecido o pipe entre os processos, um deles pode enviar “mensagens” (qualquer sequência de bytes) para o outro. 

O envio e recebimento destas “mensagens” é feito com os serviços normais de leitura e escrita em ficheiros - read() e write().

![Pipe](http://www.it.uu.se/education/course/homepage/os/vt18/images/module-2/parent-children-pipe.png)
