# HTML

# 1. Introdução 

HTML é a linguagem de marcação padrão para criar páginas da Web.

-   HTML significa Hyper Text Markup Language
-   HTML descreve a estrutura de uma página da Web
-   HTML consiste em uma série de elementos
-   Os elementos HTML informam ao navegador como exibir o conteúdo
-   Elementos HTML são representados por tags
-   As tags HTML rotulam partes do conteúdo, como "cabeçalho", "parágrafo", "tabela" e assim por diante
-   Os navegadores não exibem as tags HTML, mas as usam para renderizar o conteúdo da página

Exemplo: 
~~~
<!DOCTYPE html>
<html>
<head>
<title>Page Title</title>
</head>
<body>

<h1>My First Heading</h1>
<p>My first paragraph.</p>

</body>
</html>
~~~

Elementos: 

-   A `<!DOCTYPE html>`declaração define este documento como HTML5
-   O `<html>`elemento é o elemento raiz de uma página HTML
-   O `<head>`elemento contém meta informações sobre o documento
-   O `<title>`elemento especifica um título para o documento
-   O `<body>`elemento contém o conteúdo da página visível
-   O `<h1>`elemento define um cabeçalho grande
-   O `<p>`elemento define um parágrafo

Versões: 

| Versão | Ano |
|--|--|
|HTML | 1991 | 
| HTML 2.0| 1995 |
|HTML 3.2 | 1997|
| HTML 4.01 |1999 |
|XHTML  |2000|
| HTML5 | 2014 | 

# 2. Cabeçalhos 

Os cabeçalhos HTML são definidos com as tags `<h1>` a `<h6>`.

A tag `<h1>` define o cabeçalho mais importante e `<h6>` define o cabeçalho menos importante: 

~~~
<h1>This is heading 1</h1>
<h2>This is heading 2</h2>
<h3>This is heading 3</h3>
~~~

Os navegadores adicionam automaticamente algum espaço em branco (uma margem) antes e depois de um cabeçalho.

Cada cabeçalho HTML tem um tamanho padrão. No entanto, você pode especificar o tamanho de qualquer cabeçalho com o `style`, usando a propriedade `font-size` do CSS :

`<h1 style="font-size:60px;">Heading 1</h1>`

## 2.1. Quebra temática `<hr>`

A `<hr>` define uma quebra temática em uma página HTML e é mais frequentemente exibida como uma regra horizontal.
O `<hr>` é usado para separar o conteúdo (ou definir uma alteração) em uma página HTML:

~~~ 
<h1>This is heading 1</h1>
<p>This is some text.</p>
<hr>
<h2>This is heading 2</h2>
<p>This is some other text.</p>
<hr>
~~~

Isto irá gerar uma linha separadora entre os conteúdos. 

## 2.2. Elemento `<head>`

O `<head>` é um contêiner para metadados, que são dados sobre o documento HTML. Os metadados **não são exibidos**.

O `<head>` é colocado entre a `<html>` e a `<body>`: 

~~~
<!DOCTYPE html>
<html>

<head>
  <title>My First HTML</title>
  <meta charset="UTF-8">
</head>

<body>
~~~

Os metadados geralmente definem o título do documento, o conjunto de caracteres, os estilos, os scripts e outras metainformações.

# 3. Parágrafos

Os parágrafos HTML são definidos com a `<p>`:

~~~
<p>This is a paragraph.</p>
<p>This is another paragraph.</p>
~~~

Os navegadores adicionam automaticamente algum espaço em branco (uma margem) antes e depois de um parágrafo.

## 3.1. Exibição do HTML

Você não terá certeza de como o HTML será exibido no navegador, pois telas grandes ou pequenas e janelas redimensionadas criarão resultados diferentes.

Com o HTML, você também não pode alterar a saída adicionando espaços ou linhas extras ao seu código HTML.

O navegador removerá espaços e linhas extras quando a página for exibida:

~~~
<p>
This paragraph
contains a lot of lines
in the source code,
but the browser
ignores it.
</p>

<p>
This paragraph
contains         a lot of spaces
in the source         code,
but the        browser
ignores it.
</p>
~~~

## 3.2. Título 

Aqui, um `title` é adicionado ao `<p>`. O valor do atributo title será exibido como uma dica de ferramenta quando você passa o mouse sobre o parágrafo:

~~~
<p title="I'm a tooltip">
This is a paragraph.
</p>
~~~

## 3.3. Linebreak `<br>`

Elementos HTML sem conteúdo são chamados de elementos vazios.

`<br>`é um elemento vazio sem uma tag de fechamento (a `<br>` tag define uma quebra de linha):

`<p> This is a <br> paragraph with a line break.</p>`

Elementos vazios podem ser "fechados" na tag de abertura assim: `<br />`.

O HTML5 não requer que elementos vazios sejam fechados. Mas se você deseja uma validação mais rigorosa ou se precisa tornar seu documento legível por analisadores XML, feche todos os elementos HTML adequadamente.

## 3.4. Pré-formatação `<pre>`

O `<pre>` define o texto pré-formatado.

O texto dentro de um `<pre>` é exibido em uma fonte de largura fixa (geralmente Courier) e preserva os espaços e as quebras de linha:

~~~
<pre>
  My Bonnie lies over the ocean.

  My Bonnie lies over the sea.

  My Bonnie lies over the ocean.

  Oh, bring back my Bonnie to me.
</pre>
~~~ 

Output: 

~~~
  My Bonnie lies over the ocean.

  My Bonnie lies over the sea.

  My Bonnie lies over the ocean.
  
  Oh, bring back my Bonnie to me.
~~~

# 4. Texto

## 4.1. Texto menor `<small>`

O `<small>` define texto menor:

`<h2>HTML <small>Small</small> Formatting</h2>`

## 4.2. Texto marcado `<mark>` (Marcador de texto)

O `<mark>` define o texto marcado/destacado:

`<h2>HTML <mark>Marked</mark> Formatting</h2>`

## 4.3. Texto deletado `<del>` (Riscado)

O `<del>` define o texto excluído/removido.

`<p>My favorite color is <del>blue</del> red.</p>`

## 4.4. Texto sublinhado `<ins>` 

O `<ins>` define o texto sublinhado.

`<p>My favorite <ins>color</ins> is red.</p>`

## 4.5. Texto subscrito `<sub>`

O `<sub>`elemento HTML define o texto subscrito.

`<p>This is <sub>subscripted</sub> text.</p>`

## 4.6. Texto sobrescrito `<sup>`

O `<sup>` define o texto sobrescrito.

`<p>This is <sup>superscripted</sup> text.</p>`

## 4.7. Formatação strong e enfatizada

O HTML também define elementos especiais para definir texto com um significado especial. Ele também faz uso de elementos como `<b>`e `<i>`para formatar a saída, como texto em negrito ou itálico.

O `<strong>`elemento HTML define texto forte , com importância semântica "forte" adicionada.
`<strong>This text is strong</strong>`

No entanto, esta é uma indicação de como algo deve ser entendido. "Forte" pode (e geralmente significa) "negrito" em um navegador, mas também **pode significar um tom mais baixo** para um programa de conversação como o Jaws (para pessoas cegas) ou ser representado por um sublinhado.

O mesmo vale para `<em>` que define o texto enfatizado, com maior importância semântica.

`<em>This text is emphasized</em>`

## 4.8. Comentário

Você pode adicionar comentários à sua fonte usando a seguinte sintaxe:

`<!-- Write your comments here -->`

## 5. Elementos interativos

## 5.1. Links

Os links HTML são definidos com a <a>:

`<a href="https://www.w3schools.com">This is a link</a>`

 - O destino do link é especificado no `href` 
 - Os atributos são usados para fornecer informações adicionais sobre elementos HTML.

## 5.2. Imagens

Imagens HTML são definidas com a <img>.

O arquivo de origem (src), o texto alternativo ( alt) width e height são fornecidos como atributos:

`<img src="w3schools.jpg" alt="W3Schools.com" width="104" height="142">`

## 5.3. Botão

Os botões HTML são definidos com a <button>:

`<button>Click me</button>`

## 5.4. Listas

As listas HTML são definidas com a tag (lista `<ul>`não ordenada / marcador) ou `<ol>`(lista ordenada / numerada), seguida pelas `<li>`tags (itens da lista):

    <ul>  
    <li>Coffee</li>  
    <li>Tea</li>  
    <li>Milk</li>  
    </ul>  
      
    <ol>  
    <li>Coffee</li>  
    <li>Tea</li>  
    <li>Milk</li>  
    </ol>

# 6. Atributos

## 6.1. href

Os links HTML são definidos com a `<a>`tag. O endereço do link é especificado no `href`:

`<a href="https://www.w3schools.com">This is a link</a>`

## 6.2. src

Imagens HTML são definidas com a `<img>`.

O nome do arquivo da fonte da imagem é especificado no `src`:
`<img src="img_girl.jpg">`

## 6.3. width e height
 As imagens HTML também têm `width` e `height`, que especificam a largura e a altura da imagem:

`<img src="img_girl.jpg" width="500" height="600">`

A largura e a altura são especificadas em pixels por padrão, então width = "500" significa 500 pixels de largura.

## 6.4. alt
O `alt` especifica um texto alternativo a ser usado, se uma imagem não puder ser exibida.

O valor do altatributo pode ser lido pelos leitores de tela. Dessa forma, alguém "ouvindo" a página da Web, por exemplo, uma pessoa com deficiência visual, pode "ouvir" o elemento.

`<img src="img_girl.jpg" alt="Girl with a jacket">`

O `alt` também é útil se a imagem não puder ser exibida (por exemplo, se ela não existir):

## 6.5. style

O `style` é usado para especificar o estilo de um elemento (como cor, fonte, tamanho) e possui a seguinte sintaxe:
`<tagname style="property:value;">`

### 6.5.1.  Color

`<p style="color:red">This is a paragraph.</p>`

### 6.5.2.  Background Color

A propriedade CSS `background-color` define a cor de plano de fundo para um elemento HTML.

Este exemplo define a cor de fundo de uma página para `powderblue`:

~~~
<body style="background-color:powderblue;">

<h1>This is a heading</h1>
<p>This is a paragraph.</p>

</body>
~~~ 

### 6.5.3.  Font family

A propriedade CSS `font-family` define a fonte a ser usada para um elemento HTML:

~~~
<h1 style="font-family:verdana;">This is a heading</h1>
<p style="font-family:courier;">This is a paragraph.</p>
~~~ 

### 6.5.4.  Tamanho do texto

A propriedade CSS `font-size` define o tamanho do texto para um elemento HTML:

~~~
<h1 style="font-size:300%;">This is a heading</h1>
<p style="font-size:160%;">This is a paragraph.</p>
 Alinhamento de texto
 ~~~ 
 
### 6.5.5.  Alinhamento horizontal

A propriedade CSS `text-align` define o alinhamento horizontal do texto para um elemento HTML:

~~~
<h1 style="text-align:center;">Centered Heading</h1>
<p style="text-align:center;">Centered paragraph.</p>
~~~

## 6.6. lang

O idioma do documento pode ser declarado na `<html>`.

O idioma é declarado com o `lang`

A declaração de um idioma é importante para aplicativos de acessibilidade (leitores de tela) e mecanismos de pesquisa:

~~~
<!DOCTYPE html>
<html lang="en-US">
<body>

...

</body>
</html>
~~~ 

As duas primeiras letras especificam o idioma (en). Se houver um dialeto, adicione mais duas letras (EUA).

# 7. Citações

## 7.1. Citações curtas  `<q>`

O `<q>` elemento HTML define uma cotação curta.

Os navegadores geralmente inserem aspas ao seu redor.

`<p>WWF's goal is to: <q>Build a future where people live in harmony with nature.</q></p>`

## 7.2. Cotações `<blockquote>`

O `<blockquote>` define uma seção que é citada de outra fonte.

Navegadores geralmente tabulam `<blockquote>`.

~~~
<p>Here is a quote from WWF's website:</p>
<blockquote cite="http://www.worldwildlife.org/who/index.html">
For 50 years, WWF has been protecting the future of nature.
The world's leading conservation organization,
WWF works in 100 countries and is supported by
1.2 million members in the United States and
close to 5 million globally.
</blockquote>
~~~

## 7.3. Abreviações `<abbr>`

O `<abbr>` define uma abreviação ou acrônimo.

As abreviações de marcação podem fornecer informações úteis para navegadores, sistemas de tradução e mecanismos de busca. 
 
`<p>The <abbr title="World Health Organization">WHO</abbr> was founded in 1948.</p>`

No navegador, ao passar o mouse em cima de `WHO` será exibido: `World Health Organization`. 

## 7.4. Informações de contato `<address>`

O `<address>` define as informações de contato (autor/proprietário) de um documento ou artigo.

O `<address>` geralmente é exibido em itálico. A maioria dos navegadores adicionará uma quebra de linha antes e depois do elemento. Usualmente é exibido ao fim da página. 

~~~
<address>
Written by John Doe.<br>
Visit us at:<br>
Example.com<br>
Box 564, Disneyland<br>
USA
</address>
~~~

## 7.5. Citação de fonte `<cite>`

O `<cite>` define a fonte de um trabalho.

Os navegadores geralmente exibem `<cite>` em itálico.

`<p><cite>The Scream</cite> by Edvard Munch. Painted in 1893.</p>`

## 7.6. Reversão `<bdo>`

O `<bdo>` reverte o sentido de um texto.

`<bdo dir="rtl">This text will be written from right to left</bdo>`

# 8. Color

[Hexadecimais](https://www.w3schools.com/colors/colors_hex.asp) de cor

## 8.1. Cor de fundo

~~~
<h1 style="background-color:DodgerBlue;">Hello World</h1>
<p style="background-color:Tomato;">Lorem ipsum...</p>
~~~

## 8.2. Cor do texto

~~~
<h1 style="color:Tomato;">Hello World</h1>
<p style="color:DodgerBlue;">Lorem ipsum...</p>
<p style="color:MediumSeaGreen;">Ut wisi enim...</p>
~~~

## 8.3. Cor da borda

~~~
<h1 style="border:2px solid Tomato;">Hello World</h1>
<h1 style="border:2px solid DodgerBlue;">Hello World</h1>
<h1 style="border:2px solid Violet;">Hello World</h1>
~~~ 

# 9. CSS Básico

O CSS descreve como os elementos HTML devem ser exibidos na tela, papel ou em outra mídia.

CSS economiza muito trabalho . Ele pode controlar o layout de várias páginas da web de uma só vez.

CSS pode ser adicionado aos elementos HTML de três maneiras:

- Inline - usando o atributo style em elementos HTML.
- Interno - usando um `<style>` na seção `<head>`.
- Externo - usando um arquivo CSS externo.

A maneira mais comum de adicionar CSS é manter os estilos em arquivos CSS separados. No entanto, aqui usaremos o estilo interno e interno, porque isso é mais fácil de demonstrar e mais fácil para você experimentar.

## 9.1. CSS embutido

Um CSS embutido é usado para aplicar um estilo exclusivo a um único elemento HTML.

Este exemplo define a cor do texto do `<h1>` elemento para azul:

`<h1 style="color:blue;">This is a Blue Heading</h1>`

## 9.2. CSS interno

Um CSS interno é definido na seção `<head>` de uma página HTML, dentro de um `<style>`:

~~~
<!DOCTYPE html>
<html>
<head>
<style>
body {background-color: powderblue;}
h1   {color: blue;}
p    {color: red;}
</style>ead>
<body>

<h1>This is a heading</h1>
<p>This is a paragraph.</p>

</body>
</html>
~~~

## 9.3. CSS externo

Um template externo é usada para definir o estilo para muitas páginas HTML.

Com uma folha de estilos externa, você pode alterar a aparência de um site inteiro, alterando um arquivo!

Para usar uma folha de estilos externa, adicione um link a ela na seção `<head>` da página HTML:

~~~
<!DOCTYPE html>
<html>
<head>
  <link rel="stylesheet" href="styles.css">
</head>
<body>

<h1>This is a heading</h1>
<p>This is a paragraph.</p>

</body>
</html>
~~~

Uma folha de estilos externa pode ser escrita em qualquer editor de texto. O arquivo não deve conter nenhum código HTML e deve ser salvo com uma extensão `.css`.

Aqui está como o `styles.css` se parece:

~~~
body {
  background-color: powderblue;
}
h1 {
  color: blue;
}
p {
  color: red;
}
~~~

## 9.4. Fontes CSS

- `color` define a cor do texto a ser usada.
- `font-family` define a fonte a ser usada.
- `font-size` define o tamanho do texto a ser usado.

~~~
<!DOCTYPE html>
<html>
<head>
<style>
h1 {
  color: blue;
  font-family: verdana;
  font-size: 300%;
}
p  {
  color: red;
  font-family: courier;
  font-size: 160%;
}
</style>
</head>
<body>

<h1>This is a heading</h1>
<p>This is a paragraph.</p>

</body>
</html>
~~~

## 9.5. Borda CSS

`border` define uma borda em torno de um elemento HTML:

~~~ 
p {
  border: 1px solid powderblue;
}
~~~

## 9.6. Preenchimento CSS

A `padding` CSS define um preenchimento (espaço) entre o texto e a borda:

~~~
p {
  border: 1px solid powderblue;
  padding: 30px;
}
~~~ 

## 9.7. Margem CSS

A `margin` define uma margem (espaço) fora da borda:

~~~
p {
  border: 1px solid powderblue;
  margin: 50px;
}
~~~

## 9.8. Atributo id

Para definir um estilo específico para um elemento especial, adicione um `id` ao elemento:

`<p id="p01">I am different</p>`

Então defina um estilo para o elemento com o ID específico:

~~~
#p01 {
  color: blue;
}
~~~

Nota: O ID de um elemento deve ser exclusivo em uma página, portanto, o seletor de ID é usado para selecionar um elemento exclusivo!

## 9.9. O atributo da classe

Para definir um estilo para tipos especiais de elementos, adicione um atributo `class` ao elemento:

`<p class="error">I am different</p>`

Então defina um estilo para os elementos com a classe específica:

~~~
p.error {
  color: red;
}
~~~ 

## 9.10. Referências externas

As folhas de estilo externas podem ser referenciadas com um URL completo ou com um caminho relativo à página da web atual.

Este exemplo usa um URL completo para vincular a uma folha de estilos:

`<link rel="stylesheet" href="https://www.w3schools.com/html/styles.css">`

Este exemplo vincula a uma folha de estilos localizada na pasta html no site atual:

`<link rel="stylesheet" href="/html/styles.css">`

Este exemplo vincula a uma folha de estilos localizada na mesma pasta da página atual:

`<link rel="stylesheet" href="styles.css">`
