# Annotations

Spring Boot facilitou a configuração do Spring com seu recurso de configuração automática.

Seguem a lista de anotações e formas de uso. 

## 1. @SpringBootApplication

É uma combinação das 3 anotações: 

|Anotação| Descrição  |
|:--:|--|
| `@Configuration` | Marca a classe (tag) como um source de definições de bean para o contexto do aplicativo.  |
| `@EnableAutoConfiguration` |  Diz ao Spring Boot para começar a adicionar beans com base nas configurações do classpath, outros beans e outras configurações de propriedades. Por exemplo, se spring-webmvc estiver no classpath, essa anotação sinaliza o aplicativo como um aplicativo da Web e ativa os principais comportamentos, como configurar a DispatcherServlet.|
| `@ComponentScan` | Diz ao Spring que procure outros componentes, configurações e serviços no package, permitindo que ele encontre os controladores. |

Usamos esta anotação para marcar a classe principal de um aplicativo Spring Boot

~~~
package com.example.servingwebcontent;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class ServingWebContentApplication {

    public static void main(String[] args) {
        SpringApplication.run(ServingWebContentApplication.class, args);
    }

}
~~~ 

O main() usa o método do Spring Boot **SpringApplication.run()** para iniciar um aplicativo. Você notou que não havia uma única linha de XML? 

Também não há um arquivo `web.xml`. Esse aplicativo da Web é 100% Java e não foi preciso configurar nenhuma infraestrutura.

### 1.1. @Configuration

Esta anotação é usada em classes que definem beans. `@Configuration` é um análogo para o arquivo de configuração XML. A classe Java anotada com `@Configuration` é uma configuração por si só e terá métodos para instanciar e configurar as dependências.

É uma annotation que indica que uma classe declara um ou mais métodos `@Bean` e pode ser processada pelo contêiner 
Spring para gerar definições de bean e solicitações de serviço para esses beans em tempo de execução, por exemplo:

~~~
@Configuration
public class DataConfig{ 
  @Bean
  public DataSource source(){
    DataSource source = new OracleDataSource();
    source.setURL();
    source.setUser();
    return source;
  }
  @Bean
  public PlatformTransactionManager manager(){
    PlatformTransactionManager manager = new BasicDataSourceTransactionManager();
    manager.setDataSource(source());
    return manager;
  }
~~~

#### 1.1.1. @Bean

Se @Configuration define um repositório de beans, em seu interior devemos incluir a anotação @Bean , que deve ser inserida apenas em funções.

Para que um bean exista são necessários três elementos: as configurações, o container e a classe que o implementa. 

No caso do Spring as configurações podem vir de três fontes: 
* XML; 
* anotações
* código Java. 

Anotação utilizada em cima dos métodos de uma classe, geralmente marcada com `@Configuration`, indicando que o Spring deve invocar aquele método e gerenciar o objeto retornado por ele. Isso significa que agora este objeto pode ser injetado em qualquer ponto da sua aplicação.

Para declarar um bean, simplesmente anote um método com a `@Bean`. Quando o JavaConfig encontra esse método, ele executa o método e registra o valor de retorno como um bean dentro da `BeanFactory`. 

Exemplo 1: 

~~~
import org.springframework.context.annotation.Configuration;
// Sem definir um nome explicitamente
@Configuration
public class JavaConfig {...}
~~~ 

* Aqui aplicamos a anotação sobre um método sem definir explicitamente o nome do bean. Nesta situação o nome do bean corresponderá ao nome do método que recebeu a anotação. 

Exemplo 2: 
~~~
// Definindo um nome explicitamente
@Configuration("configuracaoJava")
public class JavaConfig {...}
~~~ 

Vemos que é possível definir múltiplos nomes para um bean (aliases), que é o que fazemos no segundo exemplo da anotação, passando como parâmetro um array de strings contendo estes nomes. 

Exemplo 3: 
~~~
@Configuration
public class JavaConfig {
 
 @Bean
 public DAOUsuario daoUsuario() {
  return new DAOUsuario();
 }
 
 @Bean(name = {"daoProduto", "produtoDAO"})
 public DAOProduto criarDAOProduto() {
  return new DAOProduto();
 }
 
 @Bean(name = "datasource")
 public DataSource getDataSource() {
  DataSource ds = null;
  GregorianCalendar data = new GregorianCalendar();
  if (data.get(GregorianCalendar.HOUR_OF_DAY) < 13) {
   ds = new DataSourceUsuarios();
  } else {
   ds = new DataSource();
  }
  return ds;
 }
}
~~~

Como pode ser observado, tudo o que os dois primeiros métodos do nosso código anterior simplesmente criam uma nova instância do bean. O uso realmente interessante pode ser observado no terceiro caso em que usamos a hora corrente do sistema para escolher qual implementação deve ser instanciada.

### 1.2. @EnableAutoConfiguration

A configuração automática do Spring Boot tenta configurar automaticamente seu aplicativo Spring com base nas dependências do jar que você adicionou. Por exemplo, se HSQLDB estiver no seu **classpath** e você não tiver configurado manualmente nenhum bean de conexão com o banco de dados, o Spring Boot **configura automaticamente** um banco de dados na memória.

Outra Característica importante da anotação, é sua propriedade exclude, a qual você pode usar para definir as classes que você quer que não sofram configurações automáticas.

Exemplo: 
~~~
import org.springframework.boot.autoconfigure.*;
import org.springframework.boot.autoconfigure.jdbc.*;
import org.springframework.context.annotation.*;

@Configuration(proxyBeanMethods = false)
@EnableAutoConfiguration(exclude={DataSourceAutoConfiguration.class})
public class MyConfiguration {
}
~~~

Você precisa ativar a configuração automática adicionando as anotações `@EnableAutoConfiguration` ou `@SpringBootApplication` a uma de suas classes marcadass por `@Configuration`.

A configuração automática geralmente é aplicada com base no classpath e nos beans definidos. Portanto, não precisamos definir nenhum DataSource, EntityManagerFactory, TransactionManager etc. O Spring Boot cria automaticamente beans apropriados e os registra para você. 
 
### 1.3. @ComponentScan

Se você entende `@ComponentScan`, entende o Spring. Spring é um framework sobre injeção de dependência. 

A primeira etapa da definição do Spring Beans é adicionar a anotação correta - @Component ou @Service ou @Repository.

No entanto, o Spring não sabe sobre o bean, a menos que saiba onde procurá-lo.

A anotação `@ComponentScan` é usada com a anotação `@Configuration` para avisar ao Spring quais são os pacotes em que ele deve procurar componentes anotados. 

Ela também é usada para especificar pacotes e classes base usando os atributos: `basePackageClasses` ou `basePackages`.

O atributo `basePackageClasses` é uma alternativa segura para o tipo `basePackages`. Quando você especifica `basePackageClasses`, o Spring verifica o pacote (e subpacotes) das classes especificadas.

Exemplo:

~~~
package com.atalhox;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ApplicationContext;
import org.springframework.context.ConfigurableApplicationContext;

@SpringBootApplication
public class SpringBootExample {

	public static void main(String[] args) {
		ApplicationContext applicationContext = 
				SpringApplication.run(SpringBootExample.class, args);
		
		for (String name : applicationContext.getBeanDefinitionNames()) {
			System.out.println(name);
		}
	}
}
~~~ 

## 2. @Component e derivados

A annotation básica que indica que uma classe vai ser gerenciada pelo container do Spring.

|Anotação| Descrição  |
|:--:|--|
| `@Component` | é um estereótipo genérico para qualquer componente gerenciado pelo Spring.  |
| `@Repository` |  anota classes na camada de persistência, que atuará como um repositório de banco de dados.|
| `@Service` | faz anotações de classes na camada de serviço.  |
| `@Controller"` | usado principalmente com aplicativos da web ou serviços da web REST para especificar que a classe é um controlador frontal e responsável por lidar com a solicitação do usuário e retornar a resposta apropriada.  |

### 2.1. @Component

Serve para indicar ao framework que aquela classe é um bean que deverá ser administrado pela implementação de IoC Container do Spring.

Quando uma classe é anotada com `@Component` significa que a mesma usará o padrão de injeção de depêndencia, e será elegível para **auto-configuração** e **auto-detecção** de beans anotados à partir de escaneamento do classpath que o IoC Container do Spring faz.

>Spring IoC: é um container que faz a função `new` para nossos objetos e também sabe resolver e ligar as dependências. Por isso, o Spring também é chamado Container IoC (Inversion of Control)

~~~
@Component("processador")
public class Processador {
...
}
~~~ 
Como pôde ser visto, ainda com anotações é possível nomear nossos beans passando como parâmetro sua identificação. Caso este valor esteja ausente, o nome do bean será definido pelo container automaticamente.

Ao carregar a aplicação, o Spring escanea o classpath atrás de classes anotadas com `@Component` ou especializações para então criar uma instância com escopo do tipo singleton por padrão, ou seja, os beans são stateless (não devem guardar estado), assim não sendo necessário uma nova instância do bean a cada vez que houver uma referência.

> **Singleton**: Padrão que garante a existência de apenas uma instância de
> uma classe, mantendo um ponto global de acesso ao seu objeto.
> 
> Quando você necessita de somente uma instância da classe, por exemplo,
> a conexão com banco de dados, vamos supor que você terá que chamar
> diversas vezes a conexão com o banco de dados em um código na mesma
> execução.
> 
> Se você instanciar toda vez a classe de banco, haverá grande
> perda de desempenho, assim usando o padrão singleton, é garantida que
> nesta execução será instanciada a classe somente uma vez.

### 2.2. @Repository

Esta anotação é usada em classes Java que acessam diretamente o banco de dados. A anotação `@Repository` funciona como marcador para qualquer classe que cumpre a função de repositório ou Objeto de Acesso a Dados (DAO).

`@Repository` possui um recurso de tradução automática. Por exemplo, quando ocorre uma exceção, existe um manipulador para essa exceção e não há necessidade de adicionar um bloco try catch.

Essa anotação é uma especialização da anotação `@Component`, portanto, as suas classes são detectadas automaticamente pela estrutura do Spring por meio da varredura do classpath.

O Spring Repository está muito próximo do padrão DAO, onde as classes DAO são responsáveis por fornecer operações CRUD nas tabelas do banco de dados. 

> **CRUD**: Trata-se das 4 operações básicas de SQL: 
> * create (insert); 
> * read (select); 
> * update; 
> * delete.

No entanto, se você estiver usando o Spring Data para gerenciar operações do banco de dados, deverá usar a interface do Spring Data Repository.

~~~ 
@Repository
public interface ClienteRepository extends JpaRepository<Cliente, Long> {
  
    public Cliente findByRg(String pRg);
    
    public Cliente findByRgAndNome (String pRg, String pNome);
  
}
~~~ 

Note que a implementação do `findByRg` fica a cargo do Spring Boot! Todos os atributos mapeados na entidade podem ser usados. 

A entidade `Cliente` tem um atributo `rg`, por isso quando for criado o `findByRg` o Spring sabe exatamente qual atributo usar na query.

### 2.3. @Service

Esta anotação é usada em uma classe. O `@Service` marca uma classe Java que executa algum serviço, como executar lógica de negócios, executar cálculos e chamar APIs externas. 

Esta anotação é uma forma especializada da anotação `@Component` destinada a ser usada na camada de serviço.

Por exemplo, um fluxo de finalização de compra envolve atualizar manipular o carrinho, enviar email, processar pagamento etc. Este é o típico código que temos dificuldade de saber onde vamos colocar, em geral ele pode ficar num Service.

### 2.4. @Controller

A anotação `@Controller` é usada para indicar que a classe é um controlador Spring. 

Esta anotação pode ser usada para identificar controladores para Spring MVC ou Spring WebFlux e é associada com classes que possuem métodos que processam requests numa aplicação web.

Um Controller é responsável tanto por receber requisições como por enviar a resposta ao usuário. 

O Controller se responsabiliza por informar a View, os atributos que serão visíveis para a mesma e também por receber parâmetros vindos da View. E, por último, responder ao usuário o que foi requisitado. 

Veja como é simples criar um Controller, mas veja que este não possui nenhum “mapping” atrelado a ele. Então criemos uma **view (.jsp)** chamada `home.jsp` dentro da pasta `/WEB-INF/views` e criaremos o mapping `/home` para exibir a view criada.

Exemplo 1: 
~~~
//Define que minha classe será um controller
@Controller 
public class HomeController {
    
    //Define a url que quando for requisitada chamara o metodo
    @RequestMapping("/home") 
    public ModelAndView home(){
        //Retorna a view que deve ser chamada, no caso home (home.jsp) aqui o .jsp é omitido
        return new ModelAndView("home");
    }
} 
~~~

Exemplo 2: 
~~~
@Controller
@RequestMapping("/welcome")
public class WelcomeController{
  @RequestMapping(method = RequestMethod.GET)
  public String welcomeAll(){
    return "welcome all";
  }  
}
~~~

Neste exemplo, apenas solicitações `GET` para `/welcome` são tratadas pelo método `welcomeAll( )`.

Exemplo 3: 

~~~ 
package com.example.servingwebcontent;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;

@Controller
public class GreetingController {

	@GetMapping("/greeting")
	public String greeting(@RequestParam(name="name", required=false, defaultValue="World") String name, Model model) {
		model.addAttribute("name", name);
		return "greeting";
	}

}
~~~ 

**Fluxo de processos**: 

1. `GreetingController`lida com GET requests para `/greeting` retornando o nome da `View` (nesse caso, greeting). A `View` é responsável por renderizar o conteúdo HTML. 

2. A `@GetMapping` garante que as solicitações HTTP GET `/greeting` sejam mapeadas para o método `greeting()`

3. `@RequestParam` liga o valor do parâmetro string das queries `name` ao parâmetro `name` do método `greeting()`. 

>Este String query não é obrigatório. Se estiver ausente na solicitação, o valor padrão `World` é usado. O valor do parâmetro `name` é adicionado a um objeto `Model`, tornando-o acessível ao template de visualização.

A implementação do corpo do método depende de uma tecnologia de exibição (Thymeleaf, etc.) para executar a renderização do HTML no lado do servidor. 

O Thymeleaf analisa o template `greeting.html` e avalia a expressão `th:text` (HTML) para renderizar o valor do `${name}` parâmetro que foi definido no controlador.

Template `Greeting.html`: 

~~~
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Getting Started: Serving Web Content</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
</head>
<body>
    <p th:text="'Hello, ' + ${name} + '!'" />
</body>
</html>
~~~

O template deverá ficar **por padrão** na pasta `src/main/resources/templates` 

#### 2.4.1. @RestController

É uma especialização de `@Controller`. 

Quando vamos chamar uma API REST, queremos que a sua resposta seja serializada, seja em JSON, XML, etc.  

Caso fosse usado o `@Controller` para tratarmos estes dados, precisaríamos sempre colocar `@ResponseBody`, tornando o código verboso. Por isso foi criado o `@RestController`. 

## 3. @RequestMapping

Geralmente utilizada em cima dos métodos de uma classe anotada com `@Controller`. Serve para você colocar os endereços da sua aplicação que, quando acessados por algum cliente, deverão ser direcionados para o determinado método.

A anotação `@RequestMapping` é usada para mapear URLs como www.DNS_da_aplicação/cliente para toda uma classe ou para um método manipulador particular. 

Normalmente, a anotação de nível de classe mapeia um caminho de requisições específico em um controlador de formulário, com anotações adicionais em nível de método, estreitando o mapeamento primário para um método específico de solicitação HTTP ("GET", "POST", etc.) ou uma condição de parâmetro de solicitação HTTP.

A anotação `@Controller` indica que a classe Cliente é um controlador do Spring MVC. Dessa forma, o DispatcherServlet poderá encaminhar requisições de usuário para serem manipuladas nesta classe.

A anotação `@RequestMapping` indica que o controlador, neste caso, a classe Cliente, receberá as requisições feitas à URL www.DNS_da_aplicação/cliente. 

~~~
package com.atalhox;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
  
@Controller
@RequestMapping(value = "/cliente")
public class Cliente {
  
    @RequestMapping(method = RequestMethod.GET)
    public String exibeTodosOsClientes(Model uiModel) {
        // ...
        return "pagina";
    }
  
    @RequestMapping(method = RequestMethod.POST)
    public String persisteNovoCliente(Model uiModel) {
        // ...
        return "pagina";
    }
}
~~~

O método `exibeTodosOsClientes` também está anotado com a anotação `@RequestMapping`, indicando que esse método irá receber as requisições feitas a URL www.DNS_da_aplicação/cliente sempre que se tratar de uma requisição HTTP GET.

Por sua vez, o método `persisteNovoCliente` receberá as requisições feitas a URL www.DNS_da_aplicação/cliente usando o método POST. 

Esse critério é definido através do uso do parâmetro method da anotação `@RequestMapping`. 

Um método mapeado com a anotação `@RequestMapping` deverá ter algum retorno que, por sua vez, será exibido ao usuário. 

Esse retorno pode ser de vários formatos: 

* uma página de hipertexto; 
* XML; 
* JSON; 
* JPEG; 
* PDF;
* etc. 

Quando se trata de páginas que serão exibidas ao usuário, estas deverão ser tratadas por algum `ViewResolver`.

## 4. @RequestParam

A anotação `@RequestParam` é usada para acessar os valores dos parâmetros de `request`. Veja o seguinte URL de solicitação:

`http://localhost:8080/springmvc/hello/101?param1=10&param2=20` 

Na solicitação de URL acima, os valores para param1 e param2 podem ser acessados ​​como abaixo:

~~~ 
public String getDetails(
    @RequestParam(value="param1", required=true) String param1,
        @RequestParam(value="param2", required=false) String param2){
...
}
~~~ 

A seguir, é apresentada a lista de parâmetros suportados pela anotação `@RequestParam`:

* defaultValue - este é o valor padrão como um mecanismo de fallback, se a solicitação não estiver com o valor ou estiver vazio.
* name - nome do parâmetro a ser vinculado.
* required - se o parâmetro é obrigatório ou não. Se for verdade, a falha no envio desse parâmetro falhará.
* value - Este é um alias para o atributo name.

## 5. @ResponseBody

Utilizada em métodos anotados com @RequestMapping para indicar que o retorno do método deve ser automaticamente escrito na resposta para o cliente. Muito comum quando queremos retornar JSON ou XML em função de algum objeto da aplicação.

A anotação significa é que o valor retornado do método constituirá o corpo da resposta HTTP. 

Obviamente, uma resposta HTTP não pode conter objetos Java. Portanto, o retorno é transformado em um formato adequado para aplicativos REST, geralmente JSON ou XML. 

A escolha do formato depende dos conversores de mensagens instalados, dos valores do atributo produzidos da anotação RequestMapping e do tipo de conteúdo que o cliente aceita (que está disponível nos cabeçalhos de solicitação HTTP. 

Por exemplo, se a solicitação indicar que aceita XML, mas não JSON, e houver um conversor de mensagens instalado que possa transformar a lista em XML, o XML será retornado.

~~~
@RequestMapping(value="/orders", method=RequestMethod.GET)
@ResponseBody
public List<Account> accountSummary() {
    return accountManager.getAllAccounts();
}
~~~ 

## 6. @Value

A anotação Spring @Value é usada para atribuir valores padrão a variáveis e argumentos de métodos. Podemos ler variáveis de ambiente, bem como variáveis de sistema usando a anotação `@Value`.

### 6.1. Valor padrão

A anotação `@Value` pode ser para atribuir os valores booleano e inteiro às variáveis: 

~~~ 
@Value("true")
private boolean defaultBoolean;

@Value("10")
private int defaultInt;
~~~ 

### 6.2. Variáveis de ambiente - Spring

Se a chave não for encontrada nas propriedades do ambiente, o valor da propriedade será ${APP_NAME_NOT_FOUND}.

~~~
@Value("${APP_NAME_NOT_FOUND}")
private String defaultAppName;
~~~ 

Podemos atribuir um valor padrão que será atribuído se a chave estiver ausente nas propriedades do ambiente.

~~~
@Value("${APP_NAME_NOT_FOUND:Default}")
private String defaultAppName;
~~~ 

### 6.3.Variáveis de ambiente - Sistema

Quando o ambiente Spring é preenchido, ele lê todas as variáveis de ambiente do sistema e as armazena como propriedades. Portanto, também podemos atribuir variáveis do sistema usando a anotação `@Value`.

~~~
@Value("${java.home}")
private String javaHome;
	
@Value("${HOME}")
private String homeDir;
~~~

### 6.4. Vários argumentos 

Quando a anotação `@Value` é encontrada em um método, o contexto do Spring invocará quando todas as configurações e beans do spring forem carregados. 

Se o método tiver vários argumentos, todos os valores de argumentos serão mapeados a partir da anotação do método. Se queremos valores diferentes para argumentos diferentes, podemos usar a anotação `@Value` diretamente no argumento.

~~~ 
@Value("Teste")
public void printValues(String s, String v){} //Tanto 's' e 'v' serão 'Teste'
~~~ 

~~~
@Value("Teste")
public void printValues(String s, @Value("Data") String v){}
// s=Teste, v=Data
~~~

## 7. @Autowired

A vantagem óbvia por trás do autowiring é a redução da configuração. O ganho oculto é a evolução natural e automática de nossa configuração em tempo de desenvolvimento, visto que o programador não precisa atualizar constantemente seus arquivos XML conforme progride no processo de criação do seu código.

A principal limitação da técnica é a substituição do explícito pelo implícito. Até então sempre tínhamos certeza de como seria feita a injeção de dependências em nossos beans pois o fazíamos manualmente. 

A partir do momento em que adotamos o autowiring delegamos esta responsabilidade ao container. 

Em projetos nos quais o número de beans seja pequeno e o número de candidatos a serem injetados
seja o aceitável o ganho de produtividade é garantido, mas conforme o projeto evolui e o número de candidatos aumenta o desenvolvedor se verá constantemente precisando excluir um ou outro candidato e, ainda pior, acabará voltando para o modo manual de configuração. 

Na esmagadora maioria dos casos os erros serão detectados em tempo de desenvolvimento, pois o container lançará uma exceção do tipo org.springframework.beans.factory.UnsatisfiedDependencyException. 

É importante salientar que há a possibilidade de erros sutis, em tempo de execução, decorrentes da injeção equivocada de um bean ou outro pelo container.

Outra limitação do autowiring é o fato deste não injetar automaticamente propriedades do tipo primitivo, listas ou strings. 

Nestes casos o desenvolvedor deve definir seus valores explicitamente sempre, mesmo porque não há como o container adivinhar seus valores.

A regra de ouro na adoção do autowiring é usá-lo apenas em projetos pequenos ou, no caso de projetos maiores, naqueles em que sejam definidas convenções rígidas bem divulgadas e adotadas por toda a equipe de desenvolvimento.

Depois que a injeção de anotações é ativada, a anotação pode ser usada em: 

* propriedades; 
* setters; 
* construtores.

### 7.1. Injeção em Propriedades

A anotação pode ser usada diretamente nas propriedades, **eliminando a necessidade de getters e setters**:

Classe `FooFormatter`: 

~~~
@Component("fooFormatter")
public class FooFormatter {
 
    public String format() {
        return "foo";
    }
}
~~~

Classe `FooService`: 
~~~ 
@Component
public class FooService {
     
    @Autowired
    private FooFormatter fooFormatter; 
}
~~~

No exemplo acima, o Spring procura e injeta `fooFormatter` quando `FooService` é criado.

### 7.2. Injeção em Setters

A anotação `@Autowired` pode ser usada nos métodos do setter. Quando a anotação é usada no método setter, ele é chamado com a **instância** de `FooFormatter` quando `FooService` é criado. 

~~~
public class FooService {
 
    private FooFormatter fooFormatter;
 
    @Autowired
    public void setFooFormatter(FooFormatter fooFormatter) {
            this.fooFormatter = fooFormatter;
    }
}
~~~

### 7.3. Injeção em Construtores

A anotação `@Autowired` também pode ser usada em construtores. No exemplo abaixo, quando a anotação é usada em um construtor, uma instância do `FooFormatter` é injetada como argumento no construtor quando o `FooService` é criado:

~~~
public class FooService {
 
    private FooFormatter fooFormatter;
 
    @Autowired
    public FooService(FooFormatter fooFormatter) {
        this.fooFormatter = fooFormatter;
    }
}
~~~

### 7.4. @Qualifiers

Por padrão, o Spring resolve entradas `@Autowired` por tipo. Se mais de um bean do mesmo tipo estiver disponível no contêiner, a estrutura lançará uma exceção, indicando que mais de um bean está disponível para Autowiring.

Classes implementando Formatter: 

~~~
@Component("fooFormatter")
public class FooFormatter implements Formatter {
 
    public String format() {
        return "foo";
    }
}
~~~

~~~ 
@Component("barFormatter")
public class BarFormatter implements Formatter {
 
    public String format() {
        return "bar";
    }
}
~~~ 

Classe `FooService` qualificando `Formatter formatter` com `fooFormatter`: 

~~~
public class FooService {
    @Autowired
    @Qualifier("fooFormatter")
    private Formatter formatter;
}
~~~ 

## 8. @Scope

Annotation utilizada para marcar o tempo de vida de um objeto gerenciado pelo container. 

Pode ser utilizada em classes anotadas com `@Component`, ou alguma de suas derivações. Além disso também pode usada em métodos anotados com `@Bean`. 

Quando você não utiliza nenhuma, o escopo default do objeto é o de aplicação, o que significa que vai existir apenas uma instância dele durante a execução do programa. 

Existem 6 tipos de Escopos definidos: 

|Scope| Descrição  |
|:--:|--|
| `singleton` | Contêiner cria uma única instância desse bean, e todas as solicitações para esse nome de bean retornarão o mesmo objeto, que é armazenado em cache. Quaisquer modificações no objeto serão refletidas em todas as referências ao bean. Esse escopo é o valor padrão se nenhum outro escopo for especificado. |
| `prototype` | Um bean com escopo de protótipo retornará uma **instância diferente toda vez** que for solicitada do contêiner. É definido configurando o protótipo de valor para a anotação `@Scope` na definição de bean. |
| `requests` | O escopo requests cria uma instância de bean para uma única solicitação HTTP. |
| `session` | O escopo session cria uma instância de bean para uma Sessão HTTP. |
| `application` | O escopo do aplicativo cria a instância do bean para o ciclo de vida de um ServletContext.  |
| `websocket` |  O escopo do websocket para uma sessão específica do WebSocket . |

Assim como na configuração XML convencional, caso seja omitido o escopo de um bean será adotado o padrão singleton.

### 8.1. Singleton

Trata-se do escopo padrão aplicado pelo Spring. Garante que apenas uma instância do bean seja instanciada pelo container e compartilhada por todos os outros beans que a usem como dependência. É recomendada quando: 

* A construção do objeto é cara, como por exemplo um pool de conexões, o objeto SessionFactory do Hibernate ou o EntityManager do JPA. Nestes casos, é interessante manter a mesma instância do objeto compartilhada por todos os
objetos clientes do sistema, garantindo assim que sua instanciação não prejudique a performance do sistema como um todo.

* O estado do objeto pode ser compartilhado por mais de um objeto cliente sem problema ou então é interessante que o estado seja compartilhado por mais de um objeto.

~~~ 
public class Person {
    private String name;
 
    // standard constructor, getters and setters
}
~~~

~~~
@Bean
@Scope("singleton")
public Person personSingleton() {
    return new Person();
}
~~~ 

### 8.2. Prototype

O escopo prototype garante que toda vez que o container receba uma requisição por um bean uma nova instância seja criada. 

É normalmente adotado em situações nas quais o bean tenha curta duração. Seu uso, de acordo com as questões que apre sentamos acima se faz recomendado quando:

* A construção do objeto é barata;
* O seu estado não deve ser compartilhado por mais de uma classe cliente;
* O objeto seja útil por um curto espaço de tempo.

### 8.3. Requests

Para o ambiente web Spring nos oferece um escopo bastante interessante que é o request, que mantém uma instância do bean durante a existência de uma requisição.

### 8.4. Session

Para o ambiente web Spring nos oferece um escopo bastante interessante que é o session, que mantém uma instância do bean durante a existência de uma sessão de usuário.

### 8.5. Application

Este escopo é semelhante ao escopo singleton, mas há uma diferença muito importante em relação ao escopo do bean.

Quando os beans têm escopo no aplicativo, a mesma instância do bean é compartilhada entre vários aplicativos baseados em servlet em execução no mesmo ServletContext , enquanto os beans no escopo singleton têm escopo para apenas um único contexto de aplicativo.

### 8.6. Websocket

Os beans com escopo WebSocket quando acessados pela primeira vez são armazenados nos atributos de sessão do WebSocket. A mesma instância do bean é retornada sempre que esse bean é acessado durante toda a sessão do WebSocket.

Também podemos dizer que ele exibe comportamento singleton, mas limitado a apenas uma sessão WebSocket.

## 9. @Primary

Caso você tenha dois métodos anotados com @Bean e com ambos retornando o mesmo tipo de objeto, como o Spring vai saber qual dos dois injetar por default em algum ponto da sua aplicação? 

É para isso que serve a annotation `@Primary`. Indica qual é a opção padrão de injeção. Caso você não queira usar a padrão, pode recorrer a annotation `@Qualifier`.

## 10. @Profile

Indica em qual profile tal bean deve ser carregado. Muito comum quando você tem **classes que só devem ser carregadas em ambiente de dev ou de produção**. Essa eu utilizo bastante e acho uma ideia simples, mas super relevante dentro do Spring.

## 11. @EnableAsync

Essa aqui não é tão comum, mas muitas vezes você precisa ações no sistema em background(outra thread). Essa annotation deve ser colocada em alguma classe marcada com @Configuration, para que o Spring habilite o suporte a execução assíncrona.

## 12. @Async

Uma vez que seu projeto habilitou o uso de execução de métodos assíncronos com a @EnableAsync, você pode marcar qualquer método de um bean gerenciado do projeto com essa annotation. Quando tal método for invocado, o Spring vai garantir que a execução dele será em outra thread.
