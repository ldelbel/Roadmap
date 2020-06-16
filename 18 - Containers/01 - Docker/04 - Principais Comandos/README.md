# Comandos Docker

## 1. Build 

| Comando | Descrição |
|--|--|
| `Docker build –t <NAME:TAG> <DIR_DOCKERFILE>` | Cria uma imagem Docker (-t formata no padrão: name:tag) com base no arquivo Dockerfile   |

* DIR indica aonde está o dockerfile 
* Tag: latest (exemplo) 

## 2. Atualização 

| Comando  |  Descrição |
|--|--|
| Docker pull <nome_da_imagem> |faz o download da imagem para o repositório local|
| Docker push <nome_da_imagem>| faz o upload da imagem para o repositório docker |
|docker commit ID/apelido nome_da_nova_imagem |  gera uma nova versão|

## 3. Deletar 

| Comando  |  Descrição |
|--|--|
|Docker kill <nome_do_container> |mata um container, mas não limpa ele.  |
|Docker rm <nome_do_container>|mata e limpa um container| 
|Docker rm $(docker ps -a -q)| mata e limpa todos os containers | 
|Docker rmi <nome_da_imagem>| deleta uma imagem | 
* `-a` == all 
* `-q` == ID

## 4. Consulta 

| Comando  |  Descrição |
|--|--|
|Docker images |Mostra todas as imagens no repositório local |
|Docker inspect |  Mostra informações construídas do docker.  |
|Docker ps|apresenta containers ativos  |
|Docker ps -a|apresenta containers ativos e já usados |
|Docker search <nome_da_imagem>|busca uma imagem no index de registros|

## 5. Renomear 

| Comando  |  Descrição |
|--|--|
|Docker rename nome_antigo nome_novo | renomeia um container docker  |
|Docker tag nome_antigo nome_novo |  renomeia uma imagem docker (mantém o antigo) |

## 6. Run 

| Comando  |  Descrição |
|--|--|
|Docker exec -it <id_do_container> bash | Roda o terminal interno ao container.  |
|Docker run <id_do_container> | roda um container a partir de uma imagem  |
|Docker run --name apelido –e <nome_da_variavel>="valor" -d <nome_da_imagem> | roda um container a partir de uma imagem e dá um apelido, seta variáveis do ambiente (pode ser usado para rodar o container). |

0 `–d` impede que seja encerrado.  

## 7. Argumentos 

A cada novo comando, novas camadas são geradas no container. Cuidado com isso. 

| Argumento  |  Descrição |
|--|--|
|`-d` | para que o container rode em segundo plano. Se der CTRL C o container não é encerrado. Imprime a container ID.|
|`-t`| simula um terminal dentro do container. Se junto ao –i, recebe dados. Para interagir com o container.  |
|`-i`| interativo (STDIN).|
|`--name` | dar o nome ao container|

