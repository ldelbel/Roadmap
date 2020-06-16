# Tutorial-JUnit

## 1. Motivação

Deve-se projetar e escrever as classes de testes, depois as classes com regra de negócios. Assim pode-se utilizar a ferramenta de base para escrever o código. 

## 2. Roadmap

* Defina uma lista de tarefas a implementar (o que testar);
* Escreva uma classe (test case) e implemente um método de teste para uma tarefa da lista;
* Rode o JUnit e certifique-se que o teste falha;
* Implemente o código mais simples que rode o teste;
* Refatore o código para remover a duplicação de dados;
* Caso necessário, escreva mais um teste ou refine o existente;
* Faça esses passos para toda a lista de tarefas.

## 3. Escrevendo o código de teste

### 3.1 Planejamento 

A classe que contém o código de teste será anotada com o intuito de indicar que a classe deve ser executada utilizando o Junit4 (ou mais recente):

`@RunWith(JUnit4.class)`

### 3.2 Anotações

#### 3.2.1 @Test

Os casos de teste são o coração de cada teste unitário, neles são implementadas toda a lógica necessária para verificar o resultado da execução. De maneira simplista, um teste se baseia em verificar se o resultado obtido é igual ao resultado esperado.

Cada método de teste deve ser anotado com a anotação **@Test** e não há restrição referente à nomenclatura:

~~~
@Test
public void metodoTeste() {
...
}
~~~

Por exemplo caso desejamos que nosso teste não demore mais que 500 milisegundos podemos realizar a seguinte anotação:

~~~
@Test(timeout = 500)
public void fastTestCase() {
    Assert.assertEquals(1500, calendar.getSize());
}
~~~

Nesta anotação podemos verificar se o método está retornando uma exception. Essa funcionalidade é muito importante por exemplo para sabermos se o sistema está realmente tratando exceções e/ou validando erros internos. Exemplo:

~~~
@Test(expected=NullPointerException.class)
public void testException(int input) {
    int month = 4;
    Assert.assertNotNull(calendar.getAllDays(month));
}
~~~

#### 3.2.2 @Ignore

Para ignorar um método de teste utilizamos a anotação:

~~~
@Ignore
@Test
public void testName() {
...
}
~~~

#### 3.2.3 @BeforeClass e @Before


Para determinar que um método vai ser executado antes dos demais métodos da classe de teste. 

Essa funcionalidade serve para que possamos antes de uma classe de teste por exemplo iniciar a conexão com o banco de dados, inicializar variaveis entre outras possibilidades. Exemplo:

~~~
@BeforeClass
public void setup() {
    dataBase = new DataBase();
   dataBaseConnection.open();
   dataBase.populate();
   list_name = new ArrayList<>();
   index = 0;
}
~~~

Em caso de métodos, utilizamos @Before. Essa funcionalidade serve por exemplo para que antes de um método possamos inicializar variaveis. Exemplo:

~~~
@Before
public void initialize() {
    list_name = new Calendar.getAllNames();
    index = 55;
}
~~~

#### 3.2.4 @AfterClass e @After

Essa funcionalidade serve para que possamos depois de uma classe de teste por exemplo fechar a conexão com o banco de dados, ajudar o garbage collection a limpar os dados ociosos entre outras possibilidades.

~~~
@AfterClass
public void close() {
    dataBase.drop();
    dataBaseConnection.close();
    dataBase = null;
    list_name = null;
    index = null;
}
~~~

Em caso de métodos, utilizamos @After. Essa funcionalidade serve por exemplo para que antes de um método possamos finalizar variaveis. Exemplo:

~~~
@After
public void finalize() {
    list_name = calendar.getAllNames();
    index = current_index;
}
~~~

Com ela podemos voltar o locale da JVM para seu estado inicial ao fim de cada teste.

#### 3.2.5 @RunWith

Uma suite de teste é basicamente uma classe que vai disparar a execução das demais classes de teste.
Abaixo exemplo de uma classe de suite de teste onde são descritos os testes a serem executados:

~~~
import org.junit.runner.RunWith;
import org.junit.runners.Suite;

@RunWith(Suite.class)
@Suite.Suite({
  TestLogin.class,
  TestLogout.class,
  TestCalendarNavigate.class,
  TestCalendarUpdate.class
})

public class CalendarTestSuite {
}
~~~

Na anotação RunWith indica a suite de teste e na segunda anotação @Suite.Suite é onde indicamos as classes de teste que serão executadas. 

Neste caso acima as classes TestLogin.class, TestLogout.class, TestCalendarNavigate.class e TestCalendarUpdate.class.

#### 3.2.6 @ClassnameFilters

há outra forma de disparar a execução de todos os testes. Com a anotação **@ClassnameFilters** definimos os padrões das classes de teste. Todas as classes de teste que atendem a esses padrões serão executadas.

~~~
import javax.naming.NamingException;
import org.junit.AfterClass;
import org.junit.BeforeClass;
import org.junit.extensions.cpsuite.ClasspathSuite;
import org.junit.extensions.cpsuite.ClasspathSuite.ClassnameFilters;
import org.junit.runner.RunWith;

@RunWith(Suite.class)
@ClassnameFilters({ ".*Test", ".*Teste" })
public class SuiteTest {
   @BeforeClass
    public static void setup() {
    }
    @AfterClass
    public static void close() {
    }
}
~~~

**Como está descrito acima então com a anotação “@ClassnameFilters({ “.*Test”, “.*Teste” })” as classes de teste contendo em seus nomes “Test” e “Teste” serão executadas automaticamente.**

#### 3.2.7 @Rule

O Junit 4.7 introduziu o conceito de Rules.

As Rules, de maneira geral, permitem adicionar comportamentos que serão executados antes e depois de cada método de teste.

~~~
public class TransferenciaBancariaServiceTest {
 
  private TransferenciaBancariaService service = new TransferenciaBancariaService();
 
 /*
  * Como se pode ver, a varíavel excecaoEsperada é inicializada com o o valor ExpectedException.none(); essa inicialização é   * para informar que, por padrão, nenhuma exceção é esperada.
  */
  
  @Rule
  public ExpectedException excecaoEsperada = ExpectedException.none();
 
  @Test
  public void transferenciaImpossivelSaldoInsuficienteDeveLancarExcecao() {
    ContaBancaria origem = new ContaBancaria("CONTA-A", BigDecimal.valueOf(1500l));
    ContaBancaria destino = new ContaBancaria("CONTA-B", BigDecimal.valueOf(500l));
 
 /*
  * excecaoEsperada.expect() – modifica o comportamento padrão definido anteriormente, informando qual o tipo de exceção       * esperamos: SaldoInsuficienteException;
  */
     excecaoEsperada.expect(SaldoInsuficienteException.class);
     
  /*
   * A última linha destacada nos permite verificar a mensagem da exceção (excecaoEsperada.expectMessage).
   */
    excecaoEsperada.expectMessage(String.format(SaldoInsuficienteException.SALDO_INSUFICIENTE_MSG, origem));
 
    service.transfere(origem, destino, BigDecimal.valueOf(2000l));
  }
 
}
~~~

### 3.3 Assert

A classe Assert contém os métodos mais comuns utilizados na escrita nos casos de teste: 

* assertEquals; 
* assertNotNull; 
* assertNull; 
* etc. 

O método **assertNotNull** verifica se o objeto não é nulo, o método **assertEquals** verifica se o resultado obtido é igual ao esperado e assim por diante. 

## 4. Execução

Com a classe de testes pronta, basta executar a classe no Eclipse, que contém integração nativa com JUnit. Com a classe aberta, acesse o menu Run > Run As > JUnit Test, seus testes serão executados e será exibido  o resultado.

Testes unitários são tão complicados quanto as unidades a serem testadas, mas acrescentam uma camada de segurança importante à aplicação. 

Qualquer alteração que gere impacto no funcionamento previsto será percebida rapidamente, dando possibilidade ao desenvolvedor de tomar as ações necessárias: seja corrigir a implementação ou atualizar os testes.


