# Javadocs - Documentando o seu código

## Estrutura

A estrutura básica de um comentário de documentação tem como característica principal, o uso de uma barra e dois asteriscos /** no início e no seu final, possui um asterisco e uma barra */. 

~~~
/** Exemplo básico de um comentário em JavaDoc
 * com mais de uma linha.
 */
 ~~~

Por convenção, como comentei anteriormente, sugere-se alocar os blocos de comentários, antes da definição de uma classe, interface, atributos, ou métodos, dessa forma, criamos uma introdução conceitual ao referido elemento do código.

| Tag | Significado |
|--|--|
|@author| Especifica o autor da classe ou do método em questão.|
|@deprecated| 	Identifica classes ou métodos obsoletos. É interessante informar nessa tag, quais métodos ou classes podem ser usadas como alternativa ao método obsoleto.|
|@link| Possibilita a definição de um link para um outro documento local ou remoto através de um URL.|
|@param| Mostra um parâmetro que será passado a um método.|
|@return| Mostra qual o tipo de retorno de um método.|
|@see| 	Possibilita a definição referências de classes ou métodos, que podem ser consultadas para melhor compreender idéia daquilo que está sendo comentada.|
|@since| Indica desde quando uma classe ou métodos foi adicionado na aplicação.|
|@throws| Indica os tipos de exceções que podem ser lançadas por um método.|
|@version| Informa a versão da classe.|

### Negrito e Itálico

Outro exemplo interresante é a possibilidade de inserção de tags HTML, dentro do próprio comemtário JavaDoc, vamos ver esse exemplo na Listagem 04 que faz o uso das Tag's `<b>` e `<i>` para negritar e colocar em itálico, trechos de nosso comentário.
  
 ### Criando o Javadocs no Eclipse
 
1. No menu Project, escolha GenerateJavadoc.

2. Na caixa de diálogo Generate Javadoc, preencha o campo Javadoccommand, com o path do comando javadoc, que está dentro do diretório bin, onde o jdk foi instalado. Exemplo: C:Program FilesJavajdk1.6.0_21binjavadoc.exe

3. Para isto, clique no botão Configure, à direita, e procure pelo jdk.

4. Depois de preenchido o campo Javadoccommand, clique em Finish.

5. O javadoc será criado e o console apresentará uma saída.

