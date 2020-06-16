# Como a internet funciona

# 1. Onde começar

Como a Internet é uma rede global de computadores, cada computador conectado à Internet deve ter um endereço exclusivo. 

Os endereços da Internet estão no formato `nnn.nnn.nnn.nnn`, em que `nnn` deve ser um número de 0 a 255. 

Esse endereço é conhecido como endereço IP (Protocolo da internet).

![Diagrama 1](https://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper_files/ruswp_diag1.gif)

# 2. Pilhas e pacotes de protocolo
 
Portanto, seu computador está conectado à Internet e possui um endereço exclusivo. Como ele 'conversa' com outros computadores conectados à Internet? 

Digamos que seu endereço IP é 1.2.3.4 e você deseja enviar uma mensagem para o computador 5.6.7.8. 

A mensagem que você deseja enviar é "Hello computer 5.6.7.8!". 

A mensagem deve ser transmitida por qualquer tipo de cabo que conecte seu computador à Internet. 

Digamos que você tenha discado em seu **Provedor(ISP)** e a mensagem deve ser transmitida pela linha telefônica. 

Portanto, a mensagem deve ser traduzida do texto alfabético em sinais eletrônicos, transmitida pela Internet e depois traduzida novamente em texto alfabético. Como isso é realizado? Através do uso de uma pilha de protocolos (**protocol stack**). 

Todo computador precisa de um para se comunicar na Internet e, geralmente, é incorporado ao sistema operacional do computador (por exemplo, Windows, Unix, etc.). 

A pilha de protocolos usada na Internet é chamada de pilha de protocolos **TCP/IP** devido aos dois principais protocolos de comunicação usados. A pilha TCP / IP tem a seguinte aparência:

| Camada de protocolo | Comentários
| - | - |
| Camada de protocolos de aplicativos | Protocolos específicos para aplicativos como WWW, email, FTP, etc.
| Camada de protocolo de controle de transmissão | TCP direciona pacotes para um aplicativo específico em um computador usando um número de porta.
Camada de Protocolo da Internet | IP direciona pacotes para um computador específico usando um endereço IP.
Camada de hardware | Converte dados binários de pacotes em sinais de rede e vice-versa. (placa de rede ethernet, modem para linhas telefônicas etc.)

Se seguíssemos o caminho que a mensagem "Hello computer 5.6.7.8!" levado do nosso computador para o computador com endereço IP 5.6.7.8, aconteceria algo como isto:

![Diagram 2](https://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper_files/ruswp_diag2.gif)

1. A mensagem começaria na parte superior da pilha de protocolos do seu computador e funcionaria bem para baixo. 

2. Se a mensagem a ser enviada for longa, cada camada de pilha pela qual a mensagem passa pode dividi-la em pequenos pedaços de dados. Isso ocorre porque os dados enviados pela Internet (e a maioria das redes de computadores) são enviados em blocos gerenciáveis. Na Internet, esses blocos de dados são conhecidos como pacotes.

3. Os pacotes atravessariam a camada de aplicativos e continuariam para a camada TCP. Cada pacote recebe um número de porta. Muitos programas podem estar usando a pilha TCP / IP e enviando mensagens. Precisamos saber qual programa no computador de destino precisa receber a mensagem porque ela estará escutando em uma porta específica.

4. Depois de passar pela camada TCP, os pacotes prosseguem para a camada IP. É aqui que cada pacote recebe seu endereço de destino, 5.6.7.8.

5. Agora que nossos pacotes de mensagens têm um número de porta e um endereço IP, eles estão prontos para serem enviados pela Internet. A camada de hardware se encarrega de transformar nossos pacotes contendo o texto alfabético de nossa mensagem em sinais eletrônicos e transmiti-los pela linha telefônica.

6. No outro extremo da linha telefônica, seu ISP tem uma conexão direta com a Internet. O roteador ISPs examina o endereço de destino em cada pacote e determina para onde enviá-lo. Freqüentemente, a próxima parada do pacote é outro roteador.

7. Eventualmente, os pacotes atingem o computador 5.6.7.8. Aqui, os pacotes começam na parte inferior da pilha TCP / IP do computador de destino e funcionam para cima.

8. À medida que os pacotes avançam pela pilha, todos os dados de roteamento adicionados pela pilha do computador de envio (como endereço IP e número da porta) são retirados dos pacotes.

9. Quando os dados chegam ao topo da pilha, os pacotes foram remontados em sua forma original, "Olá computador 5.6.7.8!"

# 3. Infraestrutura de rede

Então agora você sabe como os pacotes viajam de um computador para outro pela Internet. Mas o que há no meio? O que realmente compõe a Internet?

![Diagrama 3](https://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper_files/ruswp_diag3.gif)

Aqui vemos o diagrama 1 redesenhado com mais detalhes. A conexão física através da rede telefônica com o provedor de serviços de Internet pode ter sido fácil de adivinhar, mas além disso pode ter alguma explicação.

O ISP mantém um pool de modems para seus clientes de discagem. Isso é gerenciado por algum tipo de computador (geralmente um dedicado) que controla o fluxo de dados do pool de modems para um backbone ou roteador de linha dedicado. 

> backbone: esquema de ligações centrais de um sistema de redes mais amplo, tipicamente de elevado desempenho e com dimensões continentais.

Essa configuração pode ser chamada de servidor de porta, pois 'serve' o acesso à rede. As informações de faturamento e uso geralmente são coletadas aqui também.

Depois que seus pacotes atravessam a rede telefônica e o equipamento local do seu ISP, eles são roteados para o backbone do ISP ou um backbone do qual o ISP compra largura de banda. 

A partir daqui, os pacotes geralmente trafegam por vários roteadores e por vários backbones, linhas dedicadas e outras redes até encontrar seu destino, o computador com o endereço 5.6.7.8. 

Mas não seria bom se soubéssemos a rota exata de nossos pacotes pela Internet?

## O programa Traceroute

Se você estiver usando o Microsoft Windows ou uma versão do Unix e tiver uma conexão com a Internet, aqui está outro programa útil da Internet. 

Esse é chamado `traceroute` e mostra o caminho que seus pacotes estão seguindo para um determinado destino da Internet. 

Como o ping, você deve usar o traceroute em um prompt de comando. No Windows, use o `tracert` www.google.com. Em um prompt do Unix, digite `traceroute` www.google.com. 

Como o ping, você também pode inserir endereços IP em vez de nomes de domínio. O Traceroute imprimirá uma lista de todos os roteadores, computadores e quaisquer outras entidades da Internet pelas quais seus pacotes devem viajar para chegar ao seu destino.

Se você usar o traceroute, notará que seus pacotes devem percorrer muitas coisas para chegar ao destino. 

A maioria tem nomes longos, como sjc2-core1-h2-0-0.atlas.digex.net e fddi0-0.br4.SJC.globalcenter.net. Esses são roteadores da Internet que decidem para onde enviar seus pacotes. Vários roteadores são mostrados no diagrama 3, mas apenas alguns. 

O diagrama 3 pretende mostrar uma estrutura de rede simples. A Internet é muito mais complexa.

# 4. Infraestrutura da internet

O backbone da Internet é composto de grandes redes que se interconectam. Essas grandes redes são conhecidas como provedores de serviços de rede ou NSPs. 

Alguns dos grandes NSPs são UUNet, CerfNet, IBM, BBN Planet, SprintNet, PSINet, entre outros. 

Essas redes fazem pares entre si para trocar tráfego de pacotes. 

Cada NSP é necessário para conectar-se a três pontos de acesso à rede ou NAPs. 

Nos NAPs, o tráfego de pacotes pode saltar do backbone de um NSP para o backbone de outro NSP. 

Os NSPs também se interconectam nas Metropolitan Area Exchanges ou MAEs. 

Os MAEs têm o mesmo objetivo que os NAPs, mas são de propriedade privada. 

Os NAPs eram os pontos de interconexão originais da Internet. Os NAPs e MAEs são referidos como Internet Exchange Points ou IXs. Os NSPs também vendem largura de banda para redes menores, como ISPs e provedores de largura de banda menores. Abaixo está uma imagem mostrando essa infraestrutura hierárquica.

![Diagram 4](https://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper_files/ruswp_diag4.gif)

Esta não é uma representação verdadeira de uma parte real da Internet. 

O Diagrama 4 destina-se apenas a demonstrar como os NSPs poderiam se interconectar entre si e com os ISPs menores. Nenhum dos componentes físicos da rede é mostrado no diagrama 4, como no diagrama 3. 

Isso ocorre porque a infraestrutura de backbone de um único NSP é um desenho complexo por si só. A maioria dos NSPs publica mapas de sua infraestrutura de rede em seus sites e pode ser encontrada facilmente. 

Desenhar um mapa real da Internet seria quase impossível devido ao tamanho, complexidade e estrutura em constante mudança.

# 5. Hierarquia de routeamento da internet

Então, como os pacotes encontram-se na Internet? 

Todo computador conectado à Internet sabe onde estão os outros computadores? Os pacotes simplesmente são transmitidos para todos os computadores na Internet? A resposta para ambas as perguntas anteriores é 'não'. 

Nenhum computador sabe onde estão os outros computadores e os pacotes não são enviados para todos os computadores. As informações usadas para obter pacotes para seus destinos estão contidas nas tabelas de roteamento mantidas por cada roteador conectado à Internet.

Roteadores são comutadores de pacotes. Um roteador geralmente é conectado entre redes para rotear pacotes entre elas. Cada roteador conhece suas sub-redes e quais endereços IP eles usam. O roteador geralmente não sabe quais endereços IP estão acima dele. 

Examine o diagrama 5 abaixo. As caixas pretas que conectam os backbones são roteadores. Os backbones NSP maiores na parte superior estão conectados a uma NAP. Sob eles há várias sub-redes e, sob eles, mais sub-redes. Na parte inferior, existem duas redes locais com computadores conectados.

![Diagrama 5](https://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper_files/ruswp_diag5.gif)

Quando um pacote chega a um roteador, o roteador examina o endereço IP colocado pela camada de protocolo IP no computador de origem. 

O roteador verifica sua tabela de roteamento. Se a rede que contém o endereço IP for encontrada, o pacote será enviado para essa rede. 

Se a rede que contém o endereço IP não for encontrada, o roteador envia o pacote em uma rota padrão, geralmente na hierarquia do backbone para o próximo roteador. 

Espara-se que o próximo roteador saiba para onde enviar o pacote. 

Caso contrário, novamente o pacote é roteado para cima até atingir um backbone NSP. 

Os roteadores conectados aos backbones NSP mantêm as maiores tabelas de roteamento e aqui o pacote será roteado para o backbone correto, onde começará sua jornada 'descendente' através de redes cada vez menores até encontrar seu destino.

# 6. Nomes de domínio e resolução de endereços

Mas e se você não souber o endereço IP do computador ao qual deseja se conectar? E se você precisar acessar um servidor da web chamado www.anothercomputer.com? 

Como o seu navegador da web sabe onde está o computador na Internet? A resposta para todas essas perguntas é o Domain Name Service ou DNS. 

O DNS é um banco de dados distribuído que controla os nomes dos computadores e seus endereços IP correspondentes na Internet.

Muitos computadores conectados à Internet hospedam parte do banco de dados DNS e o software que permite que outros acessem. 

Esses computadores são conhecidos como servidores DNS. 

Nenhum servidor DNS contém o banco de dados inteiro, eles contêm apenas um subconjunto dele. 

Se um servidor DNS não contiver o nome de domínio solicitado por outro computador, o servidor DNS redirecionará o computador solicitante para outro servidor DNS.

![DNS](https://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper_files/ruswp_diag6.gif)

O Serviço de Nome de Domínio está estruturado como uma hierarquia semelhante à hierarquia de roteamento IP. 

O computador que solicita uma resolução de nomes será redirecionado para cima da hierarquia até que seja encontrado um servidor DNS que possa resolver o nome de domínio na solicitação. 

A Figura 6 ilustra uma parte da hierarquia. No topo da árvore estão as raízes do domínio. Alguns dos domínios mais antigos e comuns são vistos perto do topo. O que não é mostrado é a multiplicidade de servidores DNS em todo o mundo que formam o restante da hierarquia.

Quando uma conexão com a Internet é configurada (por exemplo, para uma LAN ou acesso à rede dial-up no Windows), um servidor DNS primário e um ou mais servidores DNS secundários geralmente são especificados como parte da instalação. 

Dessa forma, qualquer aplicativo da Internet que precise de resolução de nome de domínio poderá funcionar corretamente. 

Por exemplo, quando você insere um endereço da web no seu navegador, o navegador primeiro se conecta ao seu servidor DNS primário. 

Depois de obter o endereço IP para o nome de domínio digitado, o navegador se conecta ao computador de destino e solicita a página da web desejada.

# 8. Protocolos de aplicação: HTTP e a Rede mundial de computadores

HTTP é um protocolo no nível do aplicativo, pois fica em cima da camada TCP na pilha de protocolos e é usado por aplicativos específicos para conversar entre si. Nesse caso, os aplicativos são navegadores e servidores da web. 

Clientes (navegadores da web) enviam solicitações aos servidores da web para elementos da web, como páginas da web e imagens. 

Após a solicitação ser atendida por um servidor, a conexão entre cliente e servidor pela Internet é desconectada. 

Uma nova conexão deve ser feita para cada solicitação. A maioria dos protocolos é orientada à conexão. 

Isso significa que os dois computadores que se comunicam mantêm a conexão aberta pela Internet. Antes que uma solicitação HTTP possa ser feita por um cliente, uma nova conexão deve ser feita com o servidor.

Quando você digita um URL em um navegador da web, é o que acontece:

1. Se a URL contiver um nome de domínio, o navegador primeiro se conectará a um DNS e recuperará o endereço IP correspondente ao servidor da Web.

2. O navegador da web se conecta ao servidor da web e envia uma solicitação HTTP (via pilha de protocolos) para a página da web desejada.

3. O servidor da web recebe a solicitação e verifica a página desejada. Se a página existir, o servidor da Web a envia. Se o servidor não conseguir encontrar a página solicitada, ele enviará uma mensagem de erro HTTP 404. (404 significa "Página não encontrada", como qualquer pessoa que tenha navegado na Web provavelmente sabe.)

4. O navegador recebe a página de volta e a conexão é fechada.

5. O navegador analisa a página e procura outros elementos da página necessários para concluir a página da web. 

6. Isso geralmente inclui imagens, applets etc. Para cada elemento necessário, o navegador faz conexões adicionais e solicitações HTTP ao servidor para cada elemento.

7. Quando o navegador terminar de carregar todas as imagens, applets, etc., a página será completamente carregada na janela do navegador.


# 9. Protocolos de aplicação: SMTP e e-mail. 

Outro serviço de Internet comumente usado é o correio eletrônico. 

O email usa um protocolo no nível do aplicativo chamado Simple Mail Transfer Protocol ou SMTP. O SMTP também é um protocolo baseado em texto, mas, diferentemente do HTTP, o SMTP é orientado à conexão. 

O SMTP também é mais complicado que o HTTP. Há muito mais comandos e considerações no SMTP do que no HTTP.
Quando você abre o seu cliente de email para ler seu email, é o que normalmente acontece:

1. O cliente de email (Netscape Mail, Lotus Notes, Microsoft Outlook etc.) abre uma conexão com o servidor de email padrão. O endereço IP ou o nome de domínio do servidor de email geralmente é configurado quando o cliente de email é instalado.

2. O servidor de email sempre transmitirá a primeira mensagem para se identificar.

3. O cliente enviará um comando SMTP HELO ao qual o servidor responderá com uma mensagem 250 OK.

4. Dependendo se o cliente está checando e-mails, enviando e-mails, etc., os comandos SMTP apropriados serão enviados ao servidor, que responderá de acordo.

5. Essa transação de solicitação / resposta continuará até o cliente enviar um comando SMTP QUIT. O servidor então se despedirá e a conexão será fechada.

Uma simples 'conversa' entre um cliente SMTP e o servidor SMTP é mostrada abaixo. 

- R: indica mensagens enviadas pelo servidor (destinatário) 
- S: indica mensagens enviadas pelo cliente (remetente).

~~~
      Este exemplo de SMTP mostra as mensagens enviadas por Smith no host USC-ISIF, para
      Jones, Green e Brown no anfitrião BBN-UNIX. Aqui assumimos que
      o host USC-ISIF contata o host BBN-UNIX diretamente. O correio é
      aceito para Jones e Brown. Verde não tem uma caixa de correio em
      host BBN-UNIX.

      -------------------------------------------------- -----------

         R: 220 Pronto para o Serviço de Transferência de Correio Simples BBN-UNIX.ARPA
         S: HELO USC-ISIF.ARPA
         R: 250 BBN-UNIX.ARPA

         S: CORREIO DE: <Smith@USC-ISIF.ARPA>
         R: 250 OK

         S: RCPT PARA: <Jones@BBN-UNIX.ARPA>
         R: 250 OK

         S: RCPT PARA: <Green@BBN-UNIX.ARPA>
         R: 550 Nenhum usuário assim aqui

         S: RCPT PARA: <Brown@BBN-UNIX.ARPA>
         R: 250 OK

         S: DATA
         R: 354 Iniciar entrada de email; termina com <CRLF>. <CRLF>
         S: Blá, blá, blá ...
         S: ... etc etc etc.
         S:.
         R: 250 OK

         S: QUIT
         R: 221 BBN-UNIX.ARPA - Serviço que fecha o canal de transmissão
~~~ 

Essa transação SMTP é retirada do RFC 821, que especifica o SMTP.

# 10. TCP - Protocolo de controle de transmissão

Em outro computador na Internet, as mensagens que eles enviam (usando um protocolo de camada de aplicativo específico) são transmitidas pela pilha para a camada TCP. 

O TCP é responsável pelo roteamento de protocolos de aplicativos para o aplicativo correto no computador de destino. 

Para fazer isso são usadoss números de porta. As portas podem ser consideradas como canais separados em cada computador. 

Por exemplo, você pode navegar na web enquanto lê email. Isso ocorre porque esses dois aplicativos (o navegador da web e o cliente de email) usavam números de porta diferentes. 

Quando um pacote chega ao computador e sobe na pilha de protocolos, a camada TCP decide qual aplicativo recebe o pacote com base no número da porta.

O TCP funciona assim:

- Quando a camada TCP recebe os dados do protocolo da camada de aplicação de cima, os segmenta em 'pedaços' gerenciáveis e, em seguida, adiciona um cabeçalho TCP com informações específicas de TCP a cada 'pedaço'. As informações contidas no cabeçalho TCP incluem o número da porta do aplicativo para o qual os dados precisam ser enviados.

- Quando a camada TCP recebe um pacote da camada IP abaixo dela, a camada TCP retira os dados do cabeçalho TCP do pacote, faz alguma reconstrução de dados, se necessário, e envia os dados para o aplicativo correto usando o número da porta obtido no TCP cabeçalho.

É assim que o TCP direciona os dados que se deslocam pela pilha de protocolos para o aplicativo correto.

TCP não é um protocolo textual. O TCP é um serviço de fluxo de bytes confiável, orientado à conexão. Orientado a conexão significa que dois aplicativos que usam TCP devem primeiro estabelecer uma conexão antes de trocar dados. 

O TCP é confiável porque, para cada pacote recebido, uma confirmação é enviada ao remetente para confirmar a entrega. O TCP também inclui uma soma de verificação no cabeçalho para verificar os dados recebidos. O cabeçalho TCP fica assim:

![Diagrama](https://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper_files/ruswp_diag7.gif)

Observe que não há lugar para um endereço IP no cabeçalho TCP. Isso ocorre porque o TCP não sabe nada sobre endereços IP. 

O trabalho do TCP é obter dados de nível de aplicativo para aplicativo de maneira confiável. A tarefa de obter dados de um computador para outro é o trabalho do IP.

# 11. Protocolo de internet

Ao contrário do TCP, o IP é um protocolo não confiável e sem conexão. O IP não se importa se um pacote chega ao seu destino ou não. O IP também não conhece conexões e números de portas. 

O trabalho do IP também é enviar e encaminhar pacotes para outros computadores. Pacotes IP são entidades independentes e podem chegar fora de ordem ou não. O trabalho do TCP é garantir que os pacotes cheguem e estejam na ordem correta. 

A única coisa que o IP tem em comum com o TCP é a maneira como ele recebe dados e adiciona suas próprias informações de cabeçalho IP aos dados do TCP. O cabeçalho IP fica assim:

![IP](https://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper_files/ruswp_diag8.gif)

Acima, vemos os endereços IP dos computadores de envio e recebimento no cabeçalho IP. Abaixo está a aparência de um pacote depois de passar pela camada de aplicação, camada TCP e camada IP. 

Os dados da camada de aplicação são segmentados na camada TCP, o cabeçalho TCP é adicionado, o pacote continua na camada IP, o cabeçalho IP é adicionado e o pacote é transmitido pela Internet.

![Diagrama IP](https://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper_files/ruswp_diag9.gif)

# 12. Referência 
[InternetWhitepaper](https://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm)

