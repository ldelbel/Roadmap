# HTML

## 1. Tag `<!DOCTYPE html>`

Avisa o navegador que a documentação será em HTML5. 
`<!DOCTYPE html> `

### 1.1 Tag `<html>`:

* informa ao navegador que este é um documento HTML.
* representa a raiz de um documento HTML.
* é o contêiner para todos os outros elementos HTML (exceto a tag `<!DOCTYPE>`).
  
Pode-se declarar linguagem:
~~~
<html lang="pt-br">
//Codigo
~~~

## 2. Informações gerais `<Head>`:

Elemento que providencia informações gerais (metadados) sobre o documento, incluindo seu título e links para scripts e folhas de estilos.

Essa tag delimita o cabeçalho do documento. Não possui nenhum valor visível, porém é capaz de transmitir ao navegador diversas informações muito úteis e essenciais a uma boa apresentação do seu documento HTML;

### 2.1 Metadados `<meta>`

O elemento HTML <meta> define qualquer informação de metadados que não podem ser definidos por outros elementos HTML. (`<base>, <link>, <script>, <style> ou <title>`).

Exemplo: a informação `charset= ”UTF-8″`, que garante a compatibilidade do código com os caracteres de padrão latino americano.

`<meta charset="utf-8">`

### 2.2 Título `<title>`

Esta tag representa o título exibido no navegador, que identifica a página html. 

## 3. Corpo `<body>`

Usam-se elementos HTML de conteúdo textual para se organizar blocos ou seções de conteúdo postos entre as tags de abertura `<body>` e fechamento `</body>`

### 3.1 Introdução `<header>`

O elemento HTML <header> representa um grupo de suporte introdutório ou navegacional. Pode conter alguns elementos de cabeçalho mas também outros elementos como um logo, seções de cabeçalho, formulário de pesquisa, e outros.

### 3.2 Divisão de página `<div>`

Define uma divisão da página. Desta forma, funciona como um container para conteúdo de fluxo. Uma vez que não possui um valor semântico, é muito utilizado para organizar melhor o conteúdo. 

Exemplo: 

`<div> "Hello World" </div>`

Com isso, sempre que houver um novo bloco, a formatação será restrita ao bloco. 

### 3.3 Rodapé `<footer>` 

O elemento HTML de Rodapé. Normalmente um rodapé contém informações sobre o autor da seção de dados, direitos autorais ou links para documentos relacionados.

### 3.4 Parágrafo `<p>`

A tag `<p>` serve para incluir um parágrafo, anteriormente ao texto. (Pula linha)

Exemplo: 
~~~
>>> Olá mundo! 
>>> <p> Novo parágrafo </p>

Olá mundo! 

Novo parágrafo
~~~

#### 3.4.1 Fonte do texto

~~~
<!-- Declarando uma única fonte -->
<p style="font-family: 'Times New Roman'">Olá, mundo!</p>
 
<!-- Declarando duas possíveis fontes -->
<p style="font-family: 'Helvetica, Arial'">Olá, mundo novamente!</p>
~~~

#### 3.4.2 Estilo de texto

Alterando a cor de um texto:
~~~
<!-- Esse exemplo aplica a cor vermelha a todos os elementos do tipo parágrafo. -->
<style>
p { color: red; }
</style>
~~~ 

Alterando a cor do fundo: 
~~~
<style>
body { background-color: red; }
</style>
~~~ 

Exemplo completo: 
~~~
<!DOCTYPE html>
<html>
<head>
    <title>Meus estilos</title>
    <style>
        body { 
            background-color: red; 
            color:green; 
        }
    </style>
</head>
<body>
    <p>Olá mundo</p>
</body>
</html>
~~~ 

#### 3.4.3 Outras formatações de parágrafos:

~~~ 
<p>
    <b>Texto em negrito</b><br>
    <i>Texto em itálico</i><br>
    <u>Texto sublinhado</u><br>
    <sub>Texto subscrito</sub><br>
    <sup>Texto sobrescrito</sup><br>
    <big>Texto com fonte maior do que o padrão</big><br>
    <small>Texto com fonte menor do que o padrão</small><br>
    <em>Texto em itálico</em><br>
    <strong>Texto em negrito</strong>
</p>
~~~ 

### 3.5 Quebra de linha (Broke) `<br>` 

Esta tag quebra uma linha, mas sem representar um novo parágrafo. 

Exemplo: 
~~~
>>> Olá mundo! 
>>> <br> Novo parágrafo </br>

Olá mundo! 
Novo parágrafo
~~~

### 3.6 Linha horizontal `<hr>` 

Cria uma linha horizontal entre duas linhas. 

Exemplo: 
~~~
>>> Olá mundo! 
>>> <hr>
>>> Novo parágrafo

Olá mundo! 
--------------------------------------------------------------------------------------------------
Novo parágrafo
~~~

### 3.7 Títulos e subtítulos `<h1...h5>`

Cria títulos por hierarquia de tamanho, sendo h1 o maior tamanho possível e h5 o menor tamanho possível. 

### 3.8 Imagem `<img>` 

Quando estiver num mesmo diretório: 
~~~
<!-- Altura e largura de 600px na imagem. -->
<img src = "imagem.png" height="600px" width="600px">
~~~

O ideal é que seja incluso apenas um parâmetro, pois o navegador corrige o outro automaticamente. 

### 3.9 Listas `<ol> e <ul>`

Cada elemento interno às listas deve ser demarcado com a tag `<li>`. 

#### 3.9.1 Listas ordenadas `<ol>`

~~~
<!-- Lista ordenada -->
<ol>
<li>Primeiro elemento</li>
<li>Segundo elemento</li>
<li>Terceiro elemento</li>
</ol>
~~~

#### 3.9.2 Listas não-ordenadas `<ul>`

~~~
<!-- Lista não ordenada -->
<ul>
<li>Primeiro elemento</li>
<li>Segundo elemento</li>
<li>Terceiro elemento</li>
</ul>
~~~

### 3.10 Links externos `<a>`

Ele indica o alvo do link, seja uma URL ou um fragmento de URL. 

Um fragmento de URL é um nome precedido por  uma cerquilha (#), a qual especifica um destino interno (um ID) dentro do documento atual. URLs não precisam se limitar à documentos Web baseados em HTTP.

Exemplo: Você pode usar o fragmento especial "top" para criar um link para o topo da página.

~~~ 
 <a href="#top">Volte ao topo </a>
~~~ 

Exemplo: Acesso a link externo: 

~~~
<!-- Lista não ordenada -->
<a href = "http://google.com.br"> Google </a> 
~~~ 

### 3.11 Tabelas `<table>` 

* `<table>` define o momento de início da tabela. 
* `<tr>` define quando começará uma nova linha da tabela. 
* `<th>` define linhas de célula-cabeçalho. 
* `<td>` define linhas de célula-descrição. 

### 3.12 Formulários `<form>`

##### 3.12.1 Atributo Method

Este atributo define o método que será realizado pelo formulário, get, post, etc... 

##### 3.12.2 Atributo Action 

Exemplo: 
~~~
<form action="/action_page.php" method="get">
  First name: <input type="text" name="fname"><br>
  Last name: <input type="text" name="lname"><br>
  <input type="submit" value="Submit">
</form>
~~~

Ao enviar uma requisição, envia dados do formulário para um arquivo chamado "/action_page.php" (para processar a entrada). 

No HTML5, o atributo action não é mais necessário.

#### 3.12.3 Tag Input `<input ...>`

###### 3.12.3.1 Atributo type 

Define o tipo de dado a ser preenchido internamente a um campo do formulário. 

* text: arquivo de texto. 
* password: campo não visível, para proteção de senha. 
* hidden: campo oculto
* radio: para escolha de listas com apenas uma opção.
* checkbox: para escolha de listas com caixas de seleção (mais de uma opção)
* submit: Botão de submit para envio. 

###### 3.12.3.2 Atributo name 

Nome do campo a ser preenchido. 

###### 3.12.3.3 Atributo placeholder 

Este atributo detalha o tipo de informação que deve ser preenchida internamente ao campo. Será sobrescrito pelo dado digitado. 

#### 3.12.4 Entrada de dados em formulários `<select>`

###### 3.12.4.1 option

Permite a inclusão de listas de respostas pré-definidas 

~~~ 
<select name="selecao">
  <option value= "1"> Opção 1 </option>
  <option value= "2"> Opção 2 </option>
  </select>
~~~ 

**value** define a posição da caixa de seleção e seu valor. 

