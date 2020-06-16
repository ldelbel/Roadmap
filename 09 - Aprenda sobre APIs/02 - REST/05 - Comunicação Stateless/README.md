# Comunicação Stateless

A Web é o principal sistema que utiliza o modelo REST. Hoje ela suporta bilhões de clientes conectados e trocando informações. 

Mas, como é possível a Web ter uma escalabilidade e performance tão boas, a ponto de conseguir suportar tamanho número de clientes sem problemas?

A resposta: **Comunicação Stateless.**

Requisições feitas por um cliente a um serviço REST devem conter todas as informações necessárias para que o servidor as interprete e as execute corretamente. 

Clientes não devem depender de dados previamente armazenados no servidor para processar uma requisição. 

Qualquer informação de estado deve ser mantida pelo cliente e não pelo servidor. Isso reduz a necessidade de grandes quantidades de recursos físicos, como memória e disco, e também melhora a escalabilidade de um serviço REST.

É justamente por essa característica que a Web consegue ter uma escalabilidade praticamente infinita, pois ela não precisa manter as informações de estado de cada um dos clientes.

Esse é um dos princípios mais difíceis de ser aplicado em um serviço REST, pois é muito comum que aplicações mantenham estado entre requisições de clientes. 

Um exemplo dessa situação acontece quando precisamos armazenar os dados dos usuários que estão autenticados na aplicação.
