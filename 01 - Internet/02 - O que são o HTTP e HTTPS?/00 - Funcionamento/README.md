# Funcionamento

As pessoas que acessam um site enviam solicitações a servidores que as exibem na forma do site em formato de texto, imagens, e outros tipos de mídia.

Depois que a solicitação é atendida por um servidor, a conexão entre o usuário e o servidor é desconectada.

Uma nova conexão deve ser feita para cada solicitação, isto é, cada vez que alguém acessa o seu site.

1. Se a URL pertencer a um domínio próprio, o navegador primeiro se conecta a um servidor e recuperará o endereço IP correspondente ao servidor;

2. o navegador se conecta ao servidor e envia uma solicitação HTTP para a página da web desejada (que, neste exemplo, é o seu site);

3. o servidor recebe a solicitação e verifica a página desejada. Se a página existir, o servidor a mostrará. Se o servidor não conseguir encontrar a página solicitada, ele enviará uma mensagem de erro HTTP 404, ou seja, página não encontrada;
4. o navegador, então, recebe a página de volta e a conexão é fechada;

5. caso a página exista (e é isso que se espera), o navegador a analisa e procura outros elementos necessários para concluir a sua exibição, o que inclui seus textos, imagens e afins;

6. para cada um desses elementos, o navegador faz conexões adicionais e solicitações HTTP para o servidor para cada elemento;

7. quando o navegador terminar de carregar todos os elementos, a página será carregada na janela do navegador.
