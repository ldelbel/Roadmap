# List: 

Também chamada de seqüência. É uma coleção ordenada, que ao contrário da inferface Set, pode conter valores duplicados.

* Ao contrário de Set, as classes que implementam List possui o método get(int index). 
* É possível repurar os elementos da coleção utilizando seu índice. 

| Implementação | Característica  | 
|--|--|
| ArrayList | possui melhor agilidade na inserção e armazenamento de dados.  |
|LinkedList| possui agilidade na remoção e manipulação de dados.  |

## 1. ArrayList

Este tipo de lista é implementado como um Array que é dimensionado dinamicamente, ou seja, sempre que é necessário o seu tamanho aumenta em 50% do tamanho da lista, significa que se você tiver uma lista de tamanho igual a 10 e ela “encher”, seu tamanho aumentará para 15 automaticamente.

Além disso a ArrayList permite que elementos sejam acessados diretamente pelos métodos get() e set(), e adicionados através de add() e remove().

Todo ArrayList começa com um tamanho fixo, que vai aumentando conforme necessário, mas o custo deste aumento é alto, pois é feita uma cópia do array atual para um novo array com um novo tamanho, então imagine um array com 10mil elementos que será copiado para um novo array para criação de mais 5 mil elementos ? 

De fato é um alto custo. Então é altamente aconselhável que você já inicie seu Array com uma quantidade de elementos que atenda ao seu objetivo atual, sem a necessidade de criação dinâmica de novos espaços, ou seja, se você souber que terá que armazenar de 300 a 400 objetos em um Array, defina 500, pois é melhor sobrar espaço do que utilizar recurso do processador sem necessidade.

## 2. LinkedList

A sua principal diferença entre o ArrayList é na performance entre os métodos add, remove, get e set.

Perceba então que a principal diferença está na performance, e uma análise minuciosa deve ser feita em casos onde a performance é algo crítica e todos o pontos devem ser considerados.
