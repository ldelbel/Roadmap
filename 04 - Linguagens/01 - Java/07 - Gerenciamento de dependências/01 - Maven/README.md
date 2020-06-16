# Tutorial Maven 

## 1. Build Lifecycle

Para fácil acesso, coloquei essa informação primeiro. 

Phase | Description
:--------:|:----------------
 validate| valida se todas as informações obrigatórias do projeto estão preenchidas e são válidas.
 compile| compila o código-fonte.
 test| executa os testes unitários presentes no projeto, desde que o framework de testes utilizado seja compatível com o Maven. Por padrão, é usado o jUnit.
 package|  empacota o código compilado no formato definido pela tag packaging do pom.xml.
 integration-test| caso exista, o pacote gerado no estágio anterior é instalado em um ambiente de teste de integração.
  verify|  executa checagens para verificar se o pacote é válido e se atende aos critérios de qualidade.
 install|  instala o pacote no repositório local, de modo que outros projetos locais possam utilizá-lo como dependência.
 deploy| instala o pacote em repositórios externos, efetivamente disponibilizando-o em ambientes remotos.
 
Um ponto central do Maven é o conceito de ciclo de vida de construção (build lifecycle), que significa que os procedimentos de construção são definidos em etapas chamadas de estágios do ciclo de vida. 

Esses estágios ocorrem **de forma cumulativa**. Exemplo: 

> Se o estágio 4 de um ciclo de vida for invocado, os estágios anteriores também serão executados ordenadamente, ou seja, os estágios 1, 2 e 3 serão acionados antes do Maven ativar o estágio 4.

Os três ciclos de vida de construção que são nativos da ferramenta são o padrão (default), o clean e o site. 

* **Default**: gerencia a implementação do projeto; 
* **Clean**: gerencia a limpeza do projeto;
* **Site**: gerencia a criação automatizada da documentação do projeto. 

O ciclo de vida padrão possui mais de 20 estágios, dos quais os mais importantes são:

* **validate**: valida se todas as informações obrigatórias do projeto estão preenchidas e são válidas;
* **compile**: compila o código-fonte;
* **test**: executa os testes unitários presentes no projeto, desde que o framework de testes utilizado seja compatível com o Maven. Por padrão, é usado o jUnit;
* **package**: empacota o código compilado no formato definido pela tag packaging do pom.xml;
* **integration-test**: caso exista, o pacote gerado no estágio anterior é instalado em um ambiente de teste de integração;
* **verify**: executa checagens para verificar se o pacote é válido e se atende aos critérios de qualidade;
* **install**: instala o pacote no repositório local, de modo que outros projetos locais possam utilizá-lo como dependência;
* **deploy**: instala o pacote em repositórios externos, efetivamente disponibilizando-o em ambientes remotos.

Rotineiramente, costumamos invocar o estágio **install** ou **clean install**, que engloba todos os outros anteriores e, ao final de sua execução, temos o código fonte todo compilado, pronto para execução e disponibilizado como dependência para outros projetos locais.

## 2. Configuração dos Paths

A primeira etapa é a criação de duas variáveis de ambiente no sistema operacional: JAVA_HOME e M2_HOME. Uma variável de ambiente é um valor nomeado dinamicamente que pode afetar o modo como os processos em execução irão se comportar em um computador.

As variáveis podem ser usadas tanto por scripts quanto pela linha de comando. São geralmente referenciadas usando-se símbolos especiais na frente ou nas extremidades no nome da variável. 

Por exemplo, para mostrar o caminho de busca em um sistema DOS ou Windows, usa-se o comando `echo %PATH%`, em Unix usa-se `echo $PATH`.

* JAVA_HOME indica a localização do diretório do JDK; 
* M2_HOME representa a localização do diretório do Maven. 
* Também é necessário acrescentar ao conteúdo da variável Path do sistema a pasta bin do Maven.

Para testar se a instalação foi realizada com sucesso, basta executarmos o comando mvn -version na linha de comando

## 3. Criando projetos

### 3.1 Gerando um arquétipo

O Maven provê uma excelente funcionalidade de criação automática de projetos através de arquétipos. Os arquétipos são “esqueletos” que podem ser usados como base para projetos. 

O comando: `mvn archetype:generate` listará os arquétipos disponíveis e iniciará a criação dos projetos. 

Caso esta seja a primeira vez em que este comando esteja sendo executado, o Maven irá baixar os plugins que necessita para gerar a listagem de arquétipos. 

**Este mesmo procedimento acontecerá cada vez que o usuário invocar uma função do Maven pela primeira vez**, porque a ferramenta possui inteligência para acrescentar funcionalidades a si, por meio do download de plugins adicionais.

### 3.2 Identificando o projeto

O próximo passo é fornecermos os valores de groupId, artifactId, version e package.

* **GroupId**: nome que será usado como ponto de partida da hierarquia (grupo) do projeto no repositório Maven. Normalmente assume o nome do pacote principal.

* **ArtifactId**: nome do projeto em si.

* **Version**: versão do seu projeto, o que é muito importante à medida que o projeto amadurece e novas versões são lançadas.

* **package**: nome do pacote principal.

O Maven utiliza essas informações para definir a identidade de um artefato em particular, seja ele um projeto ou uma dependência.

A partir do diretório onde o comando do Maven foi executado, um novo diretório será criado, com o nome que foi informado para o **artifactId**.

### 3.3 Estrutura do projeto

Depois de criar o diretório do projeto, o Maven criou a pasta **src**, onde todo código-fonte deve ser mantido. Dentro de src, main e test também são criadas. 

* **Main**: conterá o código-fonte propriamente dito do projeto; 
* **Test**: conterá o código-fonte dos testes unitários. 

Finalmente, dentro destes, será criada a estrutura de pastas determinada pelo package, informado na criação do arquétipo, precedidas por um diretório pai chamado **java**.

* **Target**: Além desses diretórios, `target` é criado pelo Maven sempre que é necessário compilar, construir ou gerar informações sobre o projeto. 

Após a compilação, todo código do projeto será compilado e o seu resultado colocado dentro do diretório target, conforme podemos notar por meio da criação de um arquivo `.class` 

## 4. Gerenciamento de dependências

### 4.1 respositórios locais e remotos

Praticamente todo projeto utiliza bibliotecas nativas ou disponibilizadas por terceiros para reuso de código ou para obter funcionalidades extras. 

Gerenciar essas bibliotecas, chamadas de dependências no jargão do Maven, pode se tornar uma dor de cabeça em projetos com várias delas.

O Maven fornece uma maneira fácil de administrar as bibliotecas a partir do arquivo `pom.xml` que contém a lista de dependências que um projeto utiliza. 

Com esta lista, a ferramenta as analisa e tenta localizá-las para disponibilizar para o projeto. Os lugares onde o Maven procura por dependências chamam-se **repositórios**, cujos tipos principais são local e público.

O repositório local fica no computador onde se está rodando o Maven. Ele está localizado na pasta **.m2/repository** dentro da **pasta home** do usuário. 

Este é o primeiro lugar onde a ferramenta procura toda vez que precisa localizar uma dependência. Caso não a encontre, irá verificar o repositório público oficial, localizado em http://repo.maven.apache.org/maven2/. 

Se encontrar a dependência que precisa, o Maven primeiro copia para o repositório local e depois a disponibiliza para o projeto, de modo que não será mais necessária uma consulta ao repositório público quando precisar desta mesma dependência no futuro. 

Além destes repositórios, podemos informar que utilizaremos dependências de outros repositórios, bastando, para isso, registrá-los no pom.xml. 

Em certos ambientes corporativos, onde diretivas de segurança **vetem o acesso livre à internet**, é comum a existência de repositórios na rede local que contêm as bibliotecas **homologadas pela corporação** para uso em seus projetos.

Depois de localizadas as bibliotecas necessárias no repositório local, o Maven as utiliza durante a execução de seus comandos. 

Exemplos: 

* Se o comando for `mvn compile`, o Maven irá utilizar as dependências para compilar o projeto; 
* Se o comando for `mvn package` para um projeto web, as dependências serão inseridas dentro do **arquivo WAR** gerado pelo empacotamento do projeto, e o WAR resultante será criado dentro do diretório target; 
* Se o comando for `mvn dependency:copy-dependencies`, o Maven disponibilizará as bibliotecas para o projeto, colocando-as dentro do diretório target.

Outra capacidade da ferramenta é identificar as dependências das dependências do projeto. Ou seja, se uma biblioteca depender de outras, o Maven irá procurar por elas também e assim sucessivamente, até todas as dependências necessárias estarem à disposição do projeto.

### 4.2 Arquivo pom.xml

Este arquivo, presente no **diretório-raiz** do projeto, contém todas as configurações que o Maven necessita para interagir corretamente com o projeto. 

Ele pode ser simples, somente possuindo as coordenadas do projeto, ou extremamente complexo, relacionando:

* dependências;
* repositórios; 
* repositórios de plugins; 
* plugins específicos; 
* estratégias de construção do projeto; 
* perfis;
* etc.

~~~
<project xmlns="http://maven.apache.org/POM/4.0.0"  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  
  <groupId>com.atalhox</groupId>
  <artifactId>ProjetoExemplo</artifactId>
  <version>1.0-SNAPSHOT</version>
  <packaging>jar</packaging>
  
  <name>ProjetoExemplo</name>
  
  <properties>
       <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  </properties>
  
  <dependencies>
       <dependency>
       <groupId>junit</groupId>
       <artifactId>junit</artifactId>
       <version>3.8.1</version>
       <scope>test</scope>
       </dependency>
  </dependencies>
</project>
~~~

## 5. Documentação do projeto

Inclua o seguinte trecho em sua pom.xml: 

~~~ 
  <reporting>
    <plugins>
       <plugin>
              <groupId>org.apache.maven.plugins</groupId>
              <artifactId>maven-project-info-reports-plugin</artifactId>
              <version>2.2</version>
        </plugin>
    </plugins>
  </reporting>
~~~ 

Feito isso, ao executarmos o comando mvn clean site, o diretório site será criado dentro de target e nele haverá um arquivo chamado index.html. 

Ao abrí-lo em um navegador, veremos que foi montado um pequeno site informativo do projeto, com diversas informações úteis, como a árvore de dependências do projeto.

Outra funcionalidade útil do Maven é a geração simplificada do Javadoc do projeto. Para tanto, basta incluir o plugin do Javadoc na seção reporting: 

~~~
  <reporting>
    <plugins>
 (...)
         <plugin>
              <groupId>org.apache.maven.plugins</groupId>
              <artifactId>maven-javadoc-plugin</artifactId>
              <version>2.7</version>
        </plugin>
        (...)
    </plugins>
  </reporting>
~~~

Esta seção do pom.xml é destinada aos plugins que geram relatórios sobre o código-fonte. Para acionar o plugin, basta usar o comando `mvn clean javadoc:jar`.

## 6. Build

Em seguida, precisamos declarar explicitamente qual a versão do Maven compiler a ser utilizada. No caso do compiler, acrescentaremos a seção build, que é a seção onde definimos os plugins utilizados para geração de código. 

~~~
<build>
       <plugins>
             <plugin>
      <artifactId>maven-compiler-plugin</artifactId>
      <version>2.0.2</version>
      <configuration>
       <source>$</source>
         <target>$</target>
      </configuration>
       </plugin>
       </plugins>
  </build>
~~~

As propriedades **$** do Maven servem como ‘placeholder’ ou marcas de substituição e tem o formato ${nome.da.variavel}.

## 7. Propriedades

Segue a lista de propriedades padrão. 

| PROPRIEDADE | VALOR  _DEFAULT_|
|--|--|
| ${project.basedir} ou  ${basedir}|Pasta onde fica o  pom.xml. Ex: “D:\projeto1”|
| ${project.parent.basedir} | Pasta do  pom.xml  do parent.
| ${build.directory}| Caminho absoluto da pasta target. Ex. “D:\projeto1\target”
| ${build.outputDirectory}| Caminho absoluto da pasta classes. Ex.“D:\projeto1\target\classes”
| ${version) |Versão definido no  pom.xml. Ex. “1.0-SNAPSHOT”
| ${artifact.extension} | Extensão do arquivo que está sendo criado. Ex.: “jar”
| ${java.version}| Versão do JRE (Java Runtime Environment)
| ${java.vendor}| Fabricante do JRE
| ${java.vendor.url} | URL do Fabricante da JRE
| ${java.home}| Pasta (Diretório) onde a JRE está instalada
| ${java.vm.specification.version}| Versão da Especificação da JVM (Java Version Machine)|
| ${java.vm.specification.vendor}| Fabricante da Especificação da JVM |
| ${java.vm.specification.name} | Nome da Especificação da JVM |
| ${java.vm.version} | Versao da Implementação da JVM |
| ${java.vm.vendor} | Fabricante da Implementação da JVM |
|${java.vm.name} | Nome da Implementação da JVM |
| ${java.specification.version} | Versão da Especificação da JRE |
| ${java.specification.vendor} | Fabricante da Especificação da JRE |
| ${java.specification.name} | Nome da Especificação da JRE |
| ${java.class.version} | Versão do Formato das Classes JAVA |
| ${java.library.path}| CLASSPATH do JAVA |
| ${java.class.path} | Lista de pastas para procurar quando carregar as bibliotecas |
| ${java.io.tmpdir} | Pasta temporária padrão |
| ${java.compiler} | Name of JIT compiler to use |
| ${java.ext.dirs} | Path of extension directory or directories |
| ${os.name} | Nome do Sistema Operacional |
| ${os.arch} | Arquitetura do Sistema Operacional |
| ${os.version} | Versão do Sistema Operacional |
| ${file.separator} | Caractere separador de Arquivos (“/” on UNIX) |
|${path.separator}  | Caractere separador de Pastas (“:” on UNIX) |
| ${line.separator}| Separador de Linhas (“\n” on UNIX) |
| ${user.name} | Nome da Conta do Usuário |
| ${user.home} | Diretório padrão (home) do usuário.|
| ${user.dir} | Diretório corrente do usuário |
