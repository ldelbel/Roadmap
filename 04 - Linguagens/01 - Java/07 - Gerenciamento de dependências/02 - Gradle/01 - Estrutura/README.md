## Estrutura

Tudo no Gradle se resumo a dois conceitos básicos: Projects e Tasks.

A grande idéia do Gradle é permitir configurações baseando-se em tasks, ou seja, quando queremos criar algum novo comportamento durante o build, vamos criar uma task!

## 1. Projects

Toda build do gradle é feita de um ou mais projects, a representação de project dependerá de como você irá utilizar o Gradle. 

Por exemplo, podemos ter um project que representa um JAR ou até mesmo uma aplicação web. 

Um project não necessariamente representa coisas que serão construídas, ele também pode representar coisas que serão feitas, como o deploy de sua aplicação para ambientes de homologação ou produção.

## 2. Tasks

Cada project é feito de uma ou mais tasks, uma task representa um pedaço de trabalho que uma build vai executar. 

Podemos ter por exemplo tasks que fazem a compilação de classes, criação de JARs e até mesmo a publicação de arquivos para um repositório especifico.

Um detalhe bacana das tasks do Gradle é que não são case sensitive, por isso que conseguimos executar a task executarTask escrevendo executartask.

Basicamente, precisamos adicionar o seguinte conteúdo no corpo da nossa task:

~~~
task minhaPrimeiraTask {
    group 'personal'
    description 'testes de primeiro contato com o Gradle'
    print 'Rodando minha primeira task'
}
~~~

Dessa forma o daemon irá retornar a taks com o nome `personal` tasks. 

## 3. Gradle Daemon

O daemon trata-se de uma instância da JVM para o Gradle com a finalidade de agilizar a execução das tasks.
