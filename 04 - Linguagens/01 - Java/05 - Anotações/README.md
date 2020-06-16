# Anotacoes

As anotações são úteis quando desejamos anotar código não simplesmente para documentação, mas de maneira que essas marcações possam ser verificadas em tempo de compilação, ou utilizadas por ferramentas, tais como analisadores de código, frameworks de persistência ou de testes unitários, entre outras. 

## 1. Tipos 

### 1.1. Anotações marcadoras  

São aquelas que não possuem membros e identificadas apenas pelo nome, sem dados adicionais.  

Exemplo: `@Teste`. 

### 1.2. Anotações de valor único  

São similares às anteriores, no entanto, possuem um único membro, chamado valor. Elas são representadas pelo nome da anotação e um par nome=valor, ou simplesmente com o valor, entre parênteses.  

Quando a anotação possui um único membro, só é necessário informar o valor, além do nome da anotação.  

Exemplo: `@MinhaAnotacao(“valor”)`

### 1.3. Anotações completas  

São aquelas que possuem múltiplos membros. Devemos usar a sintaxe completa para cada par nome=valor e cada par é informado separado do outro por uma vírgula.  

Exemplo: `@Version(major=1, minor=0, micro=0)`  

## 2. Anotações comuns 

### 2.1. @Override 

É uma anotação marcadora que deve ser usada apenas com métodos. Serve para indicar que o método anotado está sobrescrevendo um método da superclasse. 

### 2.2. @Deprecated 

Assim como @Override, é também uma anotação marcadora.  

Esta anotação é utilizada quando é necessário indicar que um método não deveria mais ser usado, ou seja, informa que o método está obsoleto.  

@Deprecated deve ser colocada na assinatura do método. 

Usada porque precisamos manter a compatibilidade com sistemas legados que usam a classe. 

Mesmo implementando uma nova versão de um método, os sistemas que já existem precisam continuar funcionando. Os programadores serão então alertados da mudança e gradativamente irão modificando suas aplicações para se adaptar à nova versão da classe. 

Exemplo:  

~~~
@Deprecated 
public double getSalarioTotal 
~~~

### 2.3. @SuppressWarnings 

Permite desligar os alertas de uma parte do código da aplicação e os warnings do restante do código permanecem inalterados. 

É uma anotação de valor único, onde o valor é um array de String. Neste array, cada elemento é um tipo de alerta a ser suprimido.  

Exemplo: `@SuppressWarnings(value={"unchecked", "rawtypes"})`

### 2.4. @Retention 

As anotações podem estar presentes apenas no código fonte ou no binário de classes ou interfaces.  

@Retention é usada para escolher entre essas possibilidades.  

Ela suporta três valores:  
* SOURCE: para indicar que as anotações marcadas não estarão no código binário;  
* CLASS: para gravar as anotações no arquivo .class, mas não estarão disponíveis em tempo de execução;  
* RUNTIME: para indicar que as anotações estarão disponíveis em tempo de execução; 

### 2.5. @Documented 

É uma anotação marcadora usada para indicar que os tipos anotação anotados com ela serão incluídos na documentação Javadoc; 

### 2.6. @Target 

Ao criar um tipo anotação é possível estabelecer que elementos de uma classe podem ser anotados com ele. Para obter esse efeito, usamos `@Target`.

### 2.7. @Inherited 

Por padrão anotações declaradas em uma classe não são herdadas pelas subclasses.  

Se for necessário que essa herança ocorra, então o tipo anotação que desejamos que seja herdado deve ser anotado com `@Inherited`.  

É importante destacar que a utilização desta meta-anotação restringe-se apenas a classes.  

Exemplo:  
anotações em interfaces não são herdadas pelas classes que as implementam. 

 

