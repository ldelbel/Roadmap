# SOAP

Em uma breve descrição, SOAP é uma tecnologia desenvolvida pela Microsoft para acessar web services unicamente por meio de mensagens de requisições e respostas feitas em XML, substituindo as tecnologias que utilizavam mensagens binárias. 

Além das mensagens, utiliza-se XML para criar o arquivo WSDL (Web Service Description Language), que é um contrato entre o provedor e o consumidor do serviço, como se fosse uma assinatura de método para o serviço web.

> WSDL é um a descrição em formato XML de um Web Service que utilizará SOAP / RPC como protocolo. É o acrônimo de Web Services Description Language (Linguagem de Descrição de Serviços Web).

> RPC — Remote Procedure Calls (em português, chamada de procedimentos remotos) é um modelo que define a forma como são realizadas as chamadas a operações remotas através de web services.

Outra característica do SOAP é que é independente do protocolo de transporte, ou seja, pode ser enviado com a maioria dos protocolos, por exemplo HTTP, SMTP, TCP e JMS.

Características gerais: 

* Protocolo de transporte independente (REST utiliza somente HTTP)
* Trabalha melhor com sistemas distribuídos, pois REST trabalha com comunicação ponto-a-ponto
* O arquivo WSDL pode gerar um certo tipo de automação quando usado com determinadas ferramentas

# 1. WSDL

Por meio de um WSDL você informa ao cliente como cada serviço em um end-point deve ser invocado: quais os parâmetros e tipo de dados de cada parâmetro é esperado, e qual o tipo de dado do retorno será enviado como resposta.

Além de descrever cada serviço (que pode ser comparado analogamente à um método a ser executado no programa servidor), também descreve como podem ser encontrados. Seus elementos básicos são:

| Elemento  | Descrição  |
|--|--|
|`<types>`|  aqui deverão ser descritos os tipos de dados suportados pelo serviço em questão|
|`<message>`|aqui devem ser especificados os padrões de entrada e saída de dados dos web services |
| `<portType>` | aqui devem ser descritos os agrupamentos lógicos das operações. São as operações executadas pelo web service |
| `<binding>` | aqui devem ser apresentados os protocolos de comunicação que os web services utilizam  |
| `<operation>`  |  região que permite a especificação das assinaturas dos métodos disponibilizados |
| `<definitions>` | elemento padrão de todos os documentos WSDL. Permite efetuar descrições sobre schemas e namespaces |

Quando o WSDL é utilizado diretamente quando um cliente realiza uma chamada de serviço por meio de SOAP. Primeiramente ele solicita o WSDL para entender como se dará esta negociação.

## 1.1. Elementos

### 1.1.1. `<definitions>`

É o elemento raiz de qualquer documento WSDL. Ele contém atributos que servem para definir os namespaces utilizados no documento WSDL.

### 1.1.2. `<types>`
O elemento types contém os tipos de dados que estão presentes na mensagem.
~~~
<wsdl:part name=”endereco” type=”xsd:string” />
<wsdl:part name=”numero” type=”xsd:int” />
~~~
  
### 1.1.3. `<message>`

O elemento message define os dados a serem transmitidos. Cada elemento message recebe um ou mais elementos <part>, que formam as partes reais da mensagem.
O elemento <part> define o conteúdo da mensagem representando os parâmetros que são passados e a resposta que o serviço retorna.

~~~ 
<wsdl:message name=”getCidade”>
<wsdl:part name=”cidade” type=”xsd:string” />
</wsdl:message>
<wsdl:message name=”getCidadeResponse”>
<wsdl:part name=”getCidadeReturn” type=”xsd:string” />
</wsdl:message>
~~~ 

### 1.1.4. `<import>`

O elemento import funciona como separação entre as várias partes de uma definição WSDL. Ele possui dois atributos, os quais definem a localização do documento importado e o seu namespace.

~~~
<import 
namespasce=”http://www.cidade.com/definitions/CidadeRemoteInterface”
location=”http://localhost/esdl/Cidade-interface.wsdl/” 
/>
~~~ 

### 1.1.5. `<operation>` e `<portType>`

Os elementos portType possuem um conjunto de operações `<operation>`, as quais possuem um atributo name e um atributo opcional para especificar a ordem dos parâmetros usados nas operações.

**Tipos de mensagens de operações

| Tipo de operação | Descrição |
|--|--|
|Operação unidirecional |Define uma mensagem enviada de um cliente para um serviço, sem resposta. |
| Solicitação-Resposta | O mais utilizado. O cliente envia uma solicitação a um serviço, e recebe como resultado uma mensagem de resposta com o resultado dessa solicitação. Pode ser vista como um RPC (remote procedure call).|
|  Pedido-Resposta | Não utilizada freqüentemente. Define uma mensagem enviada do serviço para o cliente, resultando em uma mensagem enviada do cliente de volta para o serviço. |
| Notificação | É quando o serviço envia uma mensagem para o cliente |

### 1.1.6. `<binding>`

O elemento binding mapeia os elementos operation em um elemento portType, para um protocolo especifico. 

Ele associa o elemento portType ao protocolo SOAP, utilizando-se de um elemento de extensão SOAP chamado `<wsdlsoap:binding>`, através de dois parâmentos: protocolo de transporte e o estilo da requisição (rpc ou document).

~~~
<wsdl:binding name=”CidadeSoapBinding” type=”impl:Cidade”>
<wsdlsoap:binding style=”rpc” transport=http://schemas.xmlsoap.org/soap/http />
~~~

### 1.1.7. `<service>` e `<port>`

Os elementos service e port definem a localização real do serviço, tendo em vista que o mesmo pode conter varias portas e cada uma delas é especifica para um tipo de ligação, descrita no elemento binding.

~~~
<wsdl:service name=”ConsultaCidadeService”>
<wsdl:port binding=”impl:ConsultaCidadeSoapBinding” name=”ConsultaCidade”>
<wsdlsoap:address location=http://localhost/wsdl/ConsultaCidadeServer.php/>
</wsdl:port>
</wsdl:service>
~~~
