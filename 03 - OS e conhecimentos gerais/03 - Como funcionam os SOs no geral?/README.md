# Como funcionam os sistemas operacionais 

# 1. Funcionamento básico

Os sistemas operacionais possuem o seguinte funcionamento básico: 

- gerenciamento de processos;
- gerenciamento de memória;
- gerenciamento de recursos;
- entrada e saída de dados;
- sistema de arquivos.

# 2. Gerenciamento de recursos

Uma das tarefas com extrema importância atribuída ao sistema operacional é o gerenciamento de recursos, que 
tem a função de definir políticas para gerenciar o uso dos recursos de hardware pelos aplicativos, 
resolvendo disputas e conflitos. 

Vários programas de entrada de dados competem pela vez na CPU (Unidade Central de Processamento) e demandam memória, 
espaço em disco e largura. 

O sistema operacional tem a função de cuidar de cada aplicativo e para que os mesmos tenham recursos necessários 
para o melhor funcionamento e gerencia a capacidade limitada do sistema para que possa atender todas as 
necessidades de aplicativos e usuários.

# 3. Entrada e saída de dados

Sistemas operacionais controlam e gerenciam a entrada e saída (E/S) de dispositivos por três razões: 

- Primeiro, porque a maioria do hardware do dispositivo utiliza uma interface de baixo nível, a interface 
do software é complexa. 

- Em segundo lugar, porque um dispositivo é um recurso compartilhado, um sistema operacional fornece 
acesso de acordo com as políticas que tornam a partilha justa e segura. 

- Em terceiro lugar, um sistema operacional define uma interface de alto nível que esconde detalhes e 
permite que um programador possa usar um conjunto coerente e uniforme das operações ao interagir com os dispositivos.

O subsistema de E/S pode ser divididos em três peças conceituais:

- Uma interface abstrata que consiste funções de E/S de alto nível que os processos possam usar para executar I/O;
- Um conjunto de dispositivos físicos;
- Software de driver de dispositivo que conecta os dois.

De maneira geral, espera-se que os erros, como de leitura por exemplo, sejam tratados em níveis mais baixos, o mais próximo do hardware.

## 3.1. Tipos de conexão e de transferência de dados

Os dispositivos I/O podem se conectar de forma serial ou paralela. 

Na interface serial existe apenas uma linha por onde os dados trafegam. Na interface paralela os dados são transmitidos simultaneamente através das várias linhas para dados, a quantidade de linhas é um múltiplo de 1 byte (8 bits).

A transferência pode ser: 

- síncrona (bloqueante): após um read, o programa é suspenso até que os dados estejam disponíveis no buffer; 
- assíncrona (orientada à interrupção): a CPU inicia uma transferência e segue realizando outra atividade até ser sinalizada por um interrupção (o que acontece na maioria das E/S físicas).

O software de E/S é geralmente é dividido em camadas:

- A camada superior sendo a E/S vista pelo usuário; 
- a segunda camada o software que enxerga E/S da mesma forma, independente do dispositivo; 
- a terceira camada serve como interface padrão para drivers; 
- a ultima (mais inferior), composta pelos drivers propriamente ditos.

## 3.2. Utilização de buffer

O buffer pode ser utilizado em momentos em que os dados não podem ser armazenadas em seu destino final - como acontece com os pacotes que são recebidos pela rede e que precisam ser examinados. 

Outro exemplo são os dispositivos que apresentam restrições de tempo real, em que os dados devem ser antecipadamente colocados em um buffer de saída a fim de separar a taxa com a qual o buffer é preenchido. 

Essa taxa é calculada a partir da taxa com a qual ele é esvaziado. Dessa forma, evita-se a sobreposição do buffer.

Alguns dispositivos, como discos, podem ser usados por vários usuários simultaneamente. Outros, como dispositivos de fita, devem ser dedicados a um usuário até que este termine sua tarefas. 

O Sistema Operacional deve ser capaz de tratar ambos, de forma a evitar problemas.

## 3.3. Impasses (Deadlock)

Alguns dispositivos devem ser dedicados a um usuário até que este termine sua tarefa, não podendo ser interrompido para atender a solicitação de outro processo. 

Quando dois processos alocam recursos para si de forma que nenhum dos dois possa realizar a tarefa, mas também nenhum dos dois disponibilizam estes recursos antes de realizar a tarefa estes processos encontram-se em um impasse (deadlock) e permaneceram ali até que um fator externo os retire dessa situação. 

O princípio básico do impasse é: um conjunto de processos está em um impasse se cada processo do conjunto está esperando um evento que somente outro processo do conjunto pode causar. 

Como todos os processo estão esperando, nenhum deles jamais causará qualquer dos eventos que poderiam acordar qualquer dos outros membros do conjunto e todos os processos continuam a esperar eternamente.

## 3.4. Drivers

Um driver é uma camada de software que faz a comunicação do sistema operacional com o controlador do hardware que por sua vez faz a interface com o hardware. 

Ela é responsável por implementar as rotinas necessárias ao acesso e à gerencia de um dispositivo específico.

É necessário que o software de E/S realize a programação de registradores internos dos controladores que compõem a interface física dos dispositivos e implemente os respectivos tratadores de interrupção. 

Assim, cada tipo de dispositivo requer um driver apropriado. Essa camada fornece uma abstração a mais genérica possível para a camada superior, a de E/S independente do dispositivo.

Cada dispositivo de E/S ligado ao computador precisa de algum código específico do dispositivo para controlá-lo. Esse código  é chamado de driver do dispositivo.

Para acessar o hardware do dispositivo, o driver normalmente deve ser parte do núcleo do SO.

Os sistemas operacionais geralmente classificam os drivers dentre algumas poucas categorias. As categorias mais comuns são: 

- dispositivos de bloco: os quais contêm vários blocos de dados que podem ser endereçados independentemente; 
- dispositivos de caractere: os quais geram ou aceitam uma sequencia de caracteres.

A maioria dos SOs define: 

- uma interface-padrão para todos os drivers de blocos;
- uma segunda interface-padrão para todos os drivers de caracteres. 

Essas interfaces consistem em um nímero de procedimentos que o restante do so pode utilizar para fazer o driver trabalhar para ele.

Um driver de dispositivo apresenta várias funções: a mais óbvia é aceitar e executar requisições abstratas, de leitura ou gravação, de um software independente de um dispositivo localizado na camada acima da camada de drivers dos dispositivos. 

# 4. Sistema de arquivos

Na prática, um sistema de arquivo (file system, do inglês) é um conjunto de estruturas lógicas, ou seja, feitas diretamente via software, que permite ao sistema operacional ter acesso e controlar os dados gravados no disco.

Cada sistema operacional lida com um sistema de arquivos diferente e cada sistema de arquivos possui as suas peculiaridades, como limitações, qualidade, velocidade, gerenciamento de espaço, entre outras características. 

É o sistema de arquivos que define como os bytes que compõem um arquivo serão armazenados no disco e de que forma o sistema operacional terá acesso aos dados.

## 4.1. FAT

As primeiras versões do Windows usavam um sistema de arquivo chamado FAT16. O nome FAT deriva da sigla, em inglês, File Allocation Table. Este sistema de arquivos possui uma tabela que serve como um mapa de utilização do disco.

O numeral 16 deriva do fato de que cada posição no disco utiliza uma área variável de 16 bits. O sistema FAT16 trabalha com setores de alocação, também conhecidos como clusters. 

Cada cluster tem um tamanho específico, dependendo da capacidade total do disco rígido. O grande problema é que este padrão não lidava com discos maiores que 2 GB e os clusters eram muito grandes, o que acabava ocasionando um desperdício de espaço.

Para diminuir o desperdício, foi lançada uma atualização, chamada de FAT32. 

Este sistema de arquivos passou a ser usado no Windows 95 até o Windows Me. Nele, o tamanho dos clusters é menor, desperdiçando menos espaço. No entanto, o padrão 32 trazia um outro problema: era muito lento. Em geral, era 6% mais lento que o sistema FAT16.

Para completar a lista de desvantagens, em discos formatados com o sistema de arquivos FAT32, não é possível ter partições maiores do que 32 GB. 

Para piorar a situação, o sistema é incapaz de reconhecer arquivos maiores que 4 GB em sistemas FAT32. Além disso, é totalmente inseguro. Qualquer pessoa com acesso ao disco pode ler todos os arquivos.

## 4.2. NTFS

Para resolver todos esses problemas, foi criado o sistema de arquivos NTFS (New Technology File System – Nova Tecnologia de Sistema de Arquivos). O NTFS é mais seguro, possui recursos de recuperação de erros no disco, suporte para discos rígidos de maior capacidade, suporte a configuração de permissões e criptografia.

A partir do NTFS foi possível configurar permissões para cada tipo de arquivo. Isso impede que usuários sem autorização tenham acesso a determinados arquivos em seu computador. 

Além disso, o padrão não usa clusters, portanto, não há desperdício de espaço. Esse sistema de arquivos deu tão certo que é utilizado até hoje em sistemas Windows, tal como o mais recente Windows 10.
