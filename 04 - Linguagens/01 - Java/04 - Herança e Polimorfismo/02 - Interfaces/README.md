# Interfaces

## 1. Definição

* Uma interface não é considerada uma Classe e sim uma **Entidade**.
* Não possui implementação, apenas assinatura, ou seja: **apenas a definição dos seus métodos sem o corpo**.
* **Todos os métodos são abstratos**.
* Seus métodos são implicitamente Públicos e Abstratos.
* Não há como fazer uma instância de uma Interface e nem como criar um Construtor.
* Funcionam como um tipo de "contrato", onde são especificados para uma implementação obrigatória: 
  * atributos; 
  * métodos; 
  * funções.
    
Quando criamos uma Interface, nós estamos basicamente criando um **set de métodos sem qualquer implementação** que deve ser herdado por outras classes já implementadas. 

A vantagem é que desta forma consegue-se prover um caminho para uma classe ser parte de duas classes: 
* uma herdada hierarquicamente; 
* outra da Interface.

As interfaces são **padrões definidos através de contratos ou especificações**. 

Um contrato define um determinado conjunto de métodos que serão implementados nas classes que assinarem esse contrato. 

Uma interface é 100% abstrata, ou seja, os seus métodos são definidos como abstract, e as variáveis por padrão são sempre constantes (static final).

## 2. Quando usar

Quando se quer criar independência de um serviço específico, como por exemplo criar um camada de acesso a diversos bancos de dados, as interfaces auxiliam a abstrair, criando um contrato, onde não importa qual seja, **qualquer classe que queira implementar o serviço, só precisa cumprir os contratos (definir os métodos)**.

Eu prefiro encarar a interface como um compromisso comportamental. 

Por exemplo, quando um método recebe como parâmetro uma interface ele está simplesmente dizendo: “Eu espero um objeto qualquer, desde que ele se comporte dessa maneira”. 

Note que essa é uma relação fraca, pois objetos de tipos completamente diferente podem ter um mesmo comportamento. E um objeto pode ter mais de um comportamento. Por isso, ele pode implementar mais de uma interface.

O objeto pode implementar uma interface em qualquer nível da hierarquia que ele pertença. 

Por exemplo, Você tem 3 níveis: Animal->Mamífero->Cachorro. 

A interface `Farejador` poderá ser implementada apenas na classe `Cachorro`. 

Isso não é possível com classes abstratas, pois cada classe só pode ter uma classe pai. 

Você também poderia fazer isso para classes em diferentes pontos da hierarquia, como implementar `Nadador` para `Pato` (filho de Ave) e não implementar para `Galinha`; e implementar para `Jacaré` (filho de Réptil) e não implementar para `Lagartixa`;

## 3. Exemplos

~~~
interface Conta{
    void depositar(double valor);
    void sacar(double valor);
    double getSaldo();
}
~~~

A interface define o que a ContaPoupança e ContaCorrente precisarão implementar. Cada uma possui suas próprias regras de negócio. 

Conta corrente: 

~~~ 
public class ContaCorrente implements Conta {
    private double saldo;
    private double taxaOperacao = 0.45;
     
    @Override
    public void deposita(double valor) {
        this.saldo += valor - taxaOperacao;
    }
 
    @Override
    public double getSaldo() {
        return this.saldo;
    }
 
    @Override
    public void sacar(double valor) {
        this.saldo -= valor + taxaOperacao;
    }
 
}
~~~

Conta poupança: 

~~~
public class ContaPoupanca implements Conta {
    private double saldo;
     
    @Override
    public void deposita(double valor) {
        this.saldo += valor;        
    }
 
    @Override
    public double getSaldo() {
        return this.saldo;
    }
 
    @Override
    public void sacar(double valor) {
        this.saldo -= valor;
         
    }
 
}
~~~ 

Sem saber qual das contas precisarei chamar, posso criar um método genérico: 

~~~
public class GeradorExtratos {
     
    public void geradorConta(Conta conta){
        System.out.println("Saldo Atual: "+conta.getSaldo());
    }
 
}
~~~

Veja que a instância de GeradorExtratos vem somente em tempo de Runtime e pode ser chamado para os dois tipos de conta.  

~~~
public class TestaContas {
 
    public static void main(String[] args) {
         
        ContaCorrente cc = new ContaCorrente();
        cc.deposita(1200.20);
        cc.sacar(300);
 
        ContaPoupanca cp = new ContaPoupanca();
        cp.deposita(500.50);
        cp.sacar(25);
         
         
        GeradorExtratos gerador = new GeradorExtratos();
        gerador.geradorConta(cc);
        gerador.geradorConta(cp);
    }
 
}
~~~

