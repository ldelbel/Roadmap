# Evitar colocar a operação na URI

Os recursos que uma aplicação gerencia podem ser manipulados de diversas maneiras, sendo para isso disponibilizada algumas operações para manipula-los, tais como: criar, listar, excluir, atualizar, etc.

A manipulação dos recursos deve ser feita utilizando-se os métodos do protocolo HTTP, que inclusive é um dos princípios do REST que será discutido mais adiante.

Portanto, evite definir URI’s que contenham a operação a ser realizada em um recurso, tais como:

* http://servicorest.com.br/produtos/cadastrar;
* http://servicorest.com.br/clientes/10/excluir;
* http://servicorest.com.br/vendas/34/atualizar.

# Evitar adicionar na URI o formato desejado da representação do recurso

É comum que um serviço REST suporte múltiplos formatos para representar seus recursos, tais como XML, JSON e HTML. 

A informação sobre qual o formato desejado por um cliente ao consultar um serviço REST deve ser feita via Content Negotiation, conforme será mostrado mais adiante.

Portanto, evite definir URI’s que contenham o formato desejado de um recurso, tais como:

* http://servicorest.com.br/produtos/xml;
* http://servicorest.com.br/clientes/112?formato=json.

# Evite alterações nas URI’s

A URI é a porta de entrada de um serviço. Se você a altera, isso certamente causará impacto nos clientes que estavam a utilizando, pois você alterou a forma de acesso a ele.

 Após definir uma URI e disponibilizar a manipulação de um recurso por ela, evite ao máximo sua alteração.

Nos casos mais críticos, no qual realmente uma URI precisará ser alterada, notifique os clientes desse serviço previamente. 

Verifique também a possibilidade de se manter a URI antiga, fazendo um redirecionamento para a nova URI.
