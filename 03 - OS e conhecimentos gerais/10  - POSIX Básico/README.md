# Posix

# 1. Introdução

O POSIX é um padrão para determinar interfaces comuns entre sistemas operacionais e é que uma forma de ditar várias 
características esperadas de um sistema operacional. 

Normalmente quando escrevemos e compilamos programas em C e C++ é comum tomarmos como verdade alguns comportamentos do sistema.

Por exemplo, quando estamos usando um interpretador de comando que seja compativel com POSIX, se espera que seja possível 
invocar o comando ls.

Na década de 70 e 80 começaram a surgir várias iniciativas de sistemas operacionais, e como cada empresa/desenvolvedor 
fazia suas próprias interfaces percebeu-se que uma padronização era necessária.

Para tentar tornar os programas mais compatíveis entre vários sistemas operacionais, o POSIX foi escrito. 

Ele basicamente define chamadas de sistema, comandos básicos (como awk e echo), um interpretador de comandos compatível 
com shell script, vários comportamentos esperados do sistema (como sinais, pipes, gerenciamento básico de processos, etc).

Esse padrão define por exemplo:

- Variáveis que devem existir ($PATH, $SHELL…)
- Dispositivos no /dev (/dev/null…)
- Diretórios padrão (FHS)
- Utilitários (cat, find…)

# 2. Compatibilidade

O que isso importa para o desenvolvedor? Normalmente quando vamos escrever um programa multiplataforma é necessário 
estudar quais interfaces estão implementadas e quais não. 

Normalmente temos bibliotecas que tratam estas diferenças para o programador.

É muito comum hoje evitar o uso de Shell Script quando vamos mirar no Windows, pois ele não tem suporte. 
Por isso é tão comum vermos scripts de configuração em Python ou ainda um script em shell e outro em bat.

# 3. Conceitos

- stdin
- stdout
- stderr
- pipes
