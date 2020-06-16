# Criando um projeto

- Iniciar um novo repositório local na pasta do seu projeto

`git init`
   
- Associar seu repositório local ao repositório remoto, com o apelido de "origin".

`git remote add origin https://github.com/atalhox/meuprojeto.git`

* ATENÇÃO: troque pelo caminho do seu repositório do Github.

O comando **git remote add** usa dois argumentos:

* Um nome de remote, por exemplo, **origin**
* Uma URL remota, por exemplo **https://github.com/user/repo.git**

**O remote name já existe**

Esse erro significa que você tentou adicionar um remote com um nome que já existe no repositório local.

Para corrigir isso, é possível:

1. Usar um nome diferente para o novo remote

2. Renomear o remote existente 

O comando **git remote rename** tem dois argumentos:

O nome de um remote existente, como **origin**
Um novo nome para o remote, como **destination-name**

`git remote rename origin destination-name`

- Confirme o novo nome do remote

`git remote -v`

3. Excluir o remote existente

`git remote rm destination`

> Observação: o comando git remote rm não exclui o repositório do remote no servidor. Ele simplesmente remove o remote e suas referências do repositório local.
