# Domain Name System

Imagine que você gostaria de falar com uma pessoa com os seguintes dados: 
- Marcela; 
- Ipatinga;
- Minas Gerais;
- Brasil.

A Marcela será: 
- `marcela`.`ipatinga`.`minasgerais`.`brasil`. 

Para descobrir o telefone da `Marcela`, você passará pelos seguinte fluxo: 
- Contato com a telefonista no `102`;
- Contato da telefonista com a central `brasil`; 
- Contato da central `brasil` com a central `minasgerais`;
- Contato da central de `minasgerais` com a central de `ipatinga`. 

Cada central desconhece os telefones de outras regiões. Quem tem este conhecimento específico é a central regional. Este sistema tem um modelo distribuído porque facilita o funcionamento e manutenção. 

Quando a `Marcela`precisar fazer a manutenção, ela deve notificar apenas a central de `ipatinga`.

## 1. Modelo DNS

Servidores DNS (Domain Name System, ou sistema de nomes de domínios) são os responsáveis por localizar e traduzir para números IP os endereços dos sites que digitamos nos navegadores.

Estes endereços são chamados de domínio. Por exemplo, para acessar o buscador Google, basta você acessar o seguinte domínio: www.google.com.br.

O nome de domínio foi criado com a ideia de facilitar a memorização dos endereços de computadores na Internet. Sem ele, teríamos que memorizar uma sequência grande de números, que seriam os IPs.

Todo domínio possui um registro no DNS, que define qual o endereço IP do servidor de hospedagem e o IP do servidor de e-mail que responderão por este domínio. 

O processo para a descoberta dos servidores que respondem por um domínio é denominado **resolução do nome** ou **resolução do domínio**.

# 2. Definições

- Domain Name System: todos os **organismos que gerenciam** os nomes de domínios;
- Domain Name Service: o **protocolo para trocar informações** sobre os domínios;
- Domain Name Server: um computador **servidor no qual roda um software servidor que inclui o protocolo DNS** e que pode responder às perguntas sobre ele. 

# 3. Domain Name System

Tudo começa com o domínio raiz: `.` que deveria ser escrito ao fim de todos os domínios, mas em geral omitimos. 

## 3.1. TLD 

A ICANN é um organismo que gerencia a lista dos Top Level Domain (TLD), ou domínios de alto nível: 

- COM; 
- NET; 
- ORG; 
- BR; 
- UK; 
- etc. 

Existe um TLD por país (FR para a França, IT para a Itália, DE para Alemanha, BR para o Brasil, etc.), assim como alguns TLD gerais (COM, NET, ORG, MIL, BIZ). 

A ICANN delega a gestão de cada TLD para um organismo (chamado registry):

![Registry](https://img-21.ccm2.net/ZlFgF7tB6lJIyz8DhEPbJJJQ5S4=/500x/67b6589e34e84e188126690c69c68945/ccm-faq/6IsFyOb82CuFU0hb-s-.png)

Cada registry autoriza os registradores (registrars credenciados) a vender nomes de domínio, que têm um papel comercial nesta transação.

Cada país tem um TLD que correspone ao seu código de país ISO (BR Brasil, PT Portugal, FR França, IT Itália, DE Alemanha, UK Grã-Bretanha, CA Canadá, PL Polônia, BL Bélgica, etc). Eles são chamados de ccTLD Country-code TLD.

Algumas delas: 

- COM: usado em sites comerciais;
- NET: usado por organizações ou empresas em relação direta com a Internet e sua evolução;
- ORG: para outras organizações, associações e ONGs;
- EDU: reservado ao sistema educacional e universidades estadunidenses;
- GOV: para governos;
- MIL : para o exército dos Estados Unidos;
- INT: para empresas, instituições, organismos internacionais;
- COOP: para as cooperações entre empresas ou outras instituições;
- AERO: (recente) para a aeronáutica, aviação;
- BIZ: para business (empresas);
- NAME: para os indivíduos;
- INFO: para as mídias.

É possível que um provedor forneça o mesmo IP para vários sites. O DNS também tem a função de resolver o IP para mais de um site ou domínio no mesmo IP. 

## 3.2. Aspecto construtivo

O nome de domínio é um tipo de ficha de dados com (geralmente): 
- o nome do domínio; 
- os nomes e endereços do proprietário legal do domínio e do responsável técnico do domínio ou do responsável do faturamento do domínio; 
- a data de expiração do domínio e das informações técnicas (endereços dos servidores DNS etc).

# 4. Tipos de DNS

## 4.1. Resolver e Caching

O que que acontece quando eu digito um endereço HTTP? 

O servidor DHCP do seu provedor (que atribuiu o seu endereço IP) também atribui endereços de DNS. 

O seu computador se conecta a esses servidores de DNS para obter o endereço IP do site. 

Se o servidor DNS do seu provedor de acesso não tem a resposta, ele vai pedir para outros servidores DNS. (Este exemplo nem sempre é verdadeiro: O seu sistema operacional mantém um pequeno cache de DNS). 

O resolver/cache resolve nomes para uma grande rede. Além disso, ele armazena informações desde os servidores DNS root até o seu servidor DNS. Para definir quanto tempo esta informação fica armazenada, você define pelo DNS autoritative, abordado mais adiante. 

### Flush DNS - Troca de DNS

A maioria dos sistemas operacionais e clientes DNS armazenará em cache automaticamente endereços IP e outros resultados DNS. 

Isso é feito para acelerar solicitações subsequentes para o mesmo nome de host. Às vezes, resultados ruins serão armazenados em cache e, portanto, precisam ser limpos do cache para que você se comunique corretamente com o host. 

Todos os principais sistemas operacionais permitem forçar esse processo.

Exemplo: 

Imagine que você está navegando pela internet e realizando suas tarefas como de costume, mas percebeu que a conexão está mais lenta do que o normal: os sites estão demorando para carregar, as imagens não aparecem como deveriam, suas músicas nos sites de streaming estão travando constantemente, entre outros problemas.

Uma explicação para o problema de lentidão está na própria configuração do servidor. Quando você contrata um serviço de internet, seu computador é configurado automaticamente para utilizar o endereço de DNS da empresa escolhida.

Por um lado, podemos concordar que é algo mais prático para o usuário, já que não é preciso mudar configuração nenhuma. Por outro, a conexão pode ficar mais lenta justamente por haver várias pessoas usando o mesmo servidor, e é aí que surgem problemas na performance.

Nessas situações, um procedimento simples de ser realizado e que pode resolver a questão é a troca de servidor DNS. Com isso, você ganha benefícios na velocidade da conexão, mais segurança e até mesmo aumento de privacidade ao navegar.

Geralmente, o endereço DNS mais recomendado é o do Google, que é composto pelas seguintes sequências numéricas: 
- 8.8.8.8 (servidor primário);
- 8.8.4.4 (servidor secundário).

Outro muito conhecido é o OpenDNS, que oferece recursos adicionais, como sistemas de proteção parental e proteção contra sites falsos. Seus endereços são:
- 208.67.222.222 (servidor primário);
- 208.67.220.220 (servidor secundário).

Contudo, nada impede o usuário de utilizar o endereço DNS que achar necessário. 

Outra dica é que, se possível, é interessante que você faça testes de benchmark para saber qual é o servidor mais adequado para seu PC. Uma opção é o programa Namebench, que é gratuito e está disponível para todos os sistemas operacionais.

## 4.2. DNS Autoritative

Todo domínio possui autoridade sobre os domínios locais, como por exemplo a central de `ipatinga`, do nosso exemplo. 

## 4.3. DNS Reverso 

Aqui você informa o IP e fica sabendo um nome. 

O DNS reverso (que resolve 200.176.3.145 de volta para exemplo.hipotetico.com.br) começa no seu provedor de acesso ou de meio físico (ou com quem quer que lhe diga qual é o seu endereço IP). 

Você deve dizer-lhe quais servidores de DNS que respondem pelos apontamentos de DNS reverso para os seus IPs (ou, eles podem configurar esses apontamentos em seus próprios servidores de DNS), e o seu provedor passará esta informação adiante quando os servidores de DNS deles forem consultados sobre os seus apontamentos de DNS reverso. 

Então, qualquer um no mundo pode consultar os apontamentos de DNS reverso dos seus IPs, e você pode responder com qualquer nome que quiser (tendo ou não controle sobre os domínios desses nomes, embora você não deva apontá-los para nomes que não são dos seus domínios, sem permissão).

# 5. Domain Name Service - O que é? 

É um protocolo que permite aos diversos computadores trocar informações sobre os domínios. 

Pode-se obter informações sobre um domínio usando o programa Whois (ausente no Windows, mas fornecido como padrão nos sistemas Unix/Linux).

# 6. Domain Name Server

Os servidores DNS respondem às perguntas sobre os domínios (por exemplo, quando você digita http://br.ccm.net). Cada servidor DNS conversa com os servidores DNS vizinhos. 

As informações sobre um domínio se espalham de forma viral. Assim, quando um domínio é criado ou modificado, estas informações levam mais ou menos 72 horas para chegar a todos os servidores DNS do planeta. 

Em geral, este é o DNS (Servidor) que configuramos no computador. 

Este servidor é quem faz a tradução do IP para o navegador. 

# 7. Como ter um domain name 

Você precisa de quatro coisas: 

- um nome de domínio; 
- um host DNS; 
- um host HTTP (web) 
- implementar o redirecionamento.

Escolha um registrador (credenciado pela ICANN) que venda os nomes de domínio no TLD de sua escolha (COM/NET/ORG) e verificar as condições a serem preenchidas para obter um.

# 8. Referências

- [DNS Explained](https://www.youtube.com/watch?v=72snZctFFtA)
- [DNS - Videoaula Kretcheu](https://www.youtube.com/watch?v=i4KMcl0tuEg&list=PLOuKCq4Sak9e_u8JbGj7Jnc9pYq2-xcy6&index=6&t=0s)
- [O que é um DNS e como funcionam os nomes de domínio](https://br.ccm.net/faq/10093-o-que-e-um-dns-e-como-funcionam-os-nomes-de-dominio)

