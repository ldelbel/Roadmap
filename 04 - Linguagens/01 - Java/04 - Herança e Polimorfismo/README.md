# Heranca e Polimorfismo

Classes Abstratas e Interfaces são importantes quando buscamos definir responsabilidade única para classes. 

## 1. Quadro comparativo

| Característica | Interface | **Classe Abstrata**|  
|--|--|--|
| Herança múltipla |  Uma classe pode implementar diversas interfaces | Uma classe pode herdar somente uma classe
| **Implementação Padrão** |Uma interface não pode conter qualquer tipo de código, muito menos código padrão. |Uma classe abstrata pode fornecer código completo, código padrão ou ter apenas a declaração de seu esqueleto para ser posteriormente sobrescrita.
 |**Constantes**  |Suporte somente constantes do tipo estática. |Pode conter constantes estáticas e de instância.
| **Componentes de terceiros**| Uma implementação de uma interface pode ser incluída a qualquer classe de terceiros. | Uma classe de terceiros precisa ser reescrita para estender somente a partir da classe abstrata. |
| **Homogeneidade** | Se todas as diversas implementações compartilham a assinatura do método então a interface funciona melhor. |Se as várias implementações são todas do tipo e compartilham um comportamento e status comum , então a classe abstrata funciona melhor.|
| **Manutenção** | Se o código do seu cliente conversa somente em termos de uma interface, você pode facilmente alterar a implementação concreta usando um método factory. | Idêntico |
| **Velocidade** | Lento, requer trabalho extra para encontrar o método correspondente na classe atual. | Rápido|
| **Clareza** | Todas as declarações de constantes em uma interface são presumidamente publicas ou estáticas. | Você pode por código compartilhado em uma classe abstrata. Você pode usar código para computar o valor inicial de suas constantes e variáveis de instância ou estáticas. |
| **Funcionalidades Adicionais** | Se você incluir um novo método em uma interface você precisa ajustar todas as implementações da interface.|Se você incluir um novo método em uma classe abstrata você tem a opção de fornecer uma implementação padrão para ele. |

## 2. Upcasting 
Fazer um objeto se passar por um objeto que seja um supertipo dele. Ele sempre funcionará já que todo objeto é completamente compatível com um tipo do qual ele foi derivado. Como sempre pode ser realizado, é possível fazer implicitamente, ou seja, o compilador faz por você quando for necessário.

É muito comum ele ocorrer como parâmetro de um método que usará polimorfismo. O construtor manda como argumento um objeto que é o subtipo, o método recebe um parâmetro como se fosse o supertipo, mas funciona como um subtipo.

Algumas pessoas gostam de chamar de **promoção de tipo.

## 3. Downcasting 
Quando o objeto se passa como se fosse um subtipo dele. Não há garantias que funcione (pode lançar uma ClassCastException, o que obviamente é um erro de programação) e pode haver necessidade de conversões. 

O compilador só aceita se ele **puder provar que o objeto se encaixará perfeitamente e seja de fato aquele objeto.** Por isso deve ser explicitado pelo programador quando deseja essa ação. A coerção ocorre em tempo de execução.

Existe um padrão normalmente usado para evitar a exceção quando não se tem certeza que dará certo:

~~~ 
obj instanceof Tipo ? (Tipo)obj : null 
~~~ 

Nesse exemplo se o objeto não for do tipo adequado, ele criará um nulo e nem tentará o cast. 

Obviamente que qualquer tentativa de acesso ao objeto gerado será problemático, então é preciso verificar se o objeto é nulo antes de tentar acessá-lo, caso contrário, só trocará de erro.

