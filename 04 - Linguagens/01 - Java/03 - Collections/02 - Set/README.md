# Set

| Implementação | Característica  |
|--|--|
| TreeSet | Ordenação por valor |
|LinkedHashSet| Ordenação por inserção | 
|HashSet| Propósito geral, não ordena.  | 

> Nenhuma dessas estruturas permite valores duplicados. 

Estruturas de dado do tipo “Set” são conhecidas por aceitar apenas valores únicos, ou seja, **qualquer valor duplicado inserido em um “Set” será automaticamente excluído**, por isso muito cuidado ao escolher uma List ou Set.

* Esta interface não armazena a posição em que os elementos estão armazenados.
* A interface entende que as classes que a implementam são como conjuntos matemáticos onde a posição não é relevante.   

É importante notar que `TreeSet`, `HashSet` e `LinkedHashSet` implementam a interface `Set`, ou seja, temos os mesmos métodos para as 3 estruturas. 

O que difere cada uma é a forma com que é implementado o algoritmo, por exemplo, a HashSet usa HashTable em sua implementação, que por sinal é muito rápido mas não garante a ordenação dos seus elementos. 

É importante salientar uma questão muito importante:  nenhuma das implementações da interface `Set` são thread-safe. 

Se você está usando múltiplas threads para acessar o mesmo Set você deve sincronizar esses acessos externamente, pois  o Set não o fará. 

**Esse é um ponto fraco para aplicações que trabalham com frequência com múltiplas threads, pois você teria que ficar sincronizando os acessos ao seu Set para garantir a consistência dos dados**, porém levando em consideração a rapidez do HashSet ou mesmo a unicidade de elementos do Set como um todo, você deve ponderar se vale a pena deixar de usar o Set por falta de sincronismo nativo. 

## 1. TreeSet

O `TreeSet` implementa um algoritmo conhecido por red-black tree ou árvore rubro-negra. 

Sua principal característica é que ele **é o único Set que implementa a interface SortedSet em vez de Set diretamente**, mas de qualquer forma `SortedSet` implementa `Set`, assim continuamos tendo os mesmo métodos no `TreeSet`. 

Pelo fato de ele implementar `SortedSet` ele **possui elementos ordenados automaticamente**, ou seja, independente da ordem que você inserir os elementos, eles serão ordenados. 

Isso tem um custo: a complexidade para os métodos add, remove e contains são bem maiores que do HashSet, são elas O(log (n)), não é bem uma complexidade exponencial mas é bem maior que O(1) que tem seu tempo inalterado.

Por implementar `SortedSet`, o `TreeSet` oferece mais alguns métodos como: first(), last(), headSet(), tailSet().

## 2. HashSet

O HashSet é o **mais rápido de todos**, pois usa HashTable e **seus elementos não são ordenados**.

A complexidade desta estrutura é O(1), em outras palavras, não importa o quanto você adicione, remova, retire, o tempo de execução sempre será o mesmo. 

Isso é extremamente crítico em processos onde temos uma situação crítica com milhões de dados a serem inseridos em um Set.

Por outro lado, a garantia de continuidade na ordem dos elementos inseridos é zero, ou seja, esse tipo de estrutura é indicada se você precisa apenas garantir a alta performance sem se importar com a ordem com que os elementos estão ordenados.

## 3. LinkedHashSet

O LinkedHashSet faz uso também do HashTable com linked list, ou seja, temos aqui a seguinte situação: Os elementos continuam na ordem que são inseridos, diferente do HashSet que “embaralha” tudo. 
