# 1. Tokens

## Token de acesso do usuário  

Esse tipo de token de acesso é necessário sempre que o aplicativo chama uma API para ler, modificar ou gravar dados do Facebook de uma pessoa específica em seu nome.  

Os tokens de acesso do usuário geralmente são obtidos por meio de uma caixa de diálogo de login e exigem que uma pessoa permita que seu aplicativo obtenha uma. 

## Token de Acesso ao Aplicativo 

Esse tipo de token de acesso é necessário para modificar e ler as configurações do aplicativo.  

Ele é gerado usando um segredo pré-acordado entre o aplicativo e o API e é usado durante as chamadas que alteram as configurações de todo o aplicativo.  

Você obtém um token de acesso ao aplicativo por meio de uma chamada de servidor para servidor, em nome de um aplicativo e não um usuário.  

## Token de acesso à página 

Esse tipo de token de acesso é semelhante aos tokens de acesso do usuário, exceto que eles fornecem permissão para APIs que lêem, gravam ou modificam os dados pertencentes a uma Página do Facebook.  

Para obter um token de acesso à página, você precisa começar obtendo um token de acesso do usuário e solicitando a permissão para gerenciar a página.  

Depois de ter o token de acesso do usuário, você obtém o token de acesso à página por meio da API do Graph. 

## Token de cliente 

O client token é um identificador que você pode incorporar em binários móveis nativos ou aplicativos de desktop para identificar seu aplicativo.  

O token do cliente não deve ser um identificador secreto porque está incorporado nos aplicativos.  

Também é usado para acessar APIs no nível do aplicativo, mas apenas um subconjunto muito limitado.  

Este token é encontrado no painel do seu aplicativo.  

Como o token do cliente é usado raramente, não falaremos sobre isso neste documento.  
