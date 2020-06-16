# CSS Básico

O CSS descreve como os elementos HTML devem ser exibidos na tela, papel ou em outra mídia.

CSS economiza muito trabalho . Ele pode controlar o layout de várias páginas da web de uma só vez.

CSS pode ser adicionado aos elementos HTML de três maneiras:

- Inline - usando o atributo style em elementos HTML.
- Interno - usando um `<style>` na seção `<head>`.
- Externo - usando um arquivo CSS externo.

A maneira mais comum de adicionar CSS é manter os estilos em arquivos CSS separados. No entanto, aqui usaremos o estilo interno e interno, porque isso é mais fácil de demonstrar e mais fácil para você experimentar.

## 1. CSS embutido

Um CSS embutido é usado para aplicar um estilo exclusivo a um único elemento HTML.

Este exemplo define a cor do texto do `<h1>` elemento para azul:

`<h1 style="color:blue;">This is a Blue Heading</h1>`

## 2. CSS interno

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

## 3. CSS externo

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

## 4. Fontes CSS

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

## 5. Borda CSS

`border` define uma borda em torno de um elemento HTML:

~~~ 
p {
  border: 1px solid powderblue;
}
~~~

## 6. Preenchimento CSS

A `padding` CSS define um preenchimento (espaço) entre o texto e a borda:

~~~
p {
  border: 1px solid powderblue;
  padding: 30px;
}
~~~ 

## 7. Margem CSS

A `margin` define uma margem (espaço) fora da borda:

~~~
p {
  border: 1px solid powderblue;
  margin: 50px;
}
~~~

## 8. Atributo id

Para definir um estilo específico para um elemento especial, adicione um `id` ao elemento:

`<p id="p01">I am different</p>`

Então defina um estilo para o elemento com o ID específico:

~~~
#p01 {
  color: blue;
}
~~~

Nota: O ID de um elemento deve ser exclusivo em uma página, portanto, o seletor de ID é usado para selecionar um elemento exclusivo!

## 9. O atributo da classe

Para definir um estilo para tipos especiais de elementos, adicione um atributo `class` ao elemento:

`<p class="error">I am different</p>`

Então defina um estilo para os elementos com a classe específica:

~~~
p.error {
  color: red;
}
~~~ 

## 10. Referências externas

As folhas de estilo externas podem ser referenciadas com um URL completo ou com um caminho relativo à página da web atual.

Este exemplo usa um URL completo para vincular a uma folha de estilos:

`<link rel="stylesheet" href="https://www.w3schools.com/html/styles.css">`

Este exemplo vincula a uma folha de estilos localizada na pasta html no site atual:

`<link rel="stylesheet" href="/html/styles.css">`

Este exemplo vincula a uma folha de estilos localizada na mesma pasta da página atual:

`<link rel="stylesheet" href="styles.css">`
