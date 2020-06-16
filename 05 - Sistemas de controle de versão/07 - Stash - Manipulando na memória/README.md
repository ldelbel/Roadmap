# O Stash

O stash é um local de memória auxiliar, que você pode usar para salvar as alterações que ainda não deseja commitar ou se estiver trabalhando em uma branch e precisar mudar de branch para começar a trabalhar em outra coisa.

Antes de salvar qualquer coisa no stash, devemos adicionar os arquivos à área de teste, usando:

`git add .`

ou

`git add <diretórios ou nomes de arquivos específicos>`

Depois disso, quando todo o seu trabalho for realizado, basta executar o seguinte comando para mover tudo para a memória escondida. 

`git stash`

Como alternativa, você pode atribuir um nome específico aos arquivos que você trabalha, assim:

`git stash save "Implementando nova conexão com o banco de dados"`

Você pode verificar suas alterações em execução:

`git stash list`

Agora, para trazer suas alterações de volta à área de trabalho, você tem duas opções.

Para reaplicar modificações e mantê-las no stash, execute **git stash apply <stash position>**, neste caso:

`git stash aplicar stash @ {0}`

Para reaplicar mods removendo as alterações da parte superior do stash, use:

`git stash pop`

Se você deseja remover as alterações que não estão no topo, execute:

`git stash drop <posição>`

E, finalmente, se você deseja excluir tudo o que é mostrado por 'git stash list', basta executar:

`git stash clear`

