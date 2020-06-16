# Protocolo TCP/IP e UDP

Ao conectar um computador à uma rede de Internet interna ou externa, ele passa a ser identificado por um IP (Internet Protocol), ou Protocolo de Internet. O endereço de IP é único para cada computador da rede. 

# 1. IP

## 1.1. IP externo

O endereço de IP externo serve para identificar um dispositivo conectado à rede mundial de computadores, a Internet. 

Trata-se de um endereço único porém dinâmico: não existe mais de um computador com o mesmo endereço de IP conectado, mas o IP do seu modem pode ser alterado.

## 1.2. IP interno 

É utilizado na identificação de um computador, tablet ou celular ligado à uma rede interna, também conhecida como Intranet. 

O endereço de IP interno pode ser configurado como fixo ou gerenciado pelo roteador, que evita conflitos (mais de um dispositivo com o mesmo IP). 

## 1.3. IPs reservados

Na arquitetura para endereçamentos da Internet, uma rede privada (private network) é uma rede que usa o espaço privado de endereços IP, seguindo os padrões estabelecidos pela RFC 1918 para redes IPv4 e RFC 4193 para IPv6.

A IANA (Internet Assigned Numbers Authority) reserva blocos de endereços IP para uso em redes internas, sendo um bloco para redes classe A, um para classe B e outro para classe C, como segue:

- 10.0.0.0 até 10.255.255.255
- 172.16.0.0 até 172.31.255.255
- 192.168.0.0. até 192.168.255.255

As redes privadas são comuns nos escritórios (LAN), pois não há a necessidade de que todos os computadores de uma organização possuam um IP universalmente endereçável. 

Outra razão que torna importante os IPs privados, é o **número limitado de IPs públicos** (afinal, imagine se todos os computadores tivessem um endereço único). O IPv6 foi criado para resolver este último problema.

Os Roteadores são configurados para descartar qualquer tráfego que use um IP privado. 

Este isolamento garante que uma rede privada tenha uma maior segurança pois não é possível, em geral, ao mundo externo criar uma conexão direta a uma máquina que use um IP privado. 

Como as conexões não podem ser feitas entre diferentes redes privadas por meio da internet, diferentes organizações podem usar a mesma faixa de IP sem que haja conflitos (ou seja, que uma comunicação chegue acidentalmente a um elemento que não deveria).

### 1.3.1. Interface de loopback

Uma interface de loopback é uma interface de rede virtual que permite que um cliente e um servidor no mesmo host se comuniquem entre si usando a pilha de protocolos TCP/IP.

Para a interface de loopback é reservado todo o bloco de endereços IP classe A com identificação de rede 127.0.0.0/8, e por convenção, a maioria dos sistemas atribuem o endereço IP 127.0.0.1 a esta interface (::1 em redes IPv6), além de usar o nome localhost para identificá-la.

# 2. Máscara de rede

Imagine que você mora em um prédio. No seu prédio há os apartamentos 212 e 223. Eles estão no mesmo andar? Vejamos as possibilidades: 

|  | 2 | 1 | 2 |
|--|--|--|--|
|Opção 1 | Andar | Bloco | Apartamento |
|Opção 2 | Andar | Andar | Apartamento |

Considerando a opção 1, teríamos: 
- Apartamento 1: segundo andar, bloco 1, apartamento 2. 
- Apartamento 2: segundo andar, bloco 2, apartamento 3. 

Considerando a opção 2, teríamos: 
- Apartamento 1: vigésimo primeiro andar, apartamento 2. 
- Apartamento 2: vigésimo segundo andar, apartamento 3. 

Trazendo para o exemplo de redes, quem definirá esta regra é a máscara de rede. 

Com 32 bits: 00000000.00000000.00000000.00000000

Temos dois IPs: 
- `192`.`168`.`0`.`1`;
- `192`.`168`.`0`.`190`. 

Supondo que tenha sido escolhida a regra: 
- três primeiros octetos para redes: `192`.`168`.`0`;
- último octeto para hosts: `1` e `190`. 

Temos aqui 256 possibilidades (`0` a `255`). Contudo são reservados: 
- IP de rede ou máscara de rede, que representa a rede: `192`.`168`.`0`.`0`;
- IP broadcast, para quando quisermos enviar uma mensagem para todos na rede: `192`.`168`.`0`.`255`. 

Assim, teremos possíveis 254 hosts. 

Agora imagine que sejam usados 25 bits para redes e 7 para hosts: 00000000.00000000.00000000.`0`0000000

Temos duas sub-redes, alternadas entre os bits `0` e `1`, destacado anteriormente:

| Sub-rede | IP de rede | IP broadcast | 
|--|--|--|
|`192`.`168`.`0`.`0` -> `192`.`168`.`0`.`127` | `192`.`168`.`0`.`0`  |`192`.`168`.`0`.`127` |
| `192`.`168`.`0`.`128` -> `192`.`168`.`0`.`255` | `192`.`168`.`0`.`128` | `192`.`168`.`0`.`255` |

Hosts = 2^n - `2`
 - n = número de bits
 - `2` = IPs reservados para `Ip de rede` e `Broadcast`. 
 
 Neste caso, representaremos esta rede como: `192`.`168`.`0`.`127`/`25`
  - `25` representa a máscara de rede = quantos bits foram reservados para a rede. Esta nomenclatura é denominada CIDIR.

Uma máscara de rede `/24`, será representada nas formas octal e decimal: 
- `11111111`.`11111111`.`11111111`.`00000000`;
- `255`.`255`.`255`.`0`.

[Vídeo - Teoria de máscaras de redes](https://www.youtube.com/watch?v=yLgansF_h1w)

## 2.1. Default masks

Há máscaras padrão para as sub-redes, de acordo com as classes das redes. 

![Default Submasks](http://www.tcpipguide.com/free/diagrams/ipsubnetdefaultmasks.png)

# 3. Gateway

Se um dispositivo em uma rede privada deve se comunicar com outras redes, é necessário que haja um "gateway" para garantir que a rede externa seja vista com um endereço que seja "real" (ou público) de maneira que o roteador permita a comunicação. 

Normalmente este gateway será um service NAT (‘’Network address translation’’) ou um Servidor Proxy. Isto, porém, pode causar problemas se a organização tentar conectar redes que usem os mesmos endereços privados.

Exemplo: 

Imagine que você possui o seguinte cenário:

Você é o host `192`.`168`.`0`.`0` e quer se comunicar com `192`.`168`.`0`.`10`, na rede `/24`. Assim como no exemplo do prédio, em que você não precisa de um elevador para ir a um apartamento no mesmo andar, aqui você não precisa de um gateway para acessar um host na mesma rede. 

Mas e se você quiser se comunicar com um computador externo, por exemplo: `200`.`200`.`200`.`200`?

O Gateway é a máquina que liga a minha rede a outras redes:
 - roteador;
 - modem; 
 - um servidor;
 - etc. 
 
É muito comum que um Gateway seja o primeiro IP da rede, como por exemplo: `192`.`168`.`0`.`1`. Quem define este valor? Quem estiver configurando a máquina. 

# 4. NAT - Network Adress Translator

## 4.1. NAT Direto

Imagine que seu provedor de Internet atribui ao meu roteador um endereço IP público, (por exemplo: 186.45.123.69). Este IP é único no mundo.

Porém, eu possuo cinco dispositivos que precisam acessar a Internet em minha rede interna. Como conseguir a conexão para todos se só possuo um endereço IP público?

Para resolver este problema, atribuo endereços IP privados (locais e reservados) aos meus dispositivos (PC, notebook, tablet, etc.), e compartilho o IP público único que possuo entre todos eles. Quem faz a atribuição desses IPs é o roteador, via DHCP, o qual também realiza o compartilhamento do IP público.

Em sua casa você pode ter também diversos dispositivos em sua rede doméstica acessando a Internet, cada um com um IP privado – e que podem ser os mesmos IPs privados que os equipamentos da minha rede! – pois o que importa para o acesso á Internet é o IP público atribuído, que será diferente do meu.

Esse processo de “compartilhamento” de endereços públicos para as estações da rede interna é chamado de NAT – Network Address Translation (Tradução de Endereços de Rede), no qual um endereço público é “traduzido” para endereços na rede interna, e vice-versa.

Note que os vários dispositivos em uma rede interna podem se comunicar entre si livremente, mas para acessarem a rede externa (no caso, Internet), precisarão do serviço de NAT presente no roteador.

## 4.2. DNAT - NAT do destino 

O DNAT serve quando você tiver uma estação na sua rede e para que remotamente você consiga acessar um serviço, por exemplo acessar via roteador. 

Quando você acessar um endereço externo, seu roteador irá enviar para o destino o endereço de IP válido e não o IP utilizado pelo seu dispositivo. 

Em resposta, ele irá contactar o IP válido que será trocado pelo IP do seu dispositivo. 

Caso você esteja necessitando de suporte remotamente, você pode utilizar um programa de acesso remoto como o VNC. Por padrão, esta porte é a 5900, pelo seu IP válido. Agora, como saber qual estação ele irá acessar? O encaminhamento (forwarding) será configurado pela interface web do roteador através do IP do roteador. 

Caso você não saiba qual é este IP, resete o roteador. 

Nas configurações, configure para que sempre que o roteador receber um pacote pela porta 5900, ele deve encaminhar para o VNC da estação em questão. O mesmo pode ser feito para um servidor web, servidor dns, etc. 

# 5. DHCP - Dinamic Host Configuration Protocol

Este protocolo é usado para a obtenção de IP automaticamente. 

Os programas que rodam uma estação farão uma requisição DHCP para algum servidor de rede. O servidor irá receber e responder a requisição com as informações de configuração: 

- IP;
- Máscara de rede; 
- Gateway; 
- DNS. 

Quem atribui isso é o cliente DHCP que fica na estação.  

Deve-se atentar a um servidor DHCP intermediário, feito por engano ou maliciosamente, implicando em vulnerabilidade da rede. 

# 6. Proxy

Proxy é o termo utilizado para definir os intermediários entre o usuário e seu servidor. E por isso desempenha a função de conexão do computador (local) à rede externa (Internet).

Todas as requisições feitas ao servidor (o site que você quer acessar) passarão pelo seu proxy. Ao chegar ao site, o IP (Internet Protocol / Protocolo de Internet) do proxy fica registrado no cache do seu destino e não o seu. 

É pelo IP que os hackers conseguem invadir computadores, portanto deve-se manter o nível de segurança do seu gateway (porta de ligação com o proxy) seguro. 

Os riscos são vários, no entanto, dois deles podem ser enumerados como os mais fortes: 
- ter seu computador invadido; 
- ter alguém navegando com o seu IP.

## 6.1. Web Proxy

Existe, ainda, um outro tipo de proxy, os web proxies. Eles são uma versão que esconde o seu IP real e lhe permite navegar anonimamente. Muitos deles são utilizados em redes fechadas como universidades e ambientes de trabalho para burlar uma determinação de bloqueio a alguns sites da internet. 

Os conteúdos campeões de bloqueio são: sites de relacionamento (Orkut, facebook e outros), programas de troca de mensagem instantânea (Msn Messenger, Yahoo! Messenger e outros), sem contar os tão proibidos sites de pornografia.

## 6.2. Open proxy

As conexões abertas de proxy  (open proxy) são o tipo mais perigoso e convidativo aos crackers e usuários mal intencionados. 

Quando um destes usuários consegue acessar um computador, instala um servidor proxy nele para que possa entrar quando quiser na máquina e promover diversos tipos de ilegalidade como scripts que roubam senhas de bancos, fraudes envolvendo cartões de crédito e uma grande variedade de atos ilegais.

## 6.3. Redes proxy

As redes proxy são baseadas em códigos criptados que permitem a comunicação anônima entre os usuários. 

Exemplo deste tipo de rede são as conexões P2P (peer to peer) em que um usuário se conecta ao outro sem saber sua identidade e trocam arquivos entre si. 

Estas redes se caracterizam por não permitirem o controle dos servidores, os usuários comuns é quem providenciam todo o conteúdo e os arquivos. 

Certamente, muitos destes computadores são usados por pessoas mal intencionadas com segundas intenções. 

# 7. TCP e UDP

## 7.1. TCP

O pacote TCP é considerado conexão garantida devido seu processo de conexão conhecido como 3 way handshake connection. A conexão TCP passa a ser monitorada desde que o primeiro pacote entra na rede para ser entregue. 

Isto significa que o protocolo TCP necessita fazer o acompanhamento do numero de seqüência do pacote, checksums etc.

### 7.1.1. Características

| Característica | Descrição |
|--|--|
| _Orientado à conexão_ | A aplicação envia um pedido de conexão para o destino e usa a "conexão" para transferir dados. Portanto, se faz necessário o estabelecimento de uma conexão, por meio de uma sequência de passos definida no protocolo para que os dois pontos da conexão possam interagir entre si.|
| _Handshake_ | Mecanismo de estabelecimento e finalização de conexão a três e quatro tempos, respectivamente, o que permite a autenticação e encerramento de uma sessão completa. O TCP garante que, no final da conexão, todos os pacotes foram bem recebidos. |
| _Ponto a ponto_ | uma conexão TCP é estabelecida entre dois pontos. A princípio, pacotes de broadcasting parecem violar esse princípio, mas o que ocorre é que é enviado um pacote com um endereço especial em seu cabeçalho que qualquer computador em sua rede pode responder a esse pacote, mesmo que não esteja explicitamente endereçado pra ele. |
|  _Confiabilidade_ | O TCP usa várias técnicas para proporcionar uma entrega confiável dos pacotes de dados que, dependendo da aplicação, gera uma grande vantagem que tem em relação ao  UDP. Aliado a outros fatores, o protocolo se mantém bastante difundido nas redes de computadores. O TCP permite a recuperação de pacotes perdidos, a eliminação de pacotes duplicados, a recuperação de dados corrompidos e pode recuperar a ligação em caso de problemas no sistema e na rede. |
| _Full duplex_  |É possível a transferência simultânea em ambas direções (cliente-servidor) durante toda a sessão. Apesar disso, em alguns momentos, o protocolo necessita que algum pacotes de dados cheguem para que se dê o envio de outros, o que limita as transmissões.  |
|  _Entrega ordenada_  | A aplicação faz a entrega ao TCP de blocos de dados com um tamanho arbitrário num fluxo (ou  _stream_) de dados, tipicamente em  octetos). O TCP parte estes dados em segmentos de tamanho especificado pelo valor MTU). Porém, a circulação dos pacotes ao longo da rede (utilizando um protocolo de encaminhamento, na camada inferior, como o  protocolo IP pode fazer com que os pacotes não cheguem ordenados. O TCP garante a reconstrução do  _stream_  no destinatário mediante os  _números de sequência_. |
| _Controle de fluxo_ | O TCP usa o campo janela ou  _window_  para controlar o fluxo. O receptor, à medida que recebe os dados, envia mensagens ACK (=Acknowledgement), confirmando a recepção de um segmento; como funcionalidade extra, estas mensagens podem especificar o tamanho máximo do  _buffer_  no campo (janela) do segmento TCP, determinando a quantidade máxima de bytes aceita pelo receptor. O transmissor pode transmitir segmentos com um número de bytes que deverá estar confinado ao tamanho da janela permitido: o menor valor entre sua capacidade de envio e a capacidade informada pelo receptor. |
| _Controle de congestionamento_ | Baseado no número de mensagens de reconhecimentos ACK (=Acknowledgement) recebidos pelo remetente por unidade de tempo calculada com os dados do tempo de ida e de volta, ou em inglês RTT, o protocolo prediz o quanto a rede está congestionada e diminui sua taxa de transmissão de modo que o núcleo da rede não se sobrecarregue. Esse tipo de comportamento, a princípio ineficiente, se baseia fortemente na teoria dos jogos (especificamente em jogos simetricos) que, dentre várias coisas, difunde a ideia de que se ninguém recua um pouco, para dar passagem aos demais, todos perdem. | 

### 7.1.1. Flags

Tipos de flags: 
- URG - O pacote contem dados importantes
- ACK - Certificação que recebeu o ultimo pacote ou outra resposta.
- PSH - Envia imediatamente mesmo se o buffer não estiver cheio.
- RST - Reseta a conexão ( ocorreu erro ou coisa parecida ).
- SYN - Inicia conexão.
- FIN - Termina conexão 

### 7.1.2. Conexão 

Quando se inicia uma conexão, o processo de 3-way handshake entra em jogo para garantir a conexão. 

O cliente (client) envia um pacote com o flag SYN marcado. O servidor (server) recebe o pacote e responde com um pacote com o flag ACKnowledge/SYN marcado. 

Então o cliente recebe e envia outro pacote com o flag ACK marcado. Pronta a conexão foi estabelecida entre o cliente e o servidor.

Para terminar a conexão o cliente envia um pacote com flag FIN marcado. O servidor ao receber o pacote de flag FIN do cliente responde com um pacote com o flag também marcado FIN.

![3way](https://www.mdpi.com/applsci/applsci-06-00358/article_deploy/html/images/applsci-06-00358-g001-550.jpg)

Quando há ataques de Syn, conhecido como Syn Flood: 

![synflood](https://www.mdpi.com/applsci/applsci-06-00358/article_deploy/html/images/applsci-06-00358-g002-550.jpg)

### 7.1.3. TCP Header

Um pacote TCP leva os seguintes dados em seu cabeçalho: 

![tcpheader](https://www.informabr.com.br/TCP/xtcpheader.jpg.pagespeed.ic.0GeFT0FFZN.webp)

## 7.2. UDP

Suponha uma conversa entre dois amigos: 

![conversa](https://www.alura.com.br/artigos/assets/uploads/2019/01/image_0-3.png)

A conversa não faz sentido, certo? Do outro lado, o amigo que recebeu: 

![amigo](https://www.alura.com.br/artigos/assets/uploads/2019/01/image_1-2.png)

O protocolo UDP (sigla para User Datagram Protocol) tem, como característica essencial, um atributo que pode parecer esquisito para os iniciantes no tema - a falta de confiabilidade.

Isso significa que, através da utilização desse protocolo, pode-se enviar datagramas de uma máquina à outra, mas sem garantia de que os dados enviados chegarão intactos e na ordem correta.

Além do mais, o UDP é um protocolo que não é voltado à conexão. Isso significa que o "aperto de mão", ou, tecnicamente, handshake, não é necessário para que se estabeleça uma comunicação.

As características já descritas do UDP podem parecer contraprodutivas no geral, mas elas formam um outro atributo que dá muito poder ao protocolo: a velocidade! 

No geral, o protocolo UDP permite uma comunicação bastante rápida, o que é muito vantajoso.

Velocidade alta mas confiabilidade baixa, ainda parece suspeito - não funcionou no nosso caso. Acontece que o UDP justamente não é feito para esse tipo de caso! Na verdade, o UDP tem sua grande vantagem quando se trata de serviços cuja velocidade é fundamental e a perda mínima de dados não muito desvantajosa.

Um exemplo é com jogos online, em que é normal alguns bytes se perderem na comunicação,mas que é sempre importante que a aplicação continue rodando com rapidez (sem se importar tanto com as perdas e falhas), para que não ocorra o famigerado lag.

## 8. Referências

- [Diferenças entre TCP e UDP](https://www.alura.com.br/artigos/quais-as-diferencas-entre-o-tcp-e-o-udp)
