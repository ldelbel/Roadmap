Atualmente o padrão de projeto mais popular adotado pelos frameworks de desenvolvimento de aplicações web, 
trata-se de uma estratégia que nos permite isolar completamente as camadas de negócio (M/V) através da inclusão de uma intermediária (C):

* M - Modelo;
* V - Visualização;
* C - Controlador. 

A compreensão deste padrão se tornará mais clara conforme descrevemos estas camadas.

O modelo diz respeito à toda a parte do sistema responsável pela lógica de negócio e seus componentes auxiliares, como persistência, cacheamento, integração com
outros sistemas etc.

A visualização , como o próprio nome já nos diz, é a parte visível ao usuário final. Quando nos deparamos com uma janela ou página HTML, estamos lidando 
diretamente com o resultado desta camada.

Finalmente, temos a camada menos óbvia que é o controlador , que orquestra a interação entre as duas camadas 
acima citadas. Quando o usuário clica em um link, o controlador é acionado. 

Este transforma os parâmetros de entrada para um formato que seja compatível com a interface disponibilizada pela camada de negócio,
cujo resultado do processamento é recebido pelo controlador, que o modifica caso necessário e em seguida o envia à camada de visualização para que seja contemplado pelo usuário final.

![AlgaWorks](https://s3.amazonaws.com/algaworks-blog/wp-content/uploads/Fluxo-do-Spring-MVC.png)

1. Acessamos uma URL no browser que envia a requisição HTTP para o servidor que roda a aplicação web com Spring MVC. Perceba que quem recebe a requisição é o controlador do framework, o Spring MVC.

2. O controlador do framework irá procurar qual classe é responsável por tratar essa requisição, entregando a ela os dados enviados pelo browser. Essa classe faz o papel do controller.

3. O controller passa os dados para o model, que por sua vez executa todas as regras de negócio, como cálculos, validações e acesso ao banco de dados.

4. O resultado das operações realizadas pelo model é retornado ao controller.

5. O controller retorna o nome da view, junto com os dados que ela precisa para renderizar a página.

6. O Framework encontra a view que processa os dados, transformando o resultado em um HTML.

7. Finalmente, o HTML é retornado ao browser do usuário.
