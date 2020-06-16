# Gerenciamento de memória

O sistema operacional tem acesso completo à memória do sistema e deve permitir que os processos dos usuários 
tenham acesso seguro à memória quando o requisitam.

Em sua forma mais simples, está relacionado em duas tarefas essenciais:

- Alocação: Quando o programa requisita um bloco de memória, o gerenciador o disponibiliza para a alocação;
- Reciclagem: Quando um bloco de memória foi alocado, mas os dados não foram requisitados por um determinado número de ciclos ou não há nenhum tipo de referência a este bloco pelo programa, esse bloco é liberado e pode ser reutilizado para outra requisição.

Todo programa precisa utilizar memória para ser executado. Quando um programa inicia sua execução, ele começa a solicitar memória ao sistema operacional, ou seja, faz a alocação de memória necessária para a sua execução. 


## 1. Alocação de memória

A alocação de memória está dividida em 3(três) partes: Alocação estática, dinâmica e local. 

### 1.1. Alocação Estática 

Os dados tem um tamanho fixo e estão organizados sequencialmente na memória do computador. Um exemplo típico de alocação estática são as **variáveis globais e arrays**. 

A alocação estática de memória tem como principal ponto positivo a simplicidade com que pode ser realizada pelos programadores, mantendo o algoritmo simples e de fácil organização das variáveis utilizadas. 

No entanto, como principal ponto negativo, a alocação estática **ocupa uma porção fixa da memória**, em casos em que essas variáveis não sejam utilizadas após um certo ponto, a alocação estática consome desnecessariamente esta porção reservada da memória, podendo levar o programa a fica muito pesado desnecessariamente. 

Apesar disso, é importante ressaltar, que na maioria das linguagens de programação, as variáveis criadas com alocação estática são liberadas automaticamente após o fim de uma determinada função.

### 1.2. Alocação Dinâmica

Com a alocação estática tínhamos que declarar todas as variáveis que íamos usar no programa, para que o computador pudesse alocar memória para elas. 

A questão então era: há um modo de eu criar uma variável, ou seja, definí-la, enquanto o programa roda (sem ter que tê-la incluido no código)? 

Não há como declarar a variável enquanto o programa roda, porém dá para alocar memória para uma variável enquanto o programa roda.

E qual a vantagem disso? Poupa memória. Porém isso vem com um preço (como tudo na computação) - gasta mais processamento.

### 1.3. Alocação Local

Este processo de alocação é usado para variáveis que são locais a funções e sub-rotinas. Isso significa que o processo em execução deve manter acessível as variáveis locais da função ou procedimento que está executando no momento. 

Além disso, pelas propriedades do escopo em blocos, também devem estar acessíveis as variáveis de blocos mais externos. Em linguagens que permitem a definição de funções aninhadas, ter acesso a variáveis de quaisquer funções definidas externamente à função atualmente em execução. 

Como uma função pode chamar outras funções, um número arbitrário de funções pode estar no meio de sua execução em um determinado momento, mesmo que apenas uma esteja realmente sendo executada, isso indica que o contexto de várias funções deve ser mantido enquanto as mesmas não concluíram sua execução. 

## 2. Swapping

Dentro de gerenciamento de memória, pode não ser possível manter todos os processos em memória, muitas vezes 
por não existir memória suficiente para alocar aquele processo. 

Para solucionar esse problema existe um mecanismo chamado swapping, onde a gerência de memória reserva uma área 
do disco para o seu uso em determinadas situações, e um processo é completamente copiado da memória para o disco.  

Este processo é retirado da fila do processador e mais tarde será novamente copiado para a memória; 

Então, o processo ficará ativo na fila novamente. O resultado desse revezamento no disco é que o sistema 
operacional consegue executar mais processos do que caberia em um mesmo instante na memória. 

Swapping impõe aos programas um grande custo em termos de tempo de execução, pois é necessário copiar 
todo o processo para o disco e mais tarde copiar novamente todo o processo para a memória. 

Em sistemas onde o usuário interage com o programa durante sua execução, o mecanismo de swapping 
é utilizado em último caso, quando não se é possível manter todos os processos na memória, visto que a queda 
no desempenho do sistema é imediatamente sentida pelo usuário.

