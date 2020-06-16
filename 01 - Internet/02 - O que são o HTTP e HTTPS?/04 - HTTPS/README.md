# HTTPS

Cada URL que começa com HTTP usa um tipo básico de “protocolo de transferência de hipertexto”. Esse padrão de protocolo de rede é o que permite que navegadores e servidores se comuniquem através da troca de dados.

Ou seja, por se tratar de um protocolo da **camada de aplicação**, o HTTP foca em apresentar a informação, se preocupando menos com a maneira como essa informação é transmitida de um ponto para outro. Isso quer dizer que o HTTP pode ser invadido e alterado, tornando as informações trocadas entre um site e a pessoa que o visita vulneráveis.

É por isso que lojas virtuais não devem ter páginas construídas em HTTP, pois não são tão seguras para que os usuários insiram informações necessárias para a compra como dados pessoais e de cartão de crédito. Sites assim devem ser feitos em HTTPS.

Essencialmente, ambos se referem ao mesmo “protocolo de transferência de hipertexto” que permite ao usuário ver na tela os dados solicitados por meio da inserção da URL. Contudo, o HTTPS tem como diferencial ser mais avançado e seguro.

Em outras palavras, o HTTPS é uma extensão do HTTP. O “S” vem da palavra “secure” (“segurança” em inglês) e costuma ser oferecido pelo **certificado SSL**, oferecidos pela maioria dos servidores. 

Ele oferece uma conexão criptografada entre o servidor e o navegador, de maneira que o usuário possa inserir informações com mais segurança.

Ou seja, sem HTTPS, qualquer dado inserido no site (nome, e-mail, senhas, cartão de crédito, e afins) são enviados em forma de texto simples, sendo, portanto, suscetíveis a intercepção ou interceptação. 

# Diferenças técnicas HTTP x HTTPS

|  | HTTP | HTTPS |
|--:|--|--|
| Segurança | Inseguro | Seguro |
| Porta | TCP 80 | TCP 4433 |
| Camada | Aplicação | Transporte |
| Validação de domínio | Não necessária | Requer obrigatoriamente validações de domínio e certas certificações que requerem um processo legal. |
| Encriptação de dados | Não | Sim |
| SSL/TLS | Não | Sim |

