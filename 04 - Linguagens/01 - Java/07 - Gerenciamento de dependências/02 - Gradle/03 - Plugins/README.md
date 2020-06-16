# Plugins

Existem dois tipos gerais de plugins no Gradle: `plugins de script` e `plugins binários`. 

Os `plugins de script` são scripts de build adicionais que configuram ainda mais a build e geralmente implementam uma abordagem declarativa para manipular a build. 

Eles geralmente são usados em uma build, embora possam ser externalizados e acessados de um local remoto. 

`Plugins binários` são classes que implementam a interface Plugin e adotam uma abordagem programática para manipular a compilação. 

`Plugins binários` podem residir em um script de build, na hierarquia do projeto ou externamente em um jar de plug-ins.

Um plug-in geralmente começa como um `plugin de script` (porque é fácil de escrever) e à medida que o código se torna mais valioso, é migrado para um `plugin binário` que pode ser facilmente testado e compartilhado entre vários projetos ou organizações.

## 1. Java Plugin

Ao adicionar o plugin java, teremos todas as seguintes tasks agregadas ao programa. 

~~~
plugins {
    id 'java'
}
~~~

| Task | Descrição |
|--|--|
|  compileJava | Compila arquivos de origem Java de produção usando o compilador JDK. |
| processResources | Copia recursos de produção para o diretório de recursos de produção. | 
| classes | Essa é uma tarefa agregada que depende apenas de outras tarefas. Outros plugins podem anexar tarefas de compilação adicionais. |
| compileTestJava | Compila arquivos de origem Java de teste usando o compilador JDK. |
| processTestResources | Copia recursos de teste no diretório de recursos de teste. |
| testClasses | Essa é uma tarefa agregada que depende apenas de outras tarefas. Outros plugins podem anexar tarefas adicionais de compilação de teste. | 
| jar | Monta o arquivo JAR de produção, com base nas classes e recursos anexados ao mainconjunto de origem. |
| javadoc | Gera documentação da API para a origem Java de produção usando Javadoc. | 
| test | Executa os testes de unidade usando JUnit ou TestNG. |
| uploadArchives | Carrega artefatos,incluindo o arquivo JAR de produção, nos repositórios configurados. Esta tarefa foi descontinuada; você deve usar um dos plug-ins de publicação Ivy ou Maven. |
| clean | Exclui o diretório de criação do projeto.  |
| cleanTaskName | Exclui arquivos criados pela tarefa especificada. Por exemplo, cleanJar excluirá o arquivo JAR criado pela task `jar` e `cleanTest` excluirá os resultados do teste criados pela  task `test`. | 

## 2. Java Library Plugin

O plug-in Java Library expande os recursos do plug-in Java, fornecendo conhecimento específico sobre bibliotecas Java. 

Em particular, uma biblioteca Java expõe uma API aos consumidores (ou seja, outros projetos usando o plug-in Java ou Java Library). Todos os conjuntos de fontes, tarefas e configurações expostas pelo plug-in Java estão implicitamente disponíveis ao usar esse plug-in.

A principal diferença entre o plug-in Java padrão e o plug-in Java Library é que este último introduz o conceito de uma API exposta aos consumidores. 

Uma biblioteca é um componente Java destinado a ser consumido por outros componentes. É um caso de uso muito comum em compilações de vários projetos, mas também assim que você tiver dependências externas.

O plug-in expõe duas configurações que podem ser usadas para declarar dependências: `api` e `implementation`. 

1. A `api` deve ser usada para declarar dependências exportadas pela API da biblioteca. 
2. A `implementation` deve ser usada para declarar dependências internas ao componente.

~~~ 
plugins {
    id 'java-library'
}
~~~ 

~~~
dependencies {
    api 'org.apache.httpcomponents:httpclient:4.5.7'
    implementation 'org.apache.commons:commons-lang3:3.5'
}
~~~

Benefícios:

* dependências não vazam mais no caminho de classe de compilação dos consumidores, portanto você nunca dependerá acidentalmente de uma dependência transitiva

* compilação mais rápida graças ao tamanho reduzido do caminho de classe

* menos recompilações quando as dependências da implementação mudam: os consumidores não precisariam ser recompilados

* publicação mais limpa: quando usadas em conjunto com o novo maven-publish plug-in, as bibliotecas Java produzem arquivos POM que distinguem exatamente entre o que é necessário para compilar na biblioteca e o que é necessário para usar a biblioteca em tempo de execução (em outras palavras, não misture o que é necessário para compilar a própria biblioteca e o que é necessário para compilar na biblioteca).

## 3. Java Application Plugin

O plug-in de aplicativo facilita a criação de um aplicativo executável da JVM. Torna fácil iniciar o aplicativo localmente durante o desenvolvimento e empacotar o aplicativo como TAR e / ou ZIP, incluindo scripts de inicialização específicos do sistema operacional.

~~~
plugins {
    id 'application'
}
~~~

A única configuração obrigatória para o plug-in é a especificação da classe principal (ou seja, ponto de entrada) do aplicativo.

~~~
application {
    mainClassName = 'org.gradle.sample.Main'
}
~~~
