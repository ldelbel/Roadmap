# Representações dos recursos

Os recursos ficam armazenados pela aplicação que os gerencia. 

Quando são solicitados pelas aplicações clientes, por exemplo em uma requisição do tipo GET, eles não “abandonam” o servidor, como se tivessem sido transferidos para os clientes. 

Na verdade, o que é transferido para a aplicação cliente é apenas uma representação do recurso.

Um recurso pode ser representado de diversas maneiras, utilizando-se formatos específicos, tais como XML, JSON, HTML, CSV, dentre outros.

A comunicação entre as aplicações é feita via transferência de representações dos recursos a serem manipulados.

Uma representação pode ser também considerada como a indicação do estado atual de determinado recurso.

Essa comunicação feita via transferência de representações dos recursos gera um desacoplamento entre o cliente e o servidor, algo que facilita bastante a manutenção das aplicações.

# Suporte diferentes representações

É considerada uma boa prática o suporte a múltiplas representações em um serviço REST, pois isso facilita a inclusão de novos clientes. 

Ao suportar apenas um tipo de formato, um serviço REST limita seus clientes, que deverão se adaptar para conseguir se comunicar com ele.

Os três principais formatos suportados pela maioria dos serviços REST são:

* HTML;
* XML;
* JSON.

# Utilize Content Negotiation para o suporte de múltiplas representações

Quando um serviço REST suporta mais de um formato para as representações de seus recursos, é comum que ele espere que o cliente forneça a informação de qual o formato desejado. 

No REST, essa negociação do formato da representação dos recursos é chamada de Content Negotiation e no mundo Web ela deve ser feita via um cabeçalho HTTP, conhecido como accept.

Ao fazer uma chamada ao serviço REST, um cliente pode adicionar na requisição o cabeçalho accept, para indicar ao servidor o formato desejado da representação do recurso. Claro, deve ser um formato que seja suportado pelo serviço REST.
