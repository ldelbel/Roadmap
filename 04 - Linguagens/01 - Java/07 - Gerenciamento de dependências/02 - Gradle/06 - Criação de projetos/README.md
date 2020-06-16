# Criando um projeto

Começando de maneira simples, crie um `build.gradle` na `<pasta do projeto>`. Na primeira linha: 

`apply plugin: 'java'`

## 1. Build

Execute `gradle tasks` novamente e você verá novas tarefas incluídas na lista, incluindo tasks para buildar o projeto, criar JavaDoc e executar testes.

Você usará a tarefa de compilação gradle com frequência. Esta tarefa compila, testa e monta o código em um arquivo JAR. Você pode executá-lo assim:

`gradle build`
Após alguns segundos, `BUILD SUCCESSFUL` indica que a compilação foi concluída.

Para ver os resultados do esforço de construção, dê uma olhada na pasta de construção. Nele você encontrará vários diretórios, incluindo estas três pastas notáveis:

* Classes: Os arquivos `.class` compilados do projeto.
* Reports: Relatórios produzidos pela compilação (como relatórios de teste).
* Libs: Bibliotecas de projetos montadas (geralmente arquivos JAR e/ou WAR).

A pasta classes possui arquivos `.class` que são gerados a partir da compilação do código Java. 

Neste ponto, o projeto não possui nenhuma dependência de biblioteca, portanto, não há nada na pasta `dependency_cache`.

A pasta de `reports` deve conter um relatório da execução de testes unitários no projeto. Como o projeto ainda não possui testes unitários, esse relatório será irrelevante.

A pasta `libs` deve conter um arquivo JAR com o nome da pasta do projeto. 

# 2. Declarar dependências

A maioria dos aplicativos, no entanto, depende de bibliotecas externas para lidar com funcionalidades comuns e complexas.

Por exemplo, suponha que você deseja que o aplicativo imprima a data e a hora atuais. Você pode usar os recursos de data e hora nas bibliotecas Java nativas, mas pode tornar as coisas mais interessantes usando as bibliotecas Joda Time.

Crie um `HelloWorld.java` para ficar assim:

~~~
package hello;

import org.joda.time.LocalTime;

public class HelloWorld {
  public static void main(String[] args) {
    LocalTime currentTime = new LocalTime();
    System.out.println("The current local time is: " + currentTime);

    Greeter greeter = new Greeter();
    System.out.println(greeter.sayHello());
  }
}
~~~

Aqui, `HelloWorld` usa a `LocalTime` do `Joda Time` para obter e imprimir a hora atual.

Se você executasse o `build gradle`, a build falharia porque você não declarou o Joda Time como uma dependência de compilação na build.

Adicionando a biblioteca: 

~~~
repositories {
    mavenCentral()
}
~~~ 

O bloco `repositories` indica que a compilação deve resolver suas dependências no repositório do Maven Central. 

O Gradle se apóia fortemente em muitas convenções e instalações estabelecidas pela ferramenta de criação do Maven, incluindo a opção de usar o Maven Central como fonte de dependências da biblioteca.

Agora que estamos prontos para bibliotecas de terceiros, vamos declarar algumas.

~~~ 
sourceCompatibility = 1.8
targetCompatibility = 1.8

dependencies {
    compile "joda-time:joda-time:2.2"
    testCompile "junit:junit:4.12"
}
~~~ 

Com o bloco `dependencies`, você declara uma única dependência para o Joda Time. Especificamente, você está solicitando (lendo da direita para a esquerda) a versão 2.2 da biblioteca joda-time, no grupo joda-time.

Outra coisa a ser observada sobre essa dependência é que ela é uma dependência de `compilação`, indicando que deve estar disponível durante o tempo de compilação (e se você estava criando um arquivo WAR, incluído na pasta / WEB-INF / libs do WAR). 

Outros tipos notáveis de dependências incluem:

* `providedCompile`:  Dependências necessárias para compilar o código do projeto, mas isso será fornecido em tempo de execução por um contêiner executando o código (por exemplo, a API Java Servlet).

* `testCompile`: Dependências usadas para compilar e executar testes, mas não são necessárias para criar ou executar o código de tempo de execução do projeto.

Por fim, vamos especificar o nome do nosso artefato JAR.

~~~
jar {
    baseName = 'gs-gradle'
    version =  '0.1.0'
}
~~~

O bloco `jar` especifica como o arquivo JAR será nomeado. Nesse caso, ele será renderizado gs-gradle-0.1.0.jar.

Agora, se você executar `gradle build`, Gradle deverá resolver a dependência do Joda Time no repositório do Maven Central e a compilação será bem-sucedida.

# 3. Gradle Wrapper

O Wrapper Gradle é a maneira preferida de iniciar uma compilação Gradle que consiste em um script em lote para Windows e em um shell para OS X e Linux. 

Esses scripts permitem executar uma compilação Gradle sem exigir a instalação do Gradle no seu sistema. Isso costumava ser algo adicionado ao seu arquivo de construção, mas foi dobrado no Gradle, portanto não há mais necessidade. Em vez disso, você simplesmente usa o seguinte comando.

`gradle wrapper --gradle-version 2.13`

Após a conclusão desta tarefa, você notará alguns novos arquivos. Os dois scripts estão na pasta raiz, enquanto o  wrapper jar e os arquivos de propriedades foram adicionados a uma nova `gradle/wrapper`.

~~~
└── <project folder>
    └── gradlew
    └── gradlew.bat
    └── gradle
        └── wrapper
            └── gradle-wrapper.jar
            └── gradle-wrapper.properties
~~~

O Gradle Wrapper está disponível para a construção de seu projeto. Adicione-o ao seu sistema de controle de versão, e todos que clonarem seu projeto poderão construí-lo da mesma forma. 

Pode ser usado exatamente da mesma maneira que uma versão instalada do Gradle. Execute o script wrapper para executar a tarefa de construção, como você fez anteriormente:

`./gradlew build`

Na primeira vez em que você executa o wrapper para uma versão especificada do Gradle, ele baixa e armazena em cache os binários Gradle para essa versão. 

Os arquivos do Gradle Wrapper foram projetados para serem comprometidos com o controle de origem, para que qualquer pessoa possa criar o projeto sem precisar instalar e configurar uma versão específica do Gradle.

Nesta fase, você terá buildado seu código. Você pode ver os resultados aqui:

~~~ 
build
├── classes
│   └── main
│       └── hello
│           ├── Greeter.class
│           └── HelloWorld.class
├── dependency-cache
├── libs
│   └── gs-gradle-0.1.0.jar
└── tmp
    └── jar
        └── MANIFEST.MF
~~~

Estão incluídos os dois arquivos de classe esperados para `Greeter` e `HelloWorld`, assim como um arquivo JAR. 

~~~
$ jar tvf build / libs / gs-gradle-0.1.0.jar
  0 Sex May 30 16:02:32 CDT 2014 META-INF /
 25 Fri May 30 16:02:32 CDT 2014 META-INF / MANIFEST.MF
  0 Sex May 30 16:02:32 CDT 2014 Olá /
369 Sex 30 de maio 16:02:32 CDT 2014 hello / Greeter.class
988 Sex 30 de maio 16:02:32 CDT 2014 hello / HelloWorld.class
~~~

Os arquivos de classe estão agrupados. É importante observar que, mesmo que você tenha declarado o joda-time como uma dependência, a biblioteca não está incluída aqui. E o arquivo JAR também não pode ser executado.

Para tornar esse código executável, podemos usar o plugin `application` do gradle . Adicione ao seu `build.gradle`: 

~~~ 
apply plugin: 'application'

mainClassName = 'hello.HelloWorld'
~~~ 

Rode o programa: 

~~~
$ ./gradlew run
:compileJava UP-TO-DATE
:processResources UP-TO-DATE
:classes UP-TO-DATE
:run
The current local time is: 16:16:20.544
Hello world!

BUILD SUCCESSFUL

Total time: 3.798 secs
~~~

Agrupar dependências requer mais reflexão. Por exemplo, se estivéssemos construindo um arquivo WAR, um formato comumente associado à compactação em dependências de terceiros, poderíamos usar o plugin WAR da gradle. 

Se você estiver usando o Spring Boot e desejar um arquivo JAR executável, o plug-in `spring-boot-gradle` é bastante útil. 

Nesse estágio, o gradle não sabe o suficiente sobre o seu sistema para fazer uma escolha. Mas, por enquanto, isso deve ser suficiente para começar a usar o gradle.

Para finalizar este guia, aqui está um `build.gradle` completo :

~~~
apply plugin: 'java'
apply plugin: 'eclipse'
apply plugin: 'application'

mainClassName = 'hello.HelloWorld'

// tag::repositories[]
repositories {
    mavenCentral()
}
// end::repositories[]

// tag::jar[]
jar {
    baseName = 'gs-gradle'
    version =  '0.1.0'
}
// end::jar[]

// tag::dependencies[]
sourceCompatibility = 1.8
targetCompatibility = 1.8

dependencies {
    compile "joda-time:joda-time:2.2"
    testCompile "junit:junit:4.12"
}
// end::dependencies[]

// tag::wrapper[]
// end::wrapper[]
~~~

Existem muitos comentários de início/fim incorporados aqui. 

Isso torna possível extrair bits do arquivo de compilação neste guia para obter as explicações detalhadas acima. Você não precisa deles no seu arquivo de build da produção.
