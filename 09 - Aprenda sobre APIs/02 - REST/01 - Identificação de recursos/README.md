# Identificação dos Recursos

Toda aplicação gerencia algumas informações. Uma aplicação de um E-commerce, por exemplo, gerencia seus produtos, clientes, vendas, etc. Essas coisas que uma aplicação gerencia são chamadas de Recursos no modelo REST.

Um recurso nada mais é do que uma abstração sobre um determinado tipo de informação que uma aplicação gerencia, sendo que um dos princípios do REST diz que todo recurso deve possuir uma identificação única. 

Essa identificação serve para que a aplicação consiga diferenciar qual dos recursos deve ser manipulado em uma determinada solicitação.

Imagine a seguinte situação: Você desenvolveu um Web Service REST que gerencia seis tipos de recursos. Os clientes desse Web Service manipulam esses recursos via requisições HTTP. 

Ao chegar uma requisição para o Web Service, como ele saberá qual dos recursos deve ser manipulado? É justamente por isso que os recursos devem possuir uma identificação única, que deve ser informada nas requisições.

A identificação do recurso deve ser feita utilizando-se o conceito de URI (Uniform Resource Identifier), que é um dos padrões utilizados pela Web. 

Alguns exemplos de URI’s:

* http://servicorest.com.br/produtos;
* http://servicorest.com.br/clientes;
* http://servicorest.com.br/clientes/57;
* http://servicorest.com.br/vendas.

As URI’s são a interface de utilização dos seus serviços e funcionam como um contrato que será utilizado pelos clientes para acessá-los. Vejamos agora algumas boas práticas no uso de URI’s.
