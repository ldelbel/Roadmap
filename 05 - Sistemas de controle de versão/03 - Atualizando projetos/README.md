# Atualizando projetos

## 1. Atualizar seu repositório local em relação ao repositório remoto

`git pull origin master`

* ATENÇÃO: este comando só é necessário se você criou o .gitignore pelo Github.

## 2. Verificar arquivos

`git status`

## 3. Adicionar todos arquivos ao stage

`git add . `

## 4. Remover um arquivo do add

### 5.1 Remover todos arquivos

`git reset HEAD`

ou 

`git reset HEAD arquivo1 arquivo2 ...`

De maneira mais detalhada, o que o comando 'reset' faz é modificar o HEAD (último commit no repositório local) para o branch especificado. Como acima não especificamos nenhum branch, ele tentará resetar o HEAD atual para o próprio HEAD. 

Isto é estranho, mas funciona porque como o parâmetro 'mode'  não foi passado também, o 'reset' assume que iremos usar o valor 'mixed', que diz que os arquivos devem ser resetados, mas as modificações existentes nos arquivos em questão não devem ser desfeitas.

### 5.2 Remover um arquivo em específico

Opcionalmente, para remover os arquivos da lista de commit, pode-se também usar o comando 'rm' com o parâmetro --cached. Porém, só funciona para arquivos modificados e que foram colocados na lista de commit:

`git rm --cached seuarquivo.ext`

O comando acima sem o --cached remove o arquivo do stage area. Porém, quando usado com o parâmetro --cached, só irá remover do index, por isso o comando funciona.

## 6. Salvar uma nova versão do projeto.

`git commit -m "Projeto criado" `

## 7. Enviar o repositório local para o repositório remoto

`git push -u origin master`

* Nota: nas próximas vezes basta fazer: git push
