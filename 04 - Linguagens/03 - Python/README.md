# Python Basics

Como funciona? 

1. Desenvolve o script
2. Chama o interpretador python
3. Python compila e exibe resultados na tela 

## 1. Configuração

1.1 Instalar o pydev via marketplace. 

1.2 Em **window>>Preferences>>Python**, escolha o interpretador python. 

1.3 Crie um novo projeto: Botão direito + new Pydev module

Alternativa: [Google Colab](https://colab.research.google.com/)

## 2. Impressão em tela

### 2.1 Comentários

Usa-se neste caso o `#` ou ` """ ` (linhas de vários comentários). 

### 2.2 Coding 

Para que o python permita o uso de acentos e outros, precisa-se informar o **encoding utf-8**. 

`# -*- coding: utf-8 -*-` 

### 2.3 Print()

Podemos imprimir um inteiro diretamente: 
~~~ 
>>> print (5)
5
~~~

Podemos fazer isso com variáveis.

~~~ 
>>> a = 2
>>> b = 3
>>> print ( a + b )
5
~~~

Podemos formatar a saída...
~~~ 
>>> print("%.2f" % 5)
5.00
>>> print("%.5f" % 5)
5.00000
~~~

Podemos compor uma string...
~~~ 
>>> r = "vermelho"
>>> g = "verde"
>>> b = "azul"
>>> print("As cores básicas são: %s, %s e %s" % (r, g, b))
# As cores básicas são: vermelho, verde e azul
~~~

O símbolo `%` indica que as variáveis a seguir substituirão as variáveis anteriores.  

### 2.4 Format

O método format() serve para criar uma string que contem campos entre chaves a serem substituídos pelos argumentos de format. Abaixo um exemplo executado no ambiente interativo:

~~~
>>> str = '{0} é um {1} companheiro, {1} companheiro é o {0}, ninguém pode negar'
>>> str.format('Paulo', 'bom')
'Paulo é um bom companheiro, bom companheiro é o Paulo, ninguém pode negar'
>>> str.format('João', 'ótimo')
'João é um ótimo companheiro, ótimo companheiro é o João, ninguém pode negar'
>>>
~~~ 

## 3. Operações matemáticas 

### 3.1 Comuns

~~~
print(2 + 2)
print(2 - 2)
print(2 * 2)
print(2 / 2)
~~~

### 3.2 Exponenciação

Dois ao quadrado: 

`print(2 ** 2)`

### 3.3 Módulo (ou resto da divisão) 

10/3 = 3, resta 1. 

~~~ 
>> print(10 / 3)
1
~~~ 

## 4. Operações lógicas

Sintaxes: 

`and, or e not` 

## 5. Listas

Considere: 

~~~
lista1 = ["abacaxi", "melancia", "abacate"]
lista2 = [1,2,3,4,5]
lista3 = ["abacaxi", 2, 8.50, True]
~~~ 

### 5.1 Impressão completa

~~~
for item in lista1: 
  print (item)
~~~ 

### 5.2 Tamanhho

~~~
tamanho = len(lista1)
print (tamanho)
~~~ 

### 5.3 Inserindo novos itens

~~~
lista1.append("uva")
print (lista1)
~~~

### 5.4 Verificação de item na lista

~~~
if **3** in lista2: 
  print ("7 está na lista 2")
~~~ 

### 5.5 Deletar um item ou mais da lista

Deleta da posição 2 em diante: 

~~~
del lista1[2:] 
print (lista1)
~~~ 

### 5.6 Ordenar lista 

#### 5.6.1 Sort - Altera a lista

Ordenação direta: 

~~~
lista1.sort()
~~~ 

Ordenação reversa (decrescente): 

~~~
lista1.sort(reverse=True) # Opção 1
lista2.reverse() # Opção 2
~~~ 

#### 5.6.2 Sorted 

~~~
listaOrdenada = sorted(lista)
print (listaOrdenada)
print (lista)
~~~ 

### 5.7 List comprehension

Exemplo: 

x = [1,2,3,4,5] 
y = [valor_a_inserir laço condição] 

~~~
x = [1,2,3,4,5] 
y = [i**2 for i in x] 
x = [i for i in x if i%2==1] 
~~~

### 5.8 List Enumerate 

Enumera posição e item na lista, na determinada posição. 

~~~
lista = ["abacate", "bola", "cachorro"] 

for i,nome in enumerate(lista): 
  print(i,nome) 
~~~   

### 5.9 List Filter

Executa uma função com base nos valores de uma lista. 

~~~
def pares(i): 
  if i % 2 == 0: 
    return i
    
lista = [1,2,3...,10] 

lista_pares = filter(pares,lista)

print (list(lista_pares))
~~~ 

### 5.10 List Map

Cria uma lista com os valores da lista anterior aplicados a uma função. 
map(funcao, valor) 

~~~ 
def dobro(x): 
  return x*2
  
valor = [1,2,3,4,5]

doubleValues = list(map(dobro,valor))

print(doubleValues)
~~~ 

### 5.11 List Reduce

Sua utilidade está na aplicação de uma função a todos os valores do conjunto, de forma a agregá-los todos em um único valor. Por exemplo, para aplicar a operação de soma a todos os elementos de uma sequência. 

~~~
>>> import operator #necessário para obter a função de soma
>>> valores = [1, 2, 3, 4, 5]
>>> soma = reduce(operator.add, valores)
>>> print soma
15
~~~ 

### 5.12 List Zip

Concatena os valores entre duas listas

~~~
lista1 = [1,2,3,4,5] 
lista2 = ["Abacate", "Beringela", "Carambola", "DoceDeLeite", "Especial"] 
lista3 = ["R$ 1,00", "R$ 3,00", "R$ 5,00", "R$ 8,00", "R$ 10,00"]

for numero, fruta, valor in zip(lista1, lista2, lista3): 
  print (numero, fruta, valor) 
~~~

Output: 

~~~
1 Abacate R$ 1,00
2 Beringela R$ 3,00
3 Carambola R$ 5,00
4 DoceDeLeite R$ 8,00
5 Especial R$ 10,00
~~~

## 6. Estruturas condicionais

### 6.1 If

O if segue o padrão da indentação. 

~~~
if (condição): 
  ##código
~~~

### 6.2 Else e Elif

Similar ao java, o Elif é como se fosse um **if else**

~~~
if (condição1): 
  ##código
elif (condição2): 
  ##código
else: 
  ##código
~~~

## 7. Estruturas de repetição

### 7.1 While

~~~
while x < 10: 
  print (x)
  x+=1
~~~ 

### 7.2 For 

### 7.2.1 For Each

~~~ 
lista = [1,2,3,4,5] 
lista2 = ["abc, "def"]
lista 3 = [0, "Olá", true, 9.9]
~~~ 

~~~ 
for i in lista2: 
  print (i)
~~~

### 7.2.2 For range

~~~ 
>>> for i in range(10): 
  >>> print (i)
  
  #output de 1 a 9 - começa no zero. 
~~~

~~~ 
>>> for i in range(10,20): 
  >>> print (i)
  
  #output de 1 a 19
~~~

~~~ 
>>> for i in range(10,20, 2): 
  >>> print (i)
  
  #output de 10 a 18 - passo 2, 20 excludente. 
~~~

## 8. Input de dados

~~~
>>> numero = input("Digite um numero: ")
  >>> print (numero)
  
#numero digitado
~~~

Dados concatenados: 

~~~
>>> numero = input("Digite um numero: ")
  >>> print ("Este foi o valor digitado: " + numero)
  
Este foi o valor digitado: #numero digitado
~~~

Para operações numéricas, o valor recebido por input é considerado string. Precisa-se fazer o casting: 

~~~
vote = int(input('Enter the number of the player you wish to vote for'))
    if (0 < vote <=24):
        players[vote +1] += 1;cont +=1
    else:
        print('Invalid vote, try again')
~~~

## 9. Strings

### 9.1 Tamanho de uma string (len)

~~~
>>> a = "Luis Felipe"
>>> print (len(a)) 

11
~~~

### 9.2 Valor em uma determinada posição

~~~
>>> a = "Luis Felipe"
>>> letraU = a[1]
>>> print (letraU) 

u
~~~

A seguir, o código indica que ele vai ler o código a partir de 0 até **4 letras**. 

~~~
>>> a = "Luis Felipe"
>>> luis = a[0:4]
>>> print (luis) 

Luis
~~~

### 9.3 Lower/Upper

~~~
>>> A = "AAAAAAAAAAAAAAAA"
>>> b = "bbbbbbbbbbbbbbbb"

>>> a = A.lower()
>>> print (a) 


>>> B = b.upper()
>>> print (B)

aaaaaaaaaaaaaaaa
BBBBBBBBBBBBBBBB
~~~

### 9.4 Remoção de espaços vazios (strip)

~~~
>>> A = "  AAAAAAAAAAAAAAAA  "
>>> strippedA = A.strip()
>>> print (strippedA)

AAAAAAAAAAAAAAAA
~~~

### 9.5 Converter String em lista

A string será quebrada com o termo informado. 
**Case sensitive**

~~~
>>> seq = "ABCD EFGH"
>>> lista = seq.split(" ") #tambem poderia ser apenas .split()
>>> print (lista)

["ABCD","EFGH"] 
~~~

~~~
>>> seq = "ABCD BCDE CDEF DEFG"
>>> lista = seq.split(" ")
>>> print (lista)

['A', 'CD ', 'CDE CDEF DEFG']
~~~

### 9.6 Find 

Retorna a primeira aparição deste termo. 

~~~
>>> seq = "ABCD EFGH EF"
>>> busca = seq.find("EF") 
>>> print (busca)

5
~~~

Exemplo de uso: Imprimir uma lista a partir de determinada posição

~~~
>>> seq = "ABCD EFGH EF"
>>> busca = seq.find("EF") 
>>> print (seq[busca:])

EFGH EF
~~~

Se o `find` não encontrar o termo, retorna -1.

### 9.7 Replace

~~~
>>> seq = "ABCD EFGH IJKL"
>>> replacer = seq.replace("EFGH","Bazinga") 
>>> print (replacer)

ABCD Bazinga IJKL
~~~

## 10. Criando uma função

Para que as funções executem, elas devem ser declaradas na linha superior à sua chamada 

Para chamar uma função, use o nome da função seguido por parênteses:

~~~
def my_function(fname):
  print(fname + " Refsnes")

my_function("Emil")
my_function("Tobias")
my_function("Linus")
~~~

Output: 
~~~
Emil Refsnes
Tobias Refsnes
Linus Refsnes
~~~

## 11. Arquivos

### 11.1 Readlines

Esta função armazena em uma lista todas as linhas do meu arquivo. 

~~~
arquivivo = open("arquivo.txt")
linhas = arquivo.readlines()
~~~ 

### 11.2 Read

Esta função armazena em uma única variável o texto completo. 

~~~
arquivivo = open("arquivo.txt")
variavel = arquivo.read()
~~~ 

### 11.3 Write

Modo | Função
:-----:|:--------
r|somente leitura
w|escrita (sobrescreve)
a|leitura e escrita (adiciona ao fim)
r+|leitura e escrita
w+|escrita (apaga o conteúdo anterior)
a+|leitura e escrita (abre o arquivo para atualização)

Opção 1: apagando o arquivo: 

~~~
w = open("arquivo.txt", "w")
w.write("Esse é o arquivo")
w.close()
~~~ 

Opção 2: Adiciona ao fim 

~~~
a = open("arquivo.txt", "a")
a.write("Esse é o arquivo")
a.close()
~~~ 

## 12: Dicionários (Chave, valor)
 
Em Python, dicionários são arrays associativos, ou seja, um determinado valor passa a ser vinculado a uma **chave**. 

Exemplo:
`
dicionario = {"Luis": "atalhox.com"}
`

### 12.1 No dicionário acima, a chave "Luis" foi vinculado ao valor "atalhox.com". Assim, para imprimir o valor chame:

~~~
>>> print(dicionario['Luis'])

atalhox.com
~~~

### 12.2 Para imprimir apenas valores:

~~~
dicionario = {"Luis": "atalhox.com", "Google": "google.com", "Udemy": "udemy.com"}
  
for value in dicionario:
    print(dicionario[value])
~~~

Ou ainda: 

~~~
dicionario = {"Luis": "atalhox.com", "Google": "google.com", "Udemy": "udemy.com"}
  
for i in dicionario.values()
    print(i)
~~~

### 12.3 Para imprimir as chaves: 

~~~ 
dicionario = {"Luis": "atalhox.com", "Google": "google.com", "Udemy": "udemy.com"}

for key in dicionario:
    print(key)
~~~ 

Ou ainda: 

~~~
dicionario = {"Luis": "atalhox.com", "Google": "google.com", "Udemy": "udemy.com"}
  
for i in dicionario.keys()
    print(i)
~~~

### 12.4 Para imprimir os pares de chave e valor: 

~~~
dicionario = {"Luis": "atalhox.com", "Google": "google.com", "Udemy": "udemy.com"}
  
for i in dicionario.items()
    print(i)
~~~

## 13. Importando uma lib 

`from myapp import app as application` 

Ela está dizendo "do arquivo **myapp.py** importe a variável **app** com o apelido **application**".

Myapp:
~~~
def greeting(name):
  print("Hello, " + name)

person1 = {
  "name": "John",
  "age": 36,
  "country": "Norway"
}
~~~

Importe apenas o dicionário person1 do módulo:

~~~
from myapp import person1

print (person1["age"])
~~~

Ou importe o módulo chamado myapp e acesse o dicionário person1:
~~~
import myapp

a = myapp.person1["age"]
print(a)
~~~

### 13.1 Import math

#### 13.1.1 Sqrt

~~~
# import the math module  
import math  
  
# print the square root of  0  
print(math.sqrt(0)) 
~~~

### 13.2 Import random

#### 13.2.1 RandInt
~~~
import random

numero = random.randint(0,10)
print(numero)
~~~ 

#### 13.2.2 Choice

Escolhe aleatoriamente com base numa lista pré-determinada! 

~~~
import random

lista = [6,45,9]
numero = random.choice(lista)
print(numero)
~~~ 

### 13.3. Import json

Biblioteca para a manipulação de json. 

#### 13.3.1 json.load

json.load pode desserializar um arquivo em si, ou seja, aceita um objeto file:

~~~
with open("json_data.json", "r") as content:
  print(json.load(content))
~~~

Resulta: 

`{u'event': {u'id': u'5206c7e2-da67-42da-9341-6ea403c632c7', u'name': u'Sufiyan Ghori'}}`

#### 13.3.2 json.loads

~~~
with open("json_data.json", "r") as content:
  print(json.loads(content.read()))
~~~

Resulta: 

`{u'event': {u'id': u'5206c7e2-da67-42da-9341-6ea403c632c7', u'name': u'Sufiyan Ghori'}}`

content.read() ocorre porque o tipo é uma string, ou seja,<type 'str'>. Se eu usar json.load() com content.read() resulta em erro. 

Então, agora você sabe que json.load desserializa um arquivo e json.loads desserializa uma string.

## 14. Tratamento de exceções

~~~ 
a = 2
b = 0

try: 
  print(a/b)
except: 
  print ("Não é permitida divisão por 0")
~~~

## 15. Comando With

Ele é usado para garantir finalização de recursos adquiridos.

Exemplo: Um arquivo é aberto. Quem garante que ele será fechado? 

Mesmo que você coloque no código de forma explícita que ele deve ser fechado, se ocorrer uma exceção, o código sai de escopo sem executar o resto do código que está em escopo, ele pula o fechamento.

Para evitar isto usamos um **try finally**. O finally garante a finalização. Como o código fica um pouco longo e este caso é bastante frequente, a linguagem providenciou uma forma simplificada com o **with**.

Ele consegue manipular objetos que contenham os métodos __enter__() e __exit__(). Eles são chamados internamente logo no início da execução do bloco criado e dentro do finally interno criado no bloco.

Sem with: 
~~~
try:
   f = open("data.txt", "w")
   # codigo usando o arquivo f
finally:
   f.close()
~~~

Com with: 
~~~
with open("data.txt", "w") as f:
   # codigo usando o arquivo f
~~~

