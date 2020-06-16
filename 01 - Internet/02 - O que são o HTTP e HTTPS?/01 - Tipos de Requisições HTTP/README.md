# Utilização de métodos HTTP para manipulação dos recursos

Os recursos gerenciados por uma aplicação, e identificados unicamente por meio de sua URI, geralmente podem ser manipulados de diversas maneiras. 

É possível criá-los, atualizá-los, excluí-los, dentre outras operações.

Quando um cliente dispara uma requisição HTTP para um serviço, além da URI que identifica quais recursos ele pretende manipular, é necessário que ele também informe o tipo de manipulação que deseja realizar no recurso. 

É justamente aí que entra um outro conceito da Web, que são os métodos do protocolo HTTP.

O protocolo HTTP possui diversos métodos, sendo que cada um possui uma semântica distinta, e devem ser utilizados para indicar o tipo de manipulação a ser realizada em um determinado recurso.

Vejamos agora os principais métodos do protocolo HTTP e o cenário de utilização de cada um deles:

|Método |Descrição  |
|--|--|
| GET | Obter os dados de um recurso.
|POST |	Criar um novo recurso. |
|PUT | Substituir os dados de um determinado recurso.
|PATCH| Atualizar parcialmente um determinado recurso.
|DELETE| Excluir um determinado recurso.
|HEAD| Similar ao GET, mas utilizado apenas para se obter os cabeçalhos de resposta, sem os dados em si.
|OPTIONS| Obter quais manipulações podem ser realizadas em um determinado recurso.

Geralmente as aplicações apenas utilizam os métodos GET, POST, PUT e DELETE, mas se fizer sentido em sua aplicação utilizar algum dos outros métodos, não há nenhum problema nisso.

Veja a seguir o padrão de utilização dos métodos HTTP em um serviço REST, que é utilizado pela maioria das aplicações e pode ser considerado uma boa prática.

 Como exemplo será utilizado um recurso chamado Cliente.

|Método | URI | Utilização |
|--|--|--|
| GET |clientes  | Recuperar os dados de todos os clientes.|
|GET|clientes/id |	/	Recuperar os dados de um determinado cliente.
|POST|	/clientes|	Criar um novo cliente.
|PUT|	/clientes/id|	Atualizar os dados de um determinado cliente.
|DELETE|	/clientes/id|	Excluir um determinado cliente.

Como boa prática, em relação aos métodos do protocolo HTTP, evite utilizar apenas o método POST nas requisições que alteram o estado no servidor, tais como: cadastro, alteração e exclusão. 

Evite utilizar o método GET nesses tipos de operações, pois é comum os navegadores fazerem cache de requisições GET, as disparando antes mesmo do usuário clicar em botões e links em uma pagina HTML.

# Requisições

![HTTP](https://mdn.mozillademos.org/files/13687/HTTP_Request.png)

## 1. Tipos de requisições

As requisições consistem dos seguintes elementos:

- Um método HTTP, geralmente é um verbo como: 
    - GET;  
    - POST; 
    - DELETE; 
    - PUT; 
    - OPTIONS; 
    - HEAD. 
    
Tipicamente, um cliente que pegar um recurso (usando GET) ou publicar dados de um formulário HTML (usando POST), embora mais operações podem ser necessárias em outros casos.

## 2. Caminho do recurso 

As requisições também podem solicitar a URL do recurso sem os elementos que são de contexto, por exemplo: 

- sem o protocolo protocol (http://); 
- o domínio domain (como developer.mozilla.org); 
- a porta port TCP (80 que é ocultado por ser o número da porta padrão).

## 3. Versão do protocolo HTTP

A versão do protocolo pode ser: 1.0, 1.1, 2.0. 

## 4. Cabeçalhos opcionais 

Alguns destes cabeçalhos podem conter informações adicionais para os servidores.

## 5. Corpo de dados

Para alguns métodos como o POST, os cabeçalhos podem trazer um corpo de dados.
