# Códigos HTTP

Na verdade, esse não é um princípio do REST, mas sim uma boa prática.

No protocolo HTTP, toda requisição feita por um cliente a um servidor deve resultar em uma resposta, sendo que nela existe um código HTTP, utilizado para informar o resultado da requisição, tenha ela sido processada com sucesso ou não.

Existem dezenas de códigos HTTP, cada um tendo sua semântica especifica e devendo ser utilizado quando fizer sentido. Os códigos HTTP são agrupados em classes, conforme demonstrado a seguir:

| Classe |Semântica  |
|--|--|
| 2xx |	Indica que a requisição foi processada com sucesso.
| 3xx |	Indica ao cliente uma ação a ser tomada para que a requisição possa ser concluída.
|4xx|Indica erro(s) na requisição causado(s) pelo cliente.
|5xx |	Indica que a requisição não foi concluída devido a erro(s) ocorrido(s) no servidor.

A boa prática consiste em conhecer os principais códigos HTTP e utilizá-los de maneira correta. 

Veja os principais códigos HTTP e quando os utilizar:

| Código |Descrição  | 	Quando utilizar
|--|--|--|
| 200 |	OK| Em requisições GET, PUT e DELETE executadas com sucesso.
| 201 |	Created | Em requisições POST, quando um novo recurso é criado com sucesso.
|206|Partial Content| Em requisições GET que devolvem apenas uma parte do conteúdo de um recurso.
|302 |	Found|Em requisições feitas à URI’s antigas, que foram alteradas.
|400 |	Bad Request	|	Em requisições cujas informações enviadas pelo cliente sejam invalidas.
|401 |	Unauthorized|Em requisições que exigem autenticação, mas seus dados não foram fornecidos.
|403 |Forbidden	|	Em requisições que o cliente não tem permissão de acesso ao recurso solicitado.
|404 |Not Found|		Em requisições cuja URI de um determinado recurso seja inválida.
|405 |Method Not Allowed	|Em requisições cujo método HTTP indicado pelo cliente não seja suportado.
|406 |Not Acceptable	|	Em requisições cujo formato da representação do recurso requisitado pelo cliente não seja suportado.
|415 |	Unsupported Media Type	|		Em requisições cujo formato da representação do recurso enviado pelo cliente não seja suportado.
|429 |	Too Many Requests|		No caso do serviço ter um limite de requisições que pode ser feita por um cliente, e ele já tiver sido atingido.
|500 |Internal Server Error| 	Em requisições onde um erro tenha ocorrido no servidor.
|503 |	Service Unavailable	| 		Em requisições feitas a um serviço que esta fora do ar, para manutenção ou sobrecarga.

Utilize o código correto para cada tipo de situação. 

Evite a má prática de sempre utilizar um mesmo código genérico para todas as situações, como por exemplo o código 200 para qualquer tipo de requisição bem-sucedida ou o código 500 para qualquer requisição malsucedida.
