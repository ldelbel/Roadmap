# Autenticação e autorização

A principal dificuldade em criar um serviço REST totalmente Stateless ocorre quando precisamos lidar com os dados de autenticação/autorização dos clientes. 

A dificuldade ocorre porque é natural para os desenvolvedores armazenarem tais informações em sessão, pois essa é a solução comum ao se desenvolver uma aplicação Web tradicional.

A principal solução utilizada para resolver esse problema é a utilização de Tokens de acesso, que são gerados pelo serviço REST e devem ser armazenados pelos clientes, via cookies ou HTML 5 Web Storage, devendo também ser enviados pelos clientes a cada nova requisição ao serviço.

Já existem diversas tecnologias e padrões para se trabalhar com Tokens, dentre elas:

* OAUTH;
* JWT (JSON Web Token);
* Keycloack.
