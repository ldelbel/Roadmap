# Abstract Classes

Herança (através de classes abstractas) não deve ser abusada! Algumas pessoas tendem a abusar de classes abstratas com um objectivo em mente: reutilizar código, que de outra forma seria repetido em classes concretas.

Isto esta errado! Herança deve ser usada em um e um só caso: quando existe uma relação "é um tipo de" entre a classe concreta e a abstrata. Por exemplo, `um gato é um tipo de animal` ou `um apartamento é um tipo de casa`.

## 1. Características 

* As classes abstratas devem conter pelo menos um método abstrato, que não tem corpo.
* É um tipo especial de classe que não há como criar instâncias dela.
* É usada apenas para ser herdada, **funciona como uma super classe**.
* Uma grande vantagem é que força a hierarquia para todas as sub-classes.
* É um tipo de contrato que faz com que as sub-classes contemplem as mesmas hierarquias e/ou padrões.

Quando nos criamos uma Classe Abstrata, nós estamos **criando uma classe base** que pode ter um ou mais métodos completos, mas pelo menos **um ou mais destes métodos tem que criados incompletos (sem corpo)**, isto caracteriza uma Classe Abstrata.

> Vale lembrar que, se todos os método da Classe abstrata forem sem corpo, ela se torna uma Interface.

O propósito de uma Classe Abstrata é **prover uma base de definições de como um set de Classes Derivadas irão trabalhar** e então p**permitir os programadores de preencher as implementações** nas Classes derivadas.

Pode-se dizer que as classes abstratas servem como `modelo` para outras classes que dela herdem, não podendo ser instanciada por si só. 

Para ter um objeto de uma classe abstrata é necessário criar uma classe mais especializada herdando dela e então instanciar essa nova classe. Os métodos da classe abstrata devem então serem sobrescritos nas classes filhas.

## 2. Quando usar

Se há duas classes que **possuem código em comum**, você pode agrupar este código refatorando e colocando em uma superclasse o código repetido, e, ambas as subclasses extenderem a superclasse, **implementando ali suas particularidades**.

Classes abstratas representam uma relação de tipos. Aquele mesmo método, se usasse uma classe abstrata diria: “Eu preciso de um objeto que seja do mesmo tipo desse outro objeto aqui”.

Isso é uma relação muitíssimo mais forte e, portanto, você poderá esperar por mais acoplamento em seu sistema. Até por isso, classes abstratas também podem conter atributos, métodos protegidos, chamar métodos das classes filhas, etc. 

Afinal, estamos falando de classes do mesmo tipo.

## 3. Exemplos

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

Variáveis conhecidas:
`private double saldo` 

Métodos implementados: 
`public void setSaldo(double saldo)`
`public double getSaldo()`

Métodos não-implementados: 
`public abstract void imprimeExtrato()`

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

Conta poupança implementa `imprimeExtrato()`. Também poderia fazer uso dos demais métodos: 

~~~
public class TestaConta {
    public static void main(String[] args) {
        Conta cp = new ContaPoupanca();
        cp.setSaldo(2121);
        cp.imprimeExtrato();
 
    }
}
~~~
