# API

A API é um conjunto de rotinas e padrões de programação para acesso a um aplicativo de software ou plataforma baseada na Web. 

A - Application. 
P - Programming
I - Interface.

Na prática é uma interface que faz a ponte entre um programa e terceiros. Necessita um protocolo de autenticação. 

## 1.1. Endpoint

É uma URL que realiza, em geral, uma ação, podendo ser um GET, PUT, DELETE, ETC. 

## 1.2. Estrutura de URL

`esquema ou protocolo://domínio:porta/basePath/endpointPath/recurso?query_parameter#fragmento`

Todos os caminhos da API são relativos a este URL base.  

Por exemplo: `/users` na verdade significa `<scheme>://<host>/<basePath>/users`. 

### 1.2.1. Schemes 

São os protocolos de transferência usados pela API.  
Como em qualquer lista do YAML, os esquemas podem ser especificados usando:

* sintaxe da lista: 
  * Http 
  * Https 
* Sintaxe literal:  
  * [http, https] 

### 1.2.2. Path 

* Prefixo da URL para todos os caminhos da API, em relação à raiz do host.  

* Ele deve começar com uma barra inicial `/`.  

* Se o basePath não for especificado, o padrão será `/`  para todos os caminhos iniciados na raiz do host.  

* Caminhos base válidos: 
  * `/v2` 
  * `/api/v2` 
  * `/` 

### 1.2.3. Templates 

São modelos pré-formatados:

  * https://{customer_id}.saas-app.com/api/v1 
  * https://api.saas-app.com/v1/{customer_id}/apis 

### 1.2.4. Queries 

Se uma sequência de queries for usada, ela segue o componente do caminho e fornece uma sequência de informações que o recurso pode usar para algum propósito.  

Exemplo: 

* parâmetros para uma pesquisa; 
* dados a serem processados. 
* Quando a string de consulta geralmente é uma string de pares de nome e valor: 
  * term = bluebird.  
* Quando há mais de uma String de consulta:  
  * term = bluebird & source = pesquisa no navegador. 

### 1.2.5. user-Agent 

O cabeçalho de requisição User-Agent contém uma string característica que permite o protocolo de rede do cliente identificar o tipo de:  

* aplicação,  
* sistema operacional,  
* fornecedor do software  
* versão do software do agente de usuário do software solicitante. 

Exemplo: 

User-Agent: Mozilla/<version> (<system-information>) <platform> (<platform-details>) <extensions> 

## 1.3. Postman
    
| Parameters | Pares de valor-chave  |
|--|--|
| Authorization | Authorização: o que você  pode  fazer (!= Authentication: quem  você é)|
| Headers | POST, GET, etc. 
| Body | Tudo o que você  coloca  na  área de texto é enviado com a solicitação.| 

## 1.4. Repositórios de APIs

* https://www.programmableweb.com/ (Mais antigo da Web) 
* https://99apis.com/home (Brasileiro) 
* https://market.mashape.com/explore (Marketplace de APIs) 
* https://apis.io/ 
* https://www.therightapi.com/ 
* https://developers.google.com/apis-explorer/ 
* https://developers.google.com/discovery/ 
* https://apihound.com/apifinder 
