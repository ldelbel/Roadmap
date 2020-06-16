# REST

Representational State Transfer, abreviado como REST, não é uma tecnologia, uma biblioteca, e nem tampouco uma arquitetura, mas sim um modelo a ser utilizado para se projetar arquiteturas de software distribuído, baseadas em comunicação via rede.

REST é um dos modelos de arquitetura que foi descrito por Roy Fielding, um dos principais criadores do protocolo HTTP, em sua tese de doutorado e que foi adotado como o modelo a ser utilizado na evolução da arquitetura do protocolo HTTP.

Muitos desenvolvedores perceberam que também poderiam utilizar o modelo REST para a implementação de Web Services, com o objetivo de se integrar aplicações pela Web, e passaram a utilizá-lo como uma alternativa ao SOAP.

REST na verdade pode ser considerado como um conjunto de princípios, que quando aplicados de maneira correta em uma aplicação, a beneficia com a arquitetura e padrões da própria Web.

REST não é um bicho de sete cabeças. 

Possui apenas alguns poucos princípios e restrições que devem ser utilizados para se garantir algumas características importantes em aplicações e serviços, tais como: **portabilidade, escalabilidade e desacoplamento**.

A Web é o principal exemplo de implementação do modelo REST, e deveríamos nos espelhar nela ao construir nossos serviços seguindo esse mesmo modelo.

Todos os conceitos do modelo REST descritos nesse post podem também ser utilizados na implementação de aplicações Web, e não somente nos casos de integração de sistemas via Web Services.

Inclusive se você utilizar esses conceitos em uma aplicação Web tradicional, e um dia ela precisar se tornar uma API REST, o impacto das mudanças será mínimo, pois sua aplicação já estará seguindo os princípios REST. 

O que mudará é que agora ao invés de devolver para os clientes apenas páginas HTML ela também pode devolver as informações dos recursos em algum formato, como o JSON, e o cliente é quem vai se preocupar em como formatá-los.

Quando uma aplicação ou serviço segue os princípios descritos nesse artigo, ela é chamada de RESTful. 

Alguns puristas consideram apenas como RESTful a aplicação ou serviço que seguir todos os princípios do REST, inclusive os menos utilizados, como comunicação Stateless e HATEOAS.

Mas, não foque em ser ou não considerado RESTful, e sim em tentar utilizar o máximo possível dos princípios REST, para que sua aplicação ou serviço obtenha todos os benefícios desse modelo.

