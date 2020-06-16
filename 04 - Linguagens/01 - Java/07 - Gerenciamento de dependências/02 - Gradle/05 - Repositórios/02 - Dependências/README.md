# Dependências

Use esse recurso para declarar dependências externas, que deseja baixar da Web. Isso define as seguintes configurações padrão: 

* **Compile**: As dependências necessárias para compilar a fonte de produção do projeto.

* **Runtime**: As dependências requeridas pelas classes de produção no tempo de execução. Por padrão, também inclui as dependências de tempo de compilação.

* **Test Compile**: As dependências necessárias para compilar a fonte de teste do projeto. Por padrão, inclui classes de produção compiladas e as dependências de tempo de compilação.

* **Test Runtime**: As dependências necessárias para executar os testes. Por padrão, inclui dependências de tempo de execução e compilação de teste.

Exemplo: 
~~~
dependencies {
   compile group: 'org.hibernate', name: 'hibernate-core', version: '3.6.7.Final'
}
~~~
