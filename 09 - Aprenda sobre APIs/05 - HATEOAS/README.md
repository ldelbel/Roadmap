# HATEOAS (Hypermedia As The Engine Of Application State)

Para entendermos melhor o conceito de HATEOAS, vamos a um exemplo comum quando utilizamos a Web.

Imagine que você quer comprar um produto pela Web, em algum site de E-commerce. 

Você entra no site, navega pelas categorias de produtos via menu do site, encontra o seu produto e chega até a tela de detalhes dele, que possui as informações de preço, frete e o botão para realizar a compra.

Mas nem sempre o produto está disponível em estoque, por isso o site costuma fazer um tratamento nessa situação, escondendo o botão de realizar a compra e exibindo um botão para notificação quando o produto voltar a estar disponível.

No exemplo anterior, o conceito de HATEOAS foi aplicado duas vezes. 

**Primeiro**, quando o cliente entrou no site de E-commerce, como ele fez para chegar até a página de detalhes do produto? Navegando via links.

Normalmente todo site ou aplicação Web possui diversas funcionalidades, sendo que a navegação entre elas costuma ser feita via links. Um cliente até pode saber a URI de determinada página ou recurso, mas se ele não souber precisamos guiá-lo de alguma maneira para que ele encontre as informações que procura.

O **segundo** uso do HATEOAS ocorreu quando o cliente acessou a página de detalhes do produto. Se o produto estivesse em estoque, o site apresentaria o botão de comprar, e o cliente poderia finalizar seu pedido. 

Caso contrário, ele apenas poderia registrar-se para ser notificado. Tudo isso é feito, principalmente, para garantir a consistência das informações.

Perceba que os links foram utilizados como mecanismo para conduzir o cliente quanto à navegação e ao estado dos recursos. 

Esse é o conceito que foi chamado de HATEOAS, que nada mais é do que a utilização de Hypermedia, com o uso de links, como o motor para guiar os clientes quanto ao estado atual dos recursos, e também quanto as transições de estado que são possíveis no momento.

Isso certamente pode gerar algumas dúvidas para os clientes desse serviço REST, como por exemplo:

* É possível solicitar o cancelamento do pedido? 
* Como?
* Quais são os outros estados do pedido e como transitar entre eles?
* Como obter mais informações sobre o cliente desse pedido?

Essas dúvidas poderiam ser respondidas facilmente se o conceito HATEOAS fosse utilizado, facilitando assim a vida dos clientes do serviço REST. 

Vejamos agora esta representação, porém com a utilização do HATEOAS:

> < pedido self="http://servicorest.com.br/pedidos/1459">
  < id>1459</ id>
  < data>2017-01-20< /data>
  < status>PENDENTE< /status>
  < cliente ref="http://servicorest.com.br/clientes/784" />
  < acoes>
    < acao>
      < rel>self</ rel>
      < uri>http://servicorest.com.br/pedidos/1459</ uri>
      < method>GET</ method>
    < /acao>
    < acao>
      < rel>cancelar</ rel>
      < uri>http://servicorest.com.br/pedidos/1459< /uri>
      < method>DELETE</ method>
    < /acao>
  < /acoes>
< /pedido>

Perceba como agora ficou muito mais simples explorar as informações e descobrir quais caminhos seguir. HATEOAS é um dos princípios que dificilmente vemos sendo aplicados em serviços REST no mercado, quase sempre por falta de conhecimento dos desenvolvedores.
