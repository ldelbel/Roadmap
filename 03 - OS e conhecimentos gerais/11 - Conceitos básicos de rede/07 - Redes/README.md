# Principais termos de Redes

## Alias

Significa segundo nome ou apelido. Pode referenciar um endereço eletrônico alternativo de uma pessoa ou grupo de pessoas, ou um segundo nome de uma máquina. É também um dos comandos básicos do UNIX.

## Bridge

Um dispositivo que conecta duas ou mais redes de computadores transferindo, seletivamente, dados entre ambas.

## Cliente

É um processo ou programa que requisita serviços a um servidor.

## DHCP 

Dynamic Host Configuration Protocol (protocolo de configuração dinâmica de host), é um protocolo de serviço TCP/IP que oferece configuração dinâmica de terminais, com concessão de: 

* endereços IP de host
* máscara de sub-rede 
* default gateway (gateway padrão)
* número IP de um ou mais servidores DNS
* sufixos de pesquisa do DNS
* número IP de um ou mais servidores WINS

O DHCP usa um modelo **cliente-servidor.MAC:001A3FF02A2F

Resumidamente, o DHCP opera da seguinte forma:

1. Quando um computador (ou outro dispositivo) conecta-se a uma rede, o host/cliente DHCP envia um pacote UDP em broadcast (destinado a todas as máquinas) com uma requisição DHCP (para a porta 68);

2. Qualquer servidor DHCP na rede pode responder a requisição. O servidor DHCP mantém o gerenciamento centralizado dos endereços IP usados na rede e informações sobre os parâmetros de configuração dos clientes como gateway padrão, nome do domínio, servidor de nomes e servidor de horário. Os servidores DHCP que capturarem este pacote responderão (se o cliente se enquadrar numa série de critérios — ver abaixo) para a porta 68 do host solicitante com um pacote com configurações onde constará, pelo menos, um endereço IP e uma máscara de rede, além de dados opcionais, como o gateway, servidores de DNS, etc.

### Terminologia

#### Cliente DHCP

É qualquer dispositivo de rede capaz de obter as configurações do TCP/IP a partir de um servidor DHCP. Por exemplo, uma estação de trabalho com o Microsoft Windows 10, uma estação com qualquer distribuição Linux, uma impressora com placa de rede habilitada ao DHCP, etc.
  
#### Escopo 

Um escopo é o intervalo consecutivo completo dos endereços IP possíveis para uma rede (por exemplo, a faixa de 10.10.10.100 a 10.10.10.150, na rede 10.10.10.0/255.255.255.0). Em geral, os escopos definem uma única sub-rede física, na rede na qual serão oferecidos serviços DHCP. Os escopos também fornecem o método principal para que o servidor gerencie a distribuição e atribuição de endereços IP e outros parâmetros de configuração para clientes na rede, tais como o default gateway, servidor DNS e assim por diante.

#### Intervalo de exclusão

Um intervalo de exclusão é uma sequência limitada de endereços IP dentro de um escopo, excluído dos endereços que são fornecidos pelo DHCP. Os intervalos de exclusão asseguram que quaisquer endereços nesses intervalos não são oferecidos pelo servidor para clientes DHCP na sua rede. Por exemplo, dentro da faixa 10.10.10.100 a 10.10.10.150, na rede 10.10.10.0/255.255.255.0 de um determinado escopo, pode-se criar uma faixa de exclusão de 10.10.10.120 a 10.10.10.130. Os endereços da faixa de exclusão não serão utilizados pelo servidor DHCP para configurar os clientes DHCP.

#### Pool de endereços

Após definir um escopo DHCP e aplicar intervalos de exclusão, os endereços remanescentes formam o pool de endereços disponíveis dentro do escopo. Endereços em pool são qualificados para atribuição dinâmica pelo servidor para clientes DHCP na sua rede. No nosso exemplo, onde temos o escopo com a faixa 10.10.10.100 a 10.10.10.150, com uma faixa de exclusão de 10.10.10.120 a 10.10.10.130, o nosso pool de endereços é formado pelos endereços de 10.10.10.100 a 10.10.10.119, mais os endereços de 10.10.10.131 a 10.10.10.150.

#### Servidor DHCP 

É um servidor onde foi instalado e configurado o serviço DHCP. Em Microsoft Windows, após a instalação de um servidor DHCP ele precisa ser autorizado no Active Directory, antes que possa efetivamente atender pedidos de clientes. O procedimento de autorização no Active Directory é uma medida de segurança, para evitar que servidores DHCP sejam introduzidos na rede sem o conhecimento do administrador da rede. Além do Windows Server, o serviço de DHCP também pode ser instalado nas distribuições Linux, como o serviço DHCP3 Server, pacote já presente na maioria das distribuições servidoras de Linux. 

## Domínio

É uma parte da hierarquia de nomes da Internet – DNS -, que permite identificar as instituições ou conjunto de instituições na rede.

Sintaticamente, um nome de domínio da Internet consiste de uma seqüência de nomes separados por pontos(.) . Por exemplo: ci.rnp.br.

Neste caso, dentro do domínio ci.rnp.br, o administrador do sistema pode criar diferentes grupos como info.ci.rnp.br ou staff.ci.rnp.br, conforme a necessidade.

## DNS - Domain Name System

O DNS (Domain Name System) é um sistema de gerenciamento de nomes hierárquico e distribuído para computadores, serviços ou qualquer recurso conectado à Internet ou em uma rede privada. Ele se baseia em nomes hierárquicos e permite a inscrição de vários dados digitados além do nome do host e seu endereçamento IP. 

Faz parte do protocolo TCP/IP

Exemplo: 

> Se escrever na barra de URL  “http://74.125.224.72/” (sem aspas) vai até ao site de pesquisa da Google. É o mesmo que escrever “http://google.com” (sem aspas). Ou seja, quando escrever “http://google.com”, um servidor DNS entre em funcionamento e traduz esse endereço para o IP “74.125.224.72”, que é o **endereço da máquina** onde está hospedado o site de pesquisa da Google.

Para saber qual o endereço IP de qualquer site, basta abrir o MS-DOS e digitar “ping www.seusite.com.br“

## Endereço IPV4 (Inet4 no ubuntu)

Endereço IP como um número de 32 bits.

## Endereço IPV6 (Inet6 no ubuntu)

Endereço IP como um número de 128 bits.

## Ethernet 

Um padrão muito usado para a conexão física de redes locais. Descreve: 

* protocolo 
* cabeamento 
* topologia
* mecanismos de transmissão.

## Firewall

Um Firewall é um software ou hardware que bloqueia determinados tipos de acessos. Por exemplo, um firewall pode bloquear o tráfego de entrada de uma determinada porta. Pode-se também, bloquear totalmente o tráfego de entrada e liberar apenas as provenientes de um endereço IP específico.

## Gateway 

1. Sistema que possibilita o intercâmbio de serviços entre redes com tecnologias completamente distintas, como FidoNet e Internet; 
2. Sistema e convenções de interconexão entre duas redes de mesmo nível e idêntica tecnologia, mas sob administrações distintas. 
3. Roteador (terminologia TCP/IP).

Dispositivos host em uma organização geralmente se referem à rota padrão (Default Route) com um **gateway padrão** (Default Gateway) que pode ser, e geralmente é, um dispositivo de filtro como um Firewall ou um servidor Proxy.Também podem ser resumido em, parte da configuração DHCP visto como 0.0.0.0.

Os computadores dos usuários de Internet e os computadores que servem páginas para usuários são nós de rede, uma vez que os nós que conectam as redes entre elas são gateways. 

Por exemplo 
> Os computadores que controlam o tráfego entre redes de empresas ou os computadores usados pelos provedores de serviço de internet para conectar usuários à Internet são nós de gateway.

Na rede para uma empresa, um computador servidor que age como um nó de gateway está frequentemente agindo também como um servidor proxy e um servidor firewall. Um gateway é frequentemente associado com um roteador, que conhece onde direcionar um determinado pacote de dados que é recebido no gateway e comutá-lo, o que fornece o caminho de entrada e saída real do gateway para um determinado receptáculo.

Exemplos de gateway podem ser os routers (ou roteadores) e firewalls,[1] já que ambos servem de intermediários entre o utilizador e a rede. Um proxy também pode ser interpretado como um gateway (embora em outro nível, aquele da camada em que opera), já que serve de intermediário também.

Cabe igualmente ao gateway traduzir e adaptar os pacotes originários da rede local, para que esses possam atingir o destinatário, e, também, traduzir às respostas e devolvê-las ao par local da comunicação. Assim, é frequente a utilização de protocolos de tradução de endereços, como a NAT, a qual é uma das mais simples formas de implementações de gateways.

O gateway recolhe o dado de um ambiente, retira a pilha de protocolos antiga e, o reencapsula com a pilha de protocolos da rede destino.

## IP 
O Internet Protocol é o protocolo responsável pelo **roteamento de pacotes** entre dois sistemas que utilizam a família de protocolos TCP/IP, desenvolvida e usada na Internet. É considerado o mais importante dos protocolos em que a Internet é baseada.

## Localhost

O nome localhost sempre corresponde ao dispositivo que você está usando. O endereço “http://localhost“, na verdade corresponde ao endereço IPv4 “127.0.0.1” e IPv6 “::1“.

## MAC ou Hardware Address

Um endereço de controle de acesso à mídia (endereço MAC) de um dispositivo é um identificador único atribuído a uma interface de rede.

Os endereços MAC são usados na subcamada de protocolo do controle de acesso ao meio da camada de enlace de dados. Como normalmente representado, os endereços MAC são reconhecíveis como seis grupos de dois dígitos hexadecimais, separados por hífens, dois pontos ou nenhum separador (consulte as Convenções de notação abaixo).

Outros nomes: 
* endereço gravado 
* endereço de hardware Ethernet 
* endereço de hardware
* endereço físico

## Máscara de rede

### Máscara de rede

A máscara de rede padrão acompanha a classe do endereço IP: num endereço de classe A, a máscara será 255.0.0.0, indicando que o primeiro octeto se refere à rede e os três últimos ao host. Num endereço classe B, a máscara padrão será 255.255.0.0, onde os dois primeiros octetos referem-se à rede e os dois últimos ao host, e num endereço classe C, a máscara padrão será 255.255.255.0 onde apenas o último octeto refere-se ao host.

Os 32 bits das máscaras de sub-rede são divididos em duas partes: um primeiro bloco de 1s, indicando a parte do endereço IP que pertence à rede, seguido por um bloco de 0s, indicando a parte que pertence ao host.

Normalmente, as máscaras de sub-rede são representadas com quatro números de 0 a 255 separados por pontos. A máscara 255.255.255.0 (ou, em binário, 11111111.11111111.11111111.00000000).

Embora normalmente as máscaras de sub-rede sejam representadas em notação decimal, é mais fácil entender seu funcionamento usando a notação binária. Para determinar qual parte de um endereço é o da rede e qual é o do host, um dispositivo deve realizar a operação AND.

### Máscara de sub-rede

Uma máscara de sub-rede, também conhecida como subnet mask ou netmask, é um número de 32 bits usado em um IP para separar a parte correspondente à rede pública, à sub-rede e aos hosts.

Uma sub-rede é uma divisão de uma rede de computadores. A divisão de uma rede grande em menores resulta num tráfego de rede reduzido, administração simplificada e melhor performance de rede. No IPv4 uma sub-rede é identificada por seu endereço base e sua máscara de sub-rede.

|  | Endereço Decimal | Binário |
|--|--|--|
| Endereço completo |	192.168.5.10 |11000000.10101000.00000101.00001010  |
| Máscara da sub-rede | 255.255.255.0 | 11111111.11111111.11111111.00000000|
| Porção da rede |192.168.5.0  | 11000000.10101000.00000101.00000000 |

## NAT

Em redes de computadores, Network Address Translation (NAT), também conhecido como masquerading, é uma técnica que consiste em reescrever, utilizando-se de uma tabela hash, os endereços IP de origem de um pacote que passam por um router ou firewall de maneira que um computador de uma rede interna tenha acesso ao exterior ou Rede Mundial de Computadores.

Por se tratar de uma rede privada, os números de IP interno da rede (como 10.0.0.0/8, 172.16.0.0/12 e 192.168.0.0/16) nunca poderiam ser passados para a Internet pois não são roteados nela e o computador que recebesse um pedido com um desses números não saberia para onde enviar a resposta. Sendo assim, os pedidos teriam de ser gerados com um IP global do router. 

Mas quando a resposta chegasse ao router, seria preciso saber a qual dos computadores presentes na LAN pertencia aquela resposta.

A solução encontrada foi fazer um mapeamento baseado no IP interno e na porta local do computador. Com esses dois dados o NAT gera um número de 16 bits usando a tabela hash, este número é então escrito no campo da porta de origem.

O pacote enviado para fora leva o IP global do router e na porta de origem o número gerado pelo NAT. Desta forma o computador que receber o pedido sabe para onde tem de enviar a resposta. Quando o router recebe a resposta faz a operação inversa, procurando na sua tabela uma entrada que corresponda aos bits do campo da porta. Ao encontrar a entrada, é feito o direcionamento para o computador correto dentro da rede privada.

Esta foi uma medida de reação face à previsão da exaustão do espaço de endereçamento IP, e rapidamente adaptada para redes privadas também por questões econômicas (no início da Internet os endereços IP alugavam-se, quer individualmente quer por classes/grupos).

Um computador atrás de um router gateway NAT tem um endereço IP dentro de uma gama especial, própria para redes internas. Como tal, ao ascender ao exterior, o gateway seria capaz de encaminhar os seus pacotes para o destino, embora a resposta nunca chegasse, uma vez que os routers entre a comunicação não saberiam reencaminhar a resposta (imagine-se que um desses routers estava incluído em outra rede privada que, por ventura, usava o mesmo espaço de endereçamento). 

Duas situações poderiam ocorrer: ou o pacote seria indefinidamente reencaminhado, ou seria encaminhado para uma rede errada e descartado.

As entradas no NAT são geradas apenas por pedidos dos computadores de dentro da rede privada. Sendo assim, um pacote que chega ao router vindo de fora e que não tenha sido gerado em resposta a um pedido da rede, ele não encontrará nenhuma entrada no NAT e este pacote será automaticamente descartado, não sendo entregue a nenhum computador da rede. Isso impossibilita a entrada de conexões indesejadas e o NAT acaba funcionando como um firewall.

## NIS

Acrônimo para Network Information System (NIS), é um sistema distribuído de bases de dados que troca cópias de arquivos de
configuração unindo a conveniência da replicação à facilidade de gerência centralizada. Servidores NIS gerenciam as cópias de arquivos de bases de dados, e clientes NIS requerem informação dos servidores ao invés de usar suas cópias locais destes arquivos. É muito usado por administradores UNIX para gerenciar bases de dados distribuídas através de uma rede.

## NFS 

O Network File System, desenvolvido pela Sun Microsystems Inc., é um protocolo que usa IP para permitir o compartilhamento de arquivos entre computadores.

## Nó

Qualquer dispositivo, inclusive servidores e estações de trabalho, ligado a uma rede.

## OSI

O Open Systems Interconnection (OSI) é um modelo conceitual de protocolo com sete camadas definido pela ISO, para a compreensão e o projeto de redes de computadores. 

Trata-se de uma padronização internacional para facilitar a comunicação entre computadores de diferentes fabricantes.

## Pacote

Um pacote é uma unidade de dados enviados entre dispositivos. Quando você acessa uma página na Internet, o seu computador envia pacotes para o servidor web solicitando pacotes de dados para montar a página. O servidor web responde com esses pacotes e o seu navegador monta a página.

## Ping

Quando fazemos um teste de ping (como mostrado na parte DNS ), o computador dispara um pacote de 32 bytes de dados e aguarda a resposta. 

## Port

Quando uma aplicação deseja enviar ou receber tráfego, tem que usar uma porta. As portas numeradas de 1 a 65535 são usadas para receber ou enviar esse tráfego. Cada aplicação usa uma porta e é por isso que é possível saber o que cada aplicativo está usando da rede.

O padrão HTTP usa a porta 80. Quando você se conecta ao http://www.guiadopc.com.br, você está fazendo uma conexão HTTP pela porta 80.

Tente acessar o Guia do PC usando outra porta. Por exemplo, digite no seu navegador “https://guiadopc.com.br:81“. Se o nosso site não abrir é porque o servidor web não está respondendo à porta 81.

## PPP

Um dos protocolos mais conhecidos para acesso via interface serial, permite que um computador faça uso do TCP/IP através de uma linha telefônica convencional e um modem de alta velocidade. É considerado o sucessor do SLIP por ser mais confiável e eficiente.

## Protocolos – TCP, UDP, ICMP e etc
Os protocolos são diferentes formas de comunicação através da Internet. TCP e UDP são os mais comumente usados. Diferentes protocolos são ideais para diferentes tipos de comunicação.

## Route

Uma rota padrão (Default Route), também conhecida como “gateway de último recurso”, é a rota de rede utilizada por um roteador quando não há nenhuma outra rota conhecida existente para o endereço de destino de um pacote IP. 

Todos os pacotes para destinos desconhecidos pela tabela do roteador são enviados para o endereço de rota padrão. Esta rota geralmente direciona para outro roteador, que trata o pacote da mesma forma: Se a rota é conhecida, o pacote será direcionado para a rota conhecida. Se não, o pacote é direcionado para o “default route” desse roteador que geralmente direciona a outro roteador. E assim sucessivamente.

Assim que um roteador com uma rota conhecida para o destino de host é localizado, o roteador determina que rota é válida para localizar o resultado “mais específico”. A rede com a mais longa máscara de subrede correspondente ao endereço IP, vence.

---
As rotas funcionam assim: Elas fornecem instruções para um destino. Digamos que seu destino seja 192.168.10.x e sua rede local seja 192.168.1.x. 

Cada dispositivo tem uma rota padrão (0.0.0.0/0) e identifica se esse destino não está na mesma sub-rede (192.168.1.x) (**local**) e usa a rota padrão através do gateway padrão. Esse gateway padrão informará ao dispositivo A como chegar à rede remota através de um próximo salto. (Se você fizer uma rota de rastreamento para 8.8.8.8, isso fará mais sentido).

Esse processo se repete até você chegar ao destino final ou até que ele não atinja esse destino. Com o TCP, para que a comunicação ocorra, é necessário que as informações fluam nos dois sentidos, para que o extremo oposto (dispositivo B) também precise de uma rota de volta ao dispositivo A.

Uma rota estática apenas muda as direções. Em vez de passar pelo gateway padrão, você pode enviar a comunicação para outro dispositivo dentro da sub-rede, como o computador com Windows.

Exemplo: 

* VM do Windows em 192.168.1.70
* host do Linux em 192.168.1.69
* o roteador / gateway padrão é 192.168.1.1
* recursos remotos na rede 10.10.10.x.

Normalmente, quando o Linux ou o Windows VM se comunica com o mundo externo, ele usa a rota de gateway padrão para iniciar o próximo salto. Depois de iniciar um cliente vpn no windows vm, ele geralmente adiciona um novo gateway padrão substituto. Isso significa que a comunicação que não está na rede 192.168.1.x passa pela VPN.

Portanto, se você adicionar uma rota estática no host do Linux para acessar recursos, adicione uma caixa estática para Linux que indique qualquer coisa que vá para 10.10.10.x. O gateway será 192.168.1.70, quando o pacote for recebido e o compartilhamento de internet ativado, ele deve rotear esse pacote para o recurso remoto usando NAT. 

Se isso acontecer, não haverá problema. Caso contrário, o pacote provavelmente será descartado porque talvez não saiba como voltar sem uma rota estática no outro extremo.

Tudo isso depende do tipo de cliente e servidor vpn envolvido e da configuração de roteament

## UDP

Acrônimo para User Datagram Protocol, o protocolo de transporte sem conexão da família TCP/IP, usado com aplicações como o de gerenciamento de redes (SNMP) e de serviço de nomes (DNS).

## WAN [Rede de longa distância]

Acrônimo de Wide Area Network, uma rede que interliga computadores distribuídos em áreas geograficamente separadas.

