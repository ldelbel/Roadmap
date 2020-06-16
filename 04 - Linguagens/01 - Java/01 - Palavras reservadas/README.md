# Java Keywords

[Básico] Guia de palavras reservadas em java

## Modificadores de acesso
**private:** acesso apenas dentro da classe

**protected:** acesso por classes no mesmo pacote e subclasses

**public:** acesso de qualquer classe

 Modifier   |   Class |   Package |   Subclass |  World
-----------|:-----------:|:-----------:|:-----------:|:-----------:
public     |     ✔   |     ✔   |      ✔    |     ✔
 protected  |     ✔    |    ✔    |     ✔    |     ✘
 no modifier |    ✔    |    ✔  |       ✘     |    ✘
 private   |      ✔   |     ✘   |      ✘    |     ✘

## Modificadores de classes, variáveis ou métodos

### 1. Abstract e Extends
Pode-se dizer que as classes abstratas servem como “modelo” para outras classes que dela herdem, não podendo ser instanciada por si só. 

Para ter um objeto de uma classe abstrata é necessário criar uma classe mais especializada herdando dela e então instanciar essa nova classe. Os métodos da classe abstrata devem então serem sobrescritos nas classes filhas.

Usa-se **extends** quando você deseja aplicar herança á sua classe.

Classe abstrata Conta:
~~~ 
abstract class Conta {
     
    private double saldo;
     
    public void setSaldo(double saldo) {
        this.saldo = saldo;
    }
     
    public double getSaldo() {
        return saldo;
    }
     
    public abstract void imprimeExtrato();
 
}
~~~

Classe que implementa: Conta poupança

~~~ 
import java.text.SimpleDateFormat;
import java.util.Date;
 
public class ContaPoupanca extends Conta {
 
    @Override
    public void imprimeExtrato() {
        System.out.println("### Extrato da Conta ###");
         
        SimpleDateFormat sdf = new SimpleDateFormat("dd/MM/aaaa HH:mm:ss");
        Date date = new Date();
         
        System.out.println("Saldo: "+this.getSaldo());
        System.out.println("Data: "+sdf.format(date));
         
    }
}
~~~

O método **imprimeExtrato()** tem uma annotation conhecida como **@Override**, significando que estamos sobrescrevendo o método da superclasse. 

Entende-se em que na classe abstrata **Conta** os métodos que são abstratos têm um comportamento diferente, por isso não possuem corpo. As subclasses que estão herdando precisam desse método porém teremos que inserir as particularidades de cada subclasse.

Quando falamos que a classe A estende a classe B, significa que A herda alguns (ou todos) métodos e atributos da classe B.

Os únicos métodos e atributos que não são herdados são os que possuem o modificador de acesso private.

Pode-se aplicar diversos níveis de herança. Por exemplo:

~~~
class A extends B { }
class B extends C { }
class C extends D { }
~~~

Ao fazer isso, os membros com modificador de acesso public das classes D, C e B são acessíveis na classe A. 

Os membros com modificador de acesso **protected** da classe B também são acessíveis na classe A.

Em Java é possível herdar apenas de uma classe. **Não existe herança múltipla.**

### 2. Interface e implements

Uma interface "firma um contrato" entre classes em que define comportamentos (métodos) que devem ser sobrescritos pela classe que os herda.

Quando você implementa uma interface você vai ter que **obrigatoriamente** declarar todos os metodos existentes nesta interface.

A opção de implementa-los ou não é do desenvolvedor, mas **todos devem ser declarados mesmo que de forma vazia**.

Na interface a seguir, Jogar chama tocar(), porém a implementação dela se torna opcional na classe Futebol, mas a declaração dela é torna obrigatoria: 

~~~
public interface Jogar {

          void chutar();
          void tocar();
}

public class Futebol **implements** Jogar {

 void chutar() {
    System.out.println("Chutando uma bola!");
 }
 
 void tocar(){
 }
 
}       
~~~

### 3. Class e new

#### 3.1 Classe 
Em Java, um objeto é criado a partir de uma classe. Para criar um objeto de MinhaClasse, especifique o nome da classe, seguido pelo nome do objeto, e use a palavra **new**

~~~
public class MinhaClasse {
  int x = 5;

  public static void main(String[] args) {
    MinhaClasse objeto = new MinhaClasse();
    System.out.println(objeto.x);
  }
}
~~~

#### 3.2 New 
New é utilizado para criar uma nova instância de uma determinada classe.

Imagine que a planta de uma casa é a classe e uma casa construída a partir dessa planta seria a instância dessa classe - um novo objeto. 

Você pode construir diversas casas a partir dessa mesma planta, ou seja, você pode criar diversos objetos que são instâncias da mesma class.

O new faz com que a máquina virtual **aloque memória** para criar uma instância de um objeto. Além disso, **retorna o endereço(ponteiro)** para acessar a parte da memória onde foi alocado esse espaço.

**Instância** é o espaço da memória alocado q tem **todas as características descritas na classe** da classe que você criou. 

### 4. Final e Static

#### 4.1 Final
Impossibilita que uma classe seja estendida, que um método seja sobrescrito ou que uma variável seja reinicializada.

##### 4.1.1 Método final
É um método que não pode ser sobrescrito nas subclasses.
Use para garantir que um determinado algoritmo não possa ser modificado pelas subclasses.

~~~ 
class ChessAlgorithm {
    enum ChessPlayer { WHITE, BLACK }
    ...
    final ChessPlayer getFirstPlayer() {
        return ChessPlayer.WHITE;
    }
    ...
}
~~~

##### 4.1.2 Atributo final
Um atributo final de uma classe pode ter seu valor atribuído uma única vez, seja na própria declaração ou no construtor.

Use isso para garantir que um valor ou referência de objeto não vai mudar. Voltamos à **imutabilidade.**

Se você tem um algoritmo que usa esse variável, você pode armazenar valores calculados sem a preocupação do valor mudar.

~~~
public class CalculaSaldo{
    final Cliente cliente;
    final Double saldo;

    public CalculaSaldo(Cliente cliente) {

        this.cliente = cliente;

        //sabemos que saldo não muda
        this.saldo = cliente.calculaSaldo();
    }

    public Double getSaldoCliente() {
        //não precisa mais recalcular toda vez
        return saldo;
    }
}
~~~

#### 4.2 Static
O static **muda o escopo** de um método ou atributo. Com o static, ao invés deles pertencerem à instância do objeto, eles pertencem à classe.

Static significa que algo pertence diretamente a classe e que não precisa de uma instância dessa classe para poder acessá-lo.

Uma classe pode ter vários objetos. Por exemplo:
~~~
Carro vectra = new Carro();
Carro palio = new Carro();
~~~

Aqui temos apenas **uma classe**: “Carro”
Mas temos **dois objetos**: “vectra” e “palio”.

Uma variável static da classe Carro teria o mesmo valor para qualquer objeto (vectra, palio, fusca, ferrari…). 

Se você não coloca static nas variáveis, elas ficam com uma cópia diferente pra cada objeto.

**Dentro de métodos static somente é possível pode acessar outros métodos e variáveis que também sejam static.

Caso seja criado um novo objeto, as variáveis serão zeradas, enquanto que com o uso do static não, pois **a variável pertence à classe** e não ao objeto.


~~~
class StaticTemporaria {

public static int contador_static = 0;
public int contador_normal = 0;

 public StaticTemporaria() {
 }

 public static void incrementaStatic(){
     contador_static++;
     System.out.println("Contador STATIC agora é = " + contador_static);
 }

 public void incrementaContador() {
     contador_normal++;
     System.out.println("Contador NORMAL agora é = "+ contador_normal);
 }
}
~~~ 

~~~
public class Static{

 public static void main(String args[]) {
   StaticTemporaria s1 = new StaticTemporaria();
   s1.incrementaStatic();
   s1.incrementaContador();

   StaticTemporaria s2 = new StaticTemporaria();
   s2.incrementaStatic();
   s2.incrementaContador();
 }
}
~~~

Output: 
~~~
    Contador STATIC agora é = 1
    Contador NORMAL agora é = 1
    
    Contador STATIC agora é = 2
    Contador NORMAL agora é = 1
~~~

### 5. Strictfp (Pontos flutuantes)

A palavra-chave strictfp garante que você obtenha o mesmo resultado em todas as plataformas se executar operações na variável de ponto flutuante. 

A precisão pode variar de plataforma para plataforma, e é por isso que em java se usa a strictfp: para que se obtenha o mesmo resultado em todas as plataformas. P

### 6. Syncronized

Imagine que duas Threads diferentes **de um mesmo objeto** tentem chamar o método add para um dado objeto. 

Como é o método é synchronized, uma Thread terá de esperar que a Thread que chamou o método primeiro termine a execução do mesmo.

A finalidade do synchronized é evitar que você tenha problemas com estados indeterminados em um programa. Suponha que você tivesse um método para remover elementos do ArrayList. Se esse método não fosse synchronized, poderia ocorrer de você ter duas Threads tentando remover o mesmo objeto do ArrayList, o que provocaria problemas inesperados.

O Java atualmente permite 3 modos de sincronização de código:

`public synchronized void addContador() { 
 //implementação
 }`

Esta versão de addContador() é um método de instância, ou seja, threads diferentes podem invocar addContador() simultaneamente desde que as chamadas sejam realizadas em instâncias diferentes. 

O lock é feito na instância em que addContador() foi invocado.

`public static synchronized void addContador() {
 //implementação
 }`
 
Já esta versão de addContador() só pode ser executada por uma Thread por vez, pois o lock é feito **no objeto** Class do tipo em que addContador() foi invocado.

Por último o Java ainda permite o uso de blocos synchronized:

`public void addContador() { 
  synchronized(user) { .... } 
 }`

Neste caso, a política de execução vai depender do objeto passado no bloco. 

* Se for de instância, a trava é feita na instância. 
* Se for um atributo estático, a trava é feita no objeto Class. Ela te permite uma liberdade maior por permitir que apenas uma porção do método seja sincronizada.

### 7. Transient e Volatile

Eles não são modificadores de acesso, mas modificam como a Máquina Virtual Java trata os atributos em tempo de execução.

#### 7.1 Transient

O atributo **transient** impede a serialização de campos. Isso significa que ele não será serializado ou desserializado juntamente com os demais atributos de um determinado objeto.

* **Serialização**: é o processo no qual os atributos de um objeto (estado) são convertidos, um a um, numa sequência de bytes. 
* **Desserialização**: é o processo inverso, onde bytes são lidos e um novo objeto é construído.

As aplicações mais comuns são:

* Transmissão de objetos pela rede.
* Servlets: distribuição de objetos na sessão entre os nós de um cluster
* Salvar objetos em arquivos ou bancos de dados. Esta geralmente é uma abordagem ad hoc para guardar configurações ou estado de forma "fácil"

Você define explicitamente que não quer serializar um determinado atributo com transient basicamente nos casos a seguir:

* Você quer serializar a classe, mas um atributo de um certo tipo (classe) não é serializável, portanto o processo iria falhar.
* O valor do atributo é algum tipo de cache e você não precisa dele, portanto isso economiza memória e processamento.
* O atributo representa alguma entidade local e não faz sentido transmiti-la, por exemplo uma conexão com o banco de dados (Connection) ou qualquer referência a um recurso que precisa ser aberto e fechado.

**É importante também mencionar que esse atributo não tem efeito se você sobrescrever os métodos writeObject e readObject, que habilitam, respectivamente, a serialização e desserialização manual dos objetos.**

#### 7.2 Volatile

Quando definido um campo como volatile, um campo será visto de forma compartilhada/atualizada por todas as threads que utilizarem esta variavel.

O volatile é uma marcação que induz a JVM a não realizar caches na variável, ou então, a esperar a escrita de uma outra thread antes de realizar a leitura. A consequência é que o acesso a uma variável volatile é mais lenta que o normal.

Esse modificador não deve ser utilizado como alternativa a synchronized, ele garante acessos atualizados, mas não previne race-conditions.

## Controle de fluxo dentro de um bloco de código

### 1. Switch Case e default

A estrutura switch verifica uma variável e age de acordo com seus cases. Os cases são as possibilidades de resultados que são obtidos por switch.

Basicamente, o switch serve para controlar várias ações diferentes de acordo com o case definido dentro dele.

* **Case:** executa um bloco de código dependendo do teste do switch.

* **Default:** executa esse bloco de codigo caso nenhum dos teste de switch-case seja verdadeiro.

~~~
public class ExemploSwitch {
    public static void main(String args[]) {
        int diaDaSemana = 1;
        switch (diaDaSemana) {
            case 1:
                System.out.println("Domingo");
                break;
            case 2:
                System.out.println("Segunda-feira");
                break;
            case 3:
                System.out.println("Terça-feira");
                break;
            case 4:
                System.out.println("Quarta-feira");
                break;
            case 5:
                System.out.println("Quinta-feira");
                break;
            case 6:
                System.out.println("Sexta-feira");
                break;
             case 7:
                System.out.println("Sábado");
                break;
            default:
                 System.out.println("Este não é um dia válido!");
         }
    }
}
~~~

E vale também ressaltar que case não gera resultados booleanos, portanto, não há a possibilidade de fazer comparações 

`Errado: case (var1 > var2):`

### 2. Break e Continue

#### 2.1 Break

#### 2.1.1 Break no Switch
~~~ 
String resultado = "";

switch (exemplo) {
case 0:
  result = "blah";
  break;
case 1:
  result = "foo";
  break;
}

return resultado;
~~~

#### 2.1.2 Break no If (Sair de um loop)
~~~ 
for (int i = 0; i < 10; i++) {
  if (i == 4) {
    break;
  }
  System.out.println(i);
}
~~~

#### 2.2 Continue

Um continue interrompe uma iteração (no loop), se uma condição especificada ocorrer e continua com a próxima iteração no loop.

~~~
for (int i = 0; i < 10; i++) {
  if (i == 4) {
    continue;
  }
  System.out.print(i + " ");
}
~~~

Output:
~~~
0 1 2 3 5 6 7 8 9
~~~ 

### 3. While e Do While

### 3.1 While

Esta instrução é usada quando não sabemos quantas vezes um determinado bloco de instruções precisa ser repetido. 

Com ele, a execução das instruções vai continuar até que uma condição seja verdadeira. A condição a ser analisada para a execução do laço de repetição deverá retornar um valor booleano.

~~~
while (teste condicional){
   //serão executados enquanto o teste condicional for igual a verdadeiro (true)
   implementação;
}
~~~ 

Perceba que, **somente se a condição for verdadeira, o corpo do laço de repetição, com seus respectivos comandos, serão executados.** Portanto, o conteúdo será repetido até que esta condição não seja mais verdadeira.

### 3.2 Do While

O do/while tem quase o mesmo funcionamento que o while, a diferença é que com o uso dele **teremos os comandos executados ao menos uma única vez.**

~~~
decimal aumento = 250;

 do {
  Console.WriteLine("O valor atual do aumento é de: " + aumento);
  aumento += 50;
 } while (aumento < 500);     
~~~

### 4. For e For each

#### 4.1 For

Quando você souber exatamente quantas vezes deseja fazer um loop através de um bloco de código, use o for em vez de um while.


* A instrução 1 é executada (uma vez) antes da execução do bloco de código.
* A instrução 2 define a condição para executar o bloco de código.
* A instrução 3 é executada (todas as vezes) após a execução do bloco de código.

~~~
for (instrução 1; instrução 2; instrução 3) {
  // code block to be executed
 }
~~~

#### 4.2 For-each

Há também um loop " for-each ", que é usado exclusivamente para percorrer elementos quando já conhecemos o tamanho de um array (ou lista).

A grande diferença do foreach e o for tradicional é que com o foreach ele so percorre os elemento de forma crescente ou seja para frente. 

Se voce precisa percorrer os elemento da sua lista para que possam ser impressos de forma decrescente(tras para frente) tera que recorrer ao for normal. 

~~~
List <String> listaFrutas = new ArrayList<>();

    listaFrutas.add("Maçã");
    listaFrutas.add("Uva");
    listaFrutas.add("Banana");
    listaFrutas.add("Banana");
    listaFrutas.add("Mamao");
    listaFrutas.add("Laranja");
    listaFrutas.add("Morangp");

    for(String lista: listaFrutas){
        System.out.println(lista);
    }
~~~

### 5. If e if else

Java suporta as condições lógicas usuais da matemática:

* Menor que: a <b
* Menor ou igual a: a <= b
* Maior que: a> b
* Maior ou igual a: a> = b
* Igual a a == b
* Não é igual a: a! = B

~~~ 
if (condição1) {
  // bloco de código a ser executado se a condição1 for verdadeira
} else if (condição2) {
  // bloco de código a ser executado se a condição1 for falsa e a condição2 for verdadeira
} else {
  // bloco de código a ser executado se a condição1 for falsa e a condição2 for falsa
}
~~~

O else if serve para tratar das exceções das exceções. 

### 6. Instanceof 

Determina se um objeto é uma instância de determinada classe, superclasse ou interface. Retorna **true ou false**.

Um operador instanceof é usado na **comparação de variaveis de referencia de objeto.**

Você normalmente o usa quando tem uma referência ou parâmetro para um objeto que é de uma superclasse ou tipo de interface e precisa saber se o objeto real tem algum outro tipo (normalmente mais concreto).

~~~
static void method(Food a) {
   if (a instanceof Bread) {
       Bread b = (Bread) a;
       System.out.println("Downcasting performed"); 
   }
}
~~~ 

Observe que, se você precisar usar esse operador com muita frequência, geralmente é uma dica de que seu design tem algumas falhas.

## Tratamento de erros

### 1. Assertions

Testa uma expressão condicional para verificar uma suposição do programador. **Retorna como uma exceção.** 

Para adicionar asserções, basta usar a palavra-chave assert e fornecer uma condição booleana: 

~~~
public void setup() {
    Connection conn = getConnection();
    assert conn != null;
}
~~~

Java também fornece uma segunda sintaxe para asserções que usam uma String para construir o AssertionError se uma condição de erro for lançada:

~~~
public void setup() {
    Connection conn = getConnection();
    assert conn != null : "Connection is null";
}
~~~ 

É uma boa opção para testes rápidos. 

~~~
int sum(int a, int b) {
    assert (Integer.MAX_VALUE - a >= b) : "Value of " + a + " + " + b + " is too large to add.";
  final int result = a + b;
    assert (result - a == b) : "Sum of " + a + " + " + b + " returned wrong sum " + result;
  return result;
}
~~~

### 2. Try-Catch e Finally

#### 2.1 Try-catch

É uma maneira robusta de tratar possíveis erros no momento da conversão.

Exemplo:
>Não é possível converter um caractere “?” por um número, porém como a entrada de dados é liberada o usuário final poderá digitar algo inadequado, resultando em erro e quebra da execução do programa por falha.Com o try podemos evitar esta queda brusca e então tratar o erro da melhor forma.

~~~
try {
  // código que inclui comandos/invocações de métodos que podem gerar uma situação de exceção.
} catch (XException ex) {
  // bloco de tratamento associado à condição de exceção XException ou a qualquer uma de suas subclasses, identificada aqui   //pelo objeto com referência ex
} catch (YException ey) {
  // bloco de tratamento associado à condição de exceção XException ou a qualquer uma de suas subclasses, identificada aqui   //pelo objeto com referência ey
} finally {
  // bloco de código que **sempre** será executado após o bloco try, independentemente de sua conclusão ter ocorrido
  //normalmente ou ter sido interrompida
}
~~~ 

A ordem em que colocamos os blocos “catch” é muito importante: deve ser da mais específica para a mais genérica. Exemplo:
~~~
try {
  comando(s);
} catch (Exception e) {
  comando(s);
} catch (FileNotFoundException f) {
  comando(s);
}
~~~

Supondo que ocorreu uma “FileNotFoundException” dentro do bloco “try”, a execução vai procurar o primeiro bloco “catch” que seja compatível com o tipo de Exception ocorrida. 

O primeiro bloco será analisado e, como Exception é superclasse de “FileNotFoundException”, a execução entrará no primeiro bloco “catch”. O segundo sequer será testado.

Para que tudo funcione temos que trocar a ordem dos blocos “catch”:

~~~
try {
  comando(s);
} catch (FileNotFoundException f) {
  comando(s);
} catch (Exception e) {
  comando(s);
}
~~~

#### 2.2 Finally

As vezes é necessário executar um código mesmo que tenha havido uma Exception. É para isto que servem os blocos “finally”.

~~~
try {
  comando(s);
} finally {
  comando(s);
}\ou
try {
  comando(s);
} catch (ClasseDeException VarException) {
  comando(s);
} finally {
  comando(s);
}
~~~

Os comandos dentro de um bloco “finally” serão executados de qualquer maneira, mesmo que a execução tenha passado por um bloco “catch”.

Ao contrário dos blocos “catch” você só pode ter um bloco “finally” por cada bloco “try”.

### 3. Throw e Throws

#### 3.1 Throws

A palavra-chave throws serve para declarar que um método pode lançar exceções de um determinado tipo. 

~~~
public void addContador(int numero) throws Exception {
  if (numero < 0) {
    throw new Exception("Número não pode ser menor que zero!");
  }
  // resto do método
}
~~~

Criando a própria exceção: 

~~~
class MinhaClasse {

  // o "throws" no método abaixo indica que ele lança.
  // a exceção "NumeroMenorQueZeroException", que criamos acima:

  public void addContador(int numero) throws NumeroMenorQueZeroException{
    if (numero < 0) {
      throw NumeroMenorQueZeroException("Numero não pode ser menor que zero!");
    } else {
      // faz algo com o número maior ou igual a zero.
    }
  }
}
~~~ 

#### 3.2 Throw

Throw é um statement, ele manda a exceção ser lançada.

~~~
public void M2() {
    throw new IOException();
}
~~~ 

Este método lança uma exceção mas não exige que ela seja tratada por seus chamadores. Ele transfere o controle do fluxo para os métodos chamadores. 

Ele usa o que se chama unckecked exception, ou seja, uma exceção é lançada mas nada obriga ela ser tratada. É **tratado em tempo de execução.**

## Controle de pacotes

### 1. Import e packages
É possível "importar um pacote inteiro" (todas as classes do pacote, exceto os subpacotes) através do coringa **(*)**:

`import java.util.*;`

Importar todas as classes de um pacote não implica em perda de performance em tempo de execução, mas pode trazer problemas com classes de mesmo nome! 

Além disso, importar de um em um é considerado boa prática, pois facilita a leitura para outros programadores. Uma IDE como o Eclipse já vai fazer isso por você, assim como a organização em diretórios.

Import | Descrição
------|:------------
import java.net.*; | 	Importa todas as classes do pacote java.net.
import java.net.URL; | 	Importa apenas a classe URL do pacote java.net.
import static java.awt.Color.*; | Importa todos os membros estáticos da classe Color do pacote java.awt (diposnivel a partir do Java 5).
import static java.awt.color.ColorSpace.CS_GRAY; | 	Importa o membro estático CS_GRAY da classe Color do pacote java.awt

## Primitivos

* **boolean:** um valor indicando verdadeiro ou falso
* **byte:** um inteiro de 8 bits (signed)
* **char:** um caracter unicode (16-bit unsigned)
* **double:** um número de ponto flutuante de 64 bits (signed)
* **float:** um número de ponto flutuante de 32 bits (signed)
* **int:** um inteiro de 32 bits (signed)
* **long:** um inteiro de 64 bits (signed)
* **short:** um inteiro de 32 bits (signed)

## Variáveis de referência

### 1. Super
O super é utilizado para acessar o construtor da classe pai.
Chamar o construtor da superclasse e também chamar seus métodos usando super. 

Imagine que você tenha uma classe chamada de Gerente que herda da classe Funcionário e que ambas as classes possuem um método chamado calcularGratificacao(). 

Estando na classe Gerente como fazer para chamar o método calculaGratificacao() da superclasse (Funcionario)?

`super.calcularGratificacao();`

**A super classe chamada é a superclasse imediata. 

### 2. This

É uma abreviação, que só pode ser usada no início de um construtor, e diz basicamente que é para reaproveitar o código de um outro construtor dessa mesma classe.

É a referência direta à própria instância. É o mesmo que usar o nome da classe, que, por consequência é o mesmo nome do(s) método(s) construtor(es), diferenciados pelos parâmetros.

~~~
class Cidade {
    
    private String nome;
    private int populacao;
    private String estado;
    
    //A variável local **nome** recebe o valor do argumento nome.
    public Cidade (String nome) {
        this.nome = nome;
    }
    
    public Cidade (String nome, int populacao) {
         // isto está reaproveitando o construtor que aceita só o nome.
         this (nome); 
         this.populacao = populacao;
    }
    
    public Cidade (String nome, int populacao, String estado) {
         // reaproveita o construtor que aceita nome e populacao
         this (nome, populacao);
         this.estado = estado;
    }
}
~~~

## Retorno de um método

### 1. Void
indica que o método não tem retorno.

### 2. Return
Retorna de um método **sem executar qualquer código que venha depois desta linha**.

É usado para sair de um método, com ou sem um valor.





