# Developer Tools

## 1. Spring Boot DevTools

### 1.1. Configurações automáticas

O Spring-boot faz muitas configurações automáticas, incluindo a habilitação do cache por padrão para melhorar a performance. 

Um exemplo é o armazenamento em cache de templates usados pelos template engines. Contudo, durante o desenvolvimento, é mais importante ver as mudanças o mais rápido possível.

O comportamento padrão do armazenamento em cache pode ser desativado para o `thymeleaf` usando a propriedade `spring.thymeleaf.cache = false` no arquivo `application.properties`. Não precisamos fazer isso manualmente, a introdução do `pring-boot-devtools` faz isso automaticamente para nós.

### 1.2. Reinício automático

Em um ambiente típico de desenvolvimento de aplicativos, um desenvolvedor faz algumas alterações, builda o projeto e implanta/inicia o aplicativo para que novas alterações entrem em vigor, ou então tenta aproveitar o JRebel etc.

Usando o `spring-boot-devtools`, esse processo também é automatizado. 

Sempre que os arquivos mudam no `classpath`, os aplicativos que usam `spring-boot-devtools` fazem com que o aplicativo reinicie. 

O benefício desse recurso é o tempo necessário para verificar se as alterações feitas são consideravelmente reduzidas. 

### 1.3. Live Reload

O módulo `spring-boot-devtools` inclui um servidor `LiveReload` incorporado que é usado para acionar uma atualização do navegador quando um recurso é alterado. 

Para que isso aconteça no navegador, precisamos instalar o plug-in `LiveReload`. Uma dessas implementações é o Remote Live Reload for Chrome.

### 1.4. Configurações Globais

O spring-boot-devtools fornece uma maneira de definir configurações globais que não são acopladas a nenhum aplicativo. Este arquivo é nomeado como .spring-boot-devtools.properties e está localizado em $ HOME.

### 1.5. Aplicações remotas

O `spring-boot-devtools` fornece recursos prontos para depuração remota via HTTP. Para ter esse recurso, é necessário que o `spring-boot-devtools` seja empacotado como parte do aplicativo. Isso pode ser conseguido desativando a configuração `excludeDevtools` no plug-in no maven.

~~~
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
            <configuration>
                <excludeDevtools>false</excludeDevtools>
            </configuration>
        </plugin>
    </plugins>
</build>
~~~

Agora, para que a depuração remota via HTTP funcione, é necessário executar as seguintes etapas: 

1. Um aplicativo vai para deploy e que é iniciado no servidor deve ser iniciado com a Depuração Remota ativada: 

`-Xdebug -Xrunjdwp: server = y, transport = dt_socket, suspend = n` 

Como podemos ver, a porta de depuração remota não é mencionada aqui. Portanto, o java escolherá uma porta aleatória.  

2. Para o mesmo projeto, abra as Configurações de inicialização, escolha as seguintes opções: 

* Selecione a classe principal: `org.springframework.boot.devtools.RemoteSpringApplication`. 
* Nos argumentos do programa, adicione a URL do aplicativo: `http: // localhost: 8080` 

3. A porta padrão para o depurador via spring-boot é 8000 e pode ser substituída por: 

`spring.devtools.remote.debug.local-port = 8010`. 

4. Crie uma configuração de depuração remota, setando a porta 8010 conforme configurado por meio de propriedades ou 8000.

### 1.6. Atualização remota

O cliente remoto monitora o `classpath` do aplicativo em busca de alterações. Como é feito no recurso de reinicialização remota. 

Qualquer alteração no `classpath` implica no envio do recurso atualizado ao aplicativo remoto e uma reinicialização é acionada. 

As alterações são enviadas quando o cliente remoto está em funcionamento, pois o monitoramento de arquivos alterados só é possível nesse caso. 

## 2. Lombok

O Lombok é uma biblioteca Java focada em produtividade e redução de código boilerplate que por meio de anotações adicionadas ao nosso código ensinamos o compilador (maven ou gradle) durante o processo de compilação a criar código Java.

> Boilerplate se refere a seções de código que devem ser incluídas em muitos lugares com pouca ou nenhuma alteração.

**Na primeira vez, deve-se encontrar o jar do lombok, baixado pela dependência maven e rodá-lo.**

Nunca mais escreva outro método getter, setter, equals, builder e etc.

### 2.1. @Getters, @Setters, @NoArgsConstructor e @AllArgsConstrutor

Para o projeto em questão, serão necessárias: 

~~~
<dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>

<dependency>
        <groupId>com.h2database</groupId>
        <artifactId>h2</artifactId>
        <scope>runtime</scope>
</dependency>
~~~


Imagine que queremos usar a classe `User` como uma entidade JPA, logo teríamos o seguinte código:

~~~
@Entity
public class User {
 
    @Id @GeneratedValue
    private Long id; 
    private String firstName;
    private String lastName;
    private String email;
    private Date age;
    private String gender;
 
    public User() {}
 
    public User(String firstName, String lastName, String email, date age, String gender) {
        this.firstName = firstName;
        this.lastName = lastName;
        this.email = email;
        this.age = age;
        this.gender = gender;
    }
    // getters and setters
    ...
}
~~~ 

Agora com o Lombok: 

~~~
@Entity
@Getter @Setter @NoArgsConstructor
public class User {
 
    @Id @GeneratedValue
    private Long id; 
    private String firstName;
    private String lastName;
    private String email;
    private Date age;
    private String gender;
 
    public User(String firstName, String lastName, String email, Date age, String gender) {
        this.firstName = firstName;
        this.lastName = lastName;
        this.email = email;
        this.age = age;
        this.gender = gender;
    }
 }
~~~

Adicionando as anotações `@Getter` e `@Setter` no topo da classe, dissemos ao Lombok que crie os métodos para todos os atributos da classe. Para criar um construtor vazio usamos a anotação `@NoArgsConstructor` e `@AllArgsConstructor` para o construtor completo.

Todavia sabemos que não é uma boa prática criar getter e setter para todos os nossos atributos, um bom exemplo é o `id` com a anotação `@GeneratedValue`.

Simplesmente removemos as anotações `@Getter` e `@Setter` do topo da classe e adicionamos na linha de cada atributo separadamente, note que somente o atributo `id` está sem uma anotação `@Setter`.

~~~ 
@Entity
@NoArgsConstructor @AllArgsConstructor
public class User {
 
    @Id @GeneratedValue
    @Getter private Long id; 
    @Getter @Setter private String firstName;
    @Getter @Setter private String lastName;
    @Getter @Setter private String email;
    @Getter @Setter private Date age;
    @Getter @Setter private String gender;
 }
 ~~~

### 2.2. @ToString

Você pode usar essa anotação em qualquer classe e vai ser gerado um método toString(). Por padrão ele vai retornar o nome da sua classe, juntamente com cada campo, em ordem e separados por vírgulas.

Caso você queria ignorar alguns campos, basta passa-los no parâmetro exclude ou você também pode especificar exatamente quais os campos deseja usar no parâmetro `of`.

~~~
@Entity
@NoArgsConstructor @AllArgsConstructor 
@ToString(exclude="id")
public class User {
 
    @Id @GeneratedValue
    @Getter private Long id; 
    @Getter @Setter private String firstName;
    @Getter @Setter private String lastName;
    @Getter @Setter private String email;
    @Getter @Setter private Date age;
    @Getter @Setter private String gender;
}
~~~ 

### 2.3. @EqualsAndHashCode

Assim como o `@ToString` qualquer classe pode ser anotada com `@EqualsAndHashCode` e vai gerar os métodos equals() e hashCode() por padrão ele usará todos os campos não estáticos e não transientes.

E você também pode ignorar alguns campos no parâmetro exclude ou você também pode especificar exatamente quais os campos deseja usar, no parâmetro `of`.

~~~
@Entity
@NoArgsConstructor @AllArgsConstructor 
@EqualsAndHashCode(exclude={"firstName", "lastName", "gender"})
public class User {
 
    @Id @GeneratedValue
    @Getter private Long id; 
    @Getter @Setter private String firstName;
    @Getter @Setter private String lastName;
    @Getter @Setter private String email;
    @Getter @Setter private Date age;
    @Getter @Setter private String gender;
}
~~~ 

### 2.4. Logger

A anotação @Slf4j pode ser substituída por outras bibliotecas de log como por exemplo: @Log ou @CommonsLog.

~~~
@Slf4j
public class UserService {
   // log.debug(), log.info(), ...
}
~~~

### 2.5. Resumo: 

| Anotação | Descrição |
|--|--|
| @Getter/@Setter|Com estas anotações não se faz mais necessária a criação dos métodos de recuperação e configuração das propriedades das classes.   |
| @ToString |  Não há mais necessidade de iniciar um debugger para ver os campos. Basta deixar que o lombok gere o toString()
| @EqualsAndHashCode | Método equals e hashCode são gerados automaticamente para os campos do objeto de forma fácil e simples
| @Data | Todos juntos agora: Um atalho para @ToString, @EqualsAndHashCode,@Getter em todos os campos, e @Setter em todos os campos não-finais. Você ainda pode obter um construtor livre para inicializar seus campos finals!
| @Cleanup |  Gestão de recursos automática: Chame com segurança os métodos close()sem problemas.
| @Synchronized | synchronized’s corretos. Não exponha seus locks.
| @SneakThrows | Para lançar exceções onde antes não se era comum lançar.

## 3. Spring Configuration Processor

A maioria dos aplicativos em que trabalhamos como desenvolvedores deve ser configurável até certo ponto. 

No entanto, geralmente, nós realmente não entendemos o que um parâmetro de configuração faz, se ele tem um valor padrão, se está obsoleto e, às vezes, nem sabemos que a propriedade existe.

Para nos ajudar, o Spring Boot gera metadados de configuração em um arquivo JSON, que fornece informações úteis sobre como usar as propriedades. Portanto, os metadados da configuração são um arquivo descritivo que contém as informações necessárias para a interação com as propriedades da configuração.

O mais legal desse arquivo é que os IDEs também podem lê-lo, fornecendo um preenchimento automático das propriedades do Spring, além de outras dicas de configuração.

Para ver o processador em ação, vamos imaginar que temos algumas propriedades que precisamos incluir em nosso aplicativo Spring Boot por meio de um bean Java:

~~~
@Configuration
@ConfigurationProperties(prefix = "database")
public class DatabaseProperties {
     
    public static class Server {
 
        private String ip;
        private int port;
 
        // standard getters and setters
    }
     
    private String username;
    private String password;
    private Server server;
     
    // standard getters and setters
}
~~~

Para fazer isso, usamos a anotação `@ConfigurationProperties` . O processador de configuração procura classes e métodos com esta anotação para acessar os parâmetros de configuração e gerar metadados de configuração.

Vamos adicionar algumas dessas propriedades em um arquivo de propriedades. Nesse caso, chamaremos de `databaseproperties-test.properties`: 

~~~
#Simple Properties
database.username=luis
database.password=password
~~~

Depois de compilar nosso projeto, veremos um arquivo chamado `spring-configuration-metadata.json` dentro de `target/ classes/META-INF`:

~~~
{
  "groups": [
    {
      "name": "database",
      "type": "com.baeldung.autoconfiguration.annotationprocessor.DatabaseProperties",
      "sourceType": "com.baeldung.autoconfiguration.annotationprocessor.DatabaseProperties"
    },
    {
      "name": "database.server",
      "type": "com.baeldung.autoconfiguration.annotationprocessor.DatabaseProperties$Server",
      "sourceType": "com.baeldung.autoconfiguration.annotationprocessor.DatabaseProperties",
      "sourceMethod": "getServer()"
    }
  ],
  "properties": [
    {
      "name": "database.password",
      "type": "java.lang.String",
      "sourceType": "com.baeldung.autoconfiguration.annotationprocessor.DatabaseProperties"
    },
    {
      "name": "database.server.ip",
      "type": "java.lang.String",
      "sourceType": "com.baeldung.autoconfiguration.annotationprocessor.DatabaseProperties$Server"
    },
    {
      "name": "database.server.port",
      "type": "java.lang.Integer",
      "sourceType": "com.baeldung.autoconfiguration.annotationprocessor.DatabaseProperties$Server",
      "defaultValue": 0
    },
    {
      "name": "database.username",
      "type": "java.lang.String",
      "sourceType": "com.baeldung.autoconfiguration.annotationprocessor.DatabaseProperties"
    }
  ],
  "hints": []
}
~~~

Vamos ver como a alteração das anotações em nossos Java beans afeta os metadados. 

* Primeiro, vamos adicionar comentários do JavaDoc no servidor.
* Segundo, vamos atribuir um valor padrão ao campo `database.server.port` e, finalmente, adicionar as anotações `@Min` e `@Max`:

~~~
public static class Server {
 
    /**
     * The IP of the database server
     */
    private String ip;
 
    /**
     * The Port of the database server.
     * The Default value is 443.
     * The allowed values are in the range 400-4000.
     */
    @Min(400)
    @Max(800)
    private int port = 443;
 
    // standard getters and setters
}
~~~

Se verificarmos o arquivo `spring-configuration-metadata.json` agora, veremos essas informações extras refletidas:

~~~
{
  "groups": [
    {
      "name": "database",
      "type": "com.baeldung.autoconfiguration.annotationprocessor.DatabaseProperties",
      "sourceType": "com.baeldung.autoconfiguration.annotationprocessor.DatabaseProperties"
    },
    {
      "name": "database.server",
      "type": "com.baeldung.autoconfiguration.annotationprocessor.DatabaseProperties$Server",
      "sourceType": "com.baeldung.autoconfiguration.annotationprocessor.DatabaseProperties",
      "sourceMethod": "getServer()"
    }
  ],
  "properties": [
    {
      "name": "database.password",
      "type": "java.lang.String",
      "sourceType": "com.baeldung.autoconfiguration.annotationprocessor.DatabaseProperties"
    },
    {
      "name": "database.server.ip",
      "type": "java.lang.String",
      "description": "The IP of the database server",
      "sourceType": "com.baeldung.autoconfiguration.annotationprocessor.DatabaseProperties$Server"
    },
    {
      "name": "database.server.port",
      "type": "java.lang.Integer",
      "description": "The Port of the database server. The Default value is 443.
        The allowed values are in the range 400-4000",
      "sourceType": "com.baeldung.autoconfiguration.annotationprocessor.DatabaseProperties$Server",
      "defaultValue": 443
    },
    {
      "name": "database.username",
      "type": "java.lang.String",
      "sourceType": "com.baeldung.autoconfiguration.annotationprocessor.DatabaseProperties"
    }
  ],
  "hints": []
}
~~~ 

| Informação | Descrição |
|--|--|
|Grupos  | São itens de nível superior usados ​​para agrupar outras propriedades, sem especificar um valor em si. Em nosso exemplo, temos o grupo de _banco de dados_ , que também é o prefixo das propriedades de configuração. Também temos um grupo de _servidores_ , que criamos por meio de uma classe interna e agrupa propriedades de _ip_ e _porta_ |
| Propriedades |  São itens de configuração para os quais podemos especificar um valor. Essas propriedades são definidas nos arquivos _.properties_ ou _.yml_ e podem ter informações extras, como valores e validações padrão, como vimos no exemplo acima. |
| Dicas |  São informações adicionais para ajudar o usuário a definir o valor da propriedade. Por exemplo, se tivermos um conjunto de valores permitidos para uma propriedade, podemos fornecer uma descrição do que cada um deles faz. O IDE fornecerá ajuda de competição automática para essas dicas. |
