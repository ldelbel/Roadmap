# Como funcionam os browsers 

# 1.  Fluxo principal

- Os navegadores (clientes) fazem uma requisição HTTP a um servidor. O local aonde estão os recursos é passado através de um URI (identificador uniforme de recursos). 
- O cliente precisa descobrir com qual servidor ele vai se conectar. O servidor então indica qual é a máquina aonde a aplicação está instalada. 
- A máquina irá processar a requisição. 
- Normalmente será acessada uma página HTML, um arquivo de áudio, uma imagem e é retorna uma resposta.
- O navegador pegará os bytes de conteúdo e irá interpretar isso. 
   - A tag desenha uma logo, um fundo colorido... 
   - O navegador vai montando na tela esta resposta. 

# 2. Estrutura do navegador 

- Todas as áreas do display do navegador, exceto a janela principal em que você visualiza a página solicitada.
- O mecanismo de navegação , que faz a triagem das ações entre a interface do usuário e o mecanismo de renderização.
- O mecanismo de renderização, responsável pela exibição do conteúdo solicitado. 
  - Por exemplo, se o conteúdo solicitado estiver em HTML, ele é responsável pela análise do HTML e do CSS e pela exibição do conteúdo analisado na tela.
-Networking, utilizado para chamadas de rede, como solicitações HTTP. 
  - Possui interface independente de plataforma e sub-implementações para cada plataforma.
- Back-end da interface do usuário, utilizada para desenhar widgets básicos como caixas de combinação e janelas. 
  - Exibe uma interface genérica que não é específica à plataforma. Sob a interface, utiliza os métodos da interface do usuário do sistema operacional.
- Intérprete JavaScript Utilizado para analisar e executar o código JavaScript.
- Armazenamento de dados. Esta é uma camada persistente. O navegador precisa salvar dados de diversos tipos no disco rígido, como cookies. A especificação HTML (HTML5) define "banco de dados da web", que é um banco de dados completo (embora leve) no navegador.

![Componentes navegador](https://www.html5rocks.com/pt/tutorials/internals/howbrowserswork/layers.png)

# 3. HTML 

Contém as requisições são necessárias para renderizar a página.

- O DOM é uma estrutura na memória em que o navegador pega cada tag do código e representa como um objeto na memória.
- O navegador monta então uma árvore de objetos, caixas ou containers. 

Elementos da árvore: 

Página -> Seção -> Links -> Texto do link... 

Cada componente pertence a um componente superior.

Por padrão, o mecanismo de renderização pode exibir documentos e imagens HTML e XML. Ele pode exibir outros formatos por meio de plug-ins (ou extensões do navegador). Por exemplo, é possível exibir um PDF por meio de um plug-in do navegador para visualização de PDFs.

# 4. CSS

O CSS tem a função de modificar os objetos criados via HTML, seguindo um modelo de cascata. Aqui definimos larguras, alturas, cores, margens, etc. 

A responsividade é definida via CSS. 

- Leitura do CSS; 
- As regras estão de acordo com o seletor. 

# 5. Render Tree

O browser ainda precisa juntar as informações de HTML e CSS na renderização. A render tree junta as regras de CSS que batem com determinado elemento. 

Exemplo: 
- Um <div>  tem um tamanho de 50%. 
  - 50 % de quê? Da tela? De algum elemento? 
  - O navegador irá varrer a render tree para fazer o layout.
  - Serão definidos tamanho e posição de cada elemento. 
  - Só então, o primeiro pixel será impresso na tela. Esse processo será repetido por toda a tela. 
  
Nossos navegadores de referência – Firefox, Google Chrome e Safari – foram construídos com base em dois mecanismos de renderização. O Firefox utiliza o Gecko, um mecanismo de renderização criado pelo próprio Mozilla. O Safari e o Google Chrome usam o Webkit.

O Webkit é um mecanismo de renderização em código aberto que começou como um mecanismo para a plataforma Linux e foi modificado pela Apple para ser compatível com os sistemas Mac e Windows.

![Fluxo](https://www.html5rocks.com/pt/tutorials/internals/howbrowserswork/webkitflow.png)

# 6. Javascript 

O javascript ainda pode alterar os elementos no DOM, ou no CSS, ou ainda na fase de Layout. Ele é o principal responsável pela interatividade.

Um botão foi clicado? O que ocorre depois? 

Alguma cor será alterada ao passar o mouse por cima? Em que casos?

# 7. Ferramentas do browser 

- Leitor e interpretador de HTML;
- Leitor e interpretador de CSS; 
- Engine (interpretador) de javascript; 

# 8. Referências 

- [Como funcionam os navegadores Web?](https://www.youtube.com/watch?v=kDy62zaCHZE)
- [Como os navegadores funcionam: bastidores dos navegadores modernos](https://www.html5rocks.com/pt/tutorials/internals/howbrowserswork/)

