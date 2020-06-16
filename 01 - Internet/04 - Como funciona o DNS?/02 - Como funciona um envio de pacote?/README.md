# Ethernet, ARP e MAC Address

O MAC Address é uma sigla do termo Midia Access Control Address, que significa Endereço de controle de um dispositivo que pode ser uma placa ou dispositivo de rede, representado por 48 bits, em seis grupos de pares hexadecimais. 

Exemplo: 
- `0A`:`1B`: `2B`: `02`: `35`: `42`. 

Cada par acima representa 8 bits. Não pode haver numa mesma rede, dois dispositivos com o mesmo MAC Address. 

Em geral, o três primeiros octetos são escolhidos por cada fabricante para definir a marca. 

## Primeiro contato

Suponha que um usuário de uma estação quer acessar a intranet da empresa, que está hospedada no servidor interno. A estação em sua primeira comunicação não sabe a quem ela vai dirigir o pacote de rede Ethernet, via IP. Por isso, ela precisará do ARP (Address Resolution Protocol). 

Todo pacote ethernet tem dois tipos de MACs. 

A estação enviará um pacote ethernet: 
- MAC Origem: `00`:`1A`:`73`:`A9`:`CD`:`AF`.
- MAC Destino (MAC Broadcast): `FF`:`FF`:`FF`:`FF`:`FF`:`FF`.

Estas informações servem para que o switch saiba para quem ele vai enviar esta informação. 

Segue o processo: 
- Ao enviar um pacote ethernet (origem: estação) para o Broadcast, ele envia uma cópia para cada uma das máquinas conectadas. 
- O servidor abre o pacote ethernet e identifica a mensagem via protocolo ARP: 
  - Who has: 192.168.0.2? 
  - Tell: 192.168.0.10.
- Esta informação só será de interesse do servidor, pois ele tem o ip 192.168.0.2.

- O servidor enviará uma resposta somente para a estação:
- MAC Origem: `00`:`13`:`10`:`A8`:`67`:`40`.
- MAC Destino (estação): `00`:`1A`:`73`:`A9`:`CD`:`AF`.

- A estação irá abrir o pacote ethernet (há aqui ainda parte do protocolo ARP): 
  - `192`.`168`.`0`.`2` is at `00`:`13`:`10`:`A8`:`67`:`40`. 
  
## Segundo contato

Tendo feita a conexão anterior, já havendo a troca do protocolo ARP. Um novo pacote Ethernet é lançado especificamente para o servidor: 
- MAC Origem: `00`:`1A`:`73`:`A9`:`CD`:`AF`.
- MAC Destino: `00`:`13`:`10`:`A8`:`67`:`40`. 

Dentro do pacote ethernet há: 

| Dispositivo  | IP  | Porta  |
|--|--|--|
|Origem (estação) | `192`.`168`.`0`.`10` | `4045` (Normalmente usa-se uma porta acima de 1024).  |
|Destino (servidor) | `192`.`168`.`0`.`2` | `80` |

O servidor web escutará na porta `80` os pacotes TCP/IP que chegarem. E qual é o conteúdo do pacote TCP/IP que estava no pacote ethernet? 
- GET `/` HTTP/1.1  
  - `/` : raiz do site. 
  - `HTTP/1.1` : protocolo HTTP. 
  
Como fica o encapsulamento: 
Procolo HTTP --> Protocolo TCP/IP --> Protocolo Ethernet

O servidor então responde: 
- MAC Origem: `00`:`13`:`10`:`A8`:`67`:`40`;
- MAC Destino: `00`:`1A`:`73`:`A9`:`CD`:`AF`.

Dentro há um protocolo TCP/IP: 

| Dispositivo  | IP  | Porta  |
|--|--|--|
|Origem (servidor) | `192`.`168`.`0`.`2` | `80`  |
|Destino (estação) | `192`.`168`.`0`.`10` | `4045` (programa que receberá a resposta)|

Dentro do protocolo, há uma resposta: 

~~~
<html> 
    <body> 
      <h1> Deu certo </h1>
  < /body>
</html>
~~~
