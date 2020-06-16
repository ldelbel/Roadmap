# Qual estrutura devo usar? 

Collection é o pacote a ser implementado pelas estruturas de Set e List. Map não estende de Collection. 

| Estrutura | Característica  | Duplicidade | Valores nulos | 
|:--:|--|--|--|
| List |Sequência de valores ordenada por ordem de inserção.   |Permite duplicados. | Permite valores nulos infinitamente. 
|Set| Apenas valores únicos | Não permite valores duplicados | Permite um único valor nulo. 
|Map| Quando precisar de pares de chave-valor | Permite valores duplicados, mas não permite chaves duplicadas. | Permite uma única chave nula, mas infinitos valores nulos. 

