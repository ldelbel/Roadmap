# Requisições HTTP

## 1. Headers (Cabeçalhos) 

Cabeçalhos HTTP seguem a estrutura básica de uma cadeia de caracteres insensível à caixa seguida de dois pontos (':') e um valor cuja estrutura depende do cabeçalho.  

O cabeçalho inteiro, incluindo o valor, consiste em uma única linha, que pode ser bem grande. 

Há numerosos cabeçalhos de requisição disponíveis. Eles podem ser divididos em vários grupos: 
* **Cabeçalhos gerais**: como Via,  se aplicam à mensagem como um todo. 
* **Cabeçalhos de requisição**: como User-Agent, Accept-Type, modificam a requisição, especificando-a mais (como Accept-Language), dando-a contexto (como Referer), ou restringindo-a condicionalmente (como If-None). 
* **Cabeçalhos de entidade**: como Content-Length que se aplicam ao corpo da mensagem. Obviamente este cabeçalho não será transmitido se não houver corpo na requisição. 

## 2. Body 

* A parte final da requisição é o corpo.  
* Nem todas as requisições tem um.  
* As que pegam recursos, como GET, HEAD, DELETE, ou OPTIONS, usualmente não precisam de um.  
* Algumas requisições enviam dados ao servidor a fim de atualizá-lo: é o caso frequente de requisições POST (contendo dados de formulário HTML). 

Corpos podem ser divididos, a grosso modo, em duas categorias: 
* Corpos de recurso-simples, consistindo em um único arquivo, definido pelos dois cabeçalhos:  
  * Content-Type  
  * Content-Length. 
* Corpos de recurso-múltiplo, consistindo em um corpo de múltiplas partes, cada uma contendo uma porção diferente de informação. Este é tipicamente associado à Formulários HTML. 

## 3. Resposta 

A linha inicial de uma resposta HTTP, chamada de linha de status, contém a seguinte informação: 
* A versão do protocolo, normalmente HTTP/1.1. 
* Um código de status, indicando o sucesso ou falha da requisição. Códigos de status comuns são 200, 404, ou 302 
* Um texto de status. Uma descrição textual breve, puramente informativa, do código de status a fim de auxiliar o entendimento da mensagem HTTP por humanos. 

Exemplo: HTTP/1.1 404 Not Found. 
