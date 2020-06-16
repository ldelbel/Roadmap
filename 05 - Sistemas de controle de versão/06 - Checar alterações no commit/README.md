# Checando alterações no commit

Então, você está olhando para o commit mais recente em sua branch e deseja saber exatamente o que mudou. 

Podemos começar a listar apenas os nomes dos arquivos que foram alterados:

`git diff HEAD~1 --name-only`

**HEAD ~ 1** significa que o Git comparará o último commit com o anterior.

**--name-only** lista apenas os nomes dos arquivos.  Se você remover esse argumento, verá os arquivos de texto diff.

Se você deseja comparar o commit mais recente com as três commits anteriores, listando as diferenças reais e não apenas os nomes dos arquivos:

`git diff HEAD~3`

Se você deseja comparar o commit antes da última com os quatro commit anteriores:

`git diff HEAD~1 HEAD~5`
