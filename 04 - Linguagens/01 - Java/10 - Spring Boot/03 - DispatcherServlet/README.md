# Servlets

Um `servlet` é uma classe Java usada para estender os recursos de servidores que hospedam aplicativos acessados por meio de um modelo de programação de solicitação-resposta. 

Embora os servlets possam responder a qualquer tipo de solicitação, eles geralmente são usados para estender os aplicativos hospedados pelos servidores da web. Para esses aplicativos, a tecnologia Java Servlet define classes de servlet específicas do HTTP.

Os pacotes `javax.servlet` e `javax.servlet.http` oferecem interfaces e classes para escrever servlets. 

Ao receber uma requisição, um Servlet pode capturar os parâmetros desta requisição, efetuar qualquer processamento inerente a uma classe Java, e devolver uma página HTML.

São basicamente módulos de software que são executados em um servidor web para atender as requisições de aplicações cliente e prestar-lhes algum tipo de serviço.

Ou seja, quando você recebe sua requisição na `view`, você precisa receber essa requisição, processar de alguma forma e enviar uma resposta. 

> View é a apresentação de dados, é a saída, é como o usuário irá ver o que foi produzido por uma ação da aplicação, e é a forma como uma entrada de dados ocorrerá e iniciará uma ação por parte do usuário.

Resumindo: o objetivo é receber chamadas HTTP, processá-las e devolver uma resposta ao cliente.

## 1. DispatcherServlets

DispatcherServlet atua como controlador frontal para aplicativos da Web baseados em Spring. Ele fornece um mecanismo para o processamento de solicitações, onde o trabalho real é executado por componentes delegados configuráveis. É herdado do javax.servlet.http.HttpServlet e normalmente é configurado no arquivo web.xml.

Um aplicativo da web pode definir qualquer número de instâncias do **DispatcherServlet**. 

Cada servlet operará em seu próprio **namespace**, carregando seu próprio application context com mappings, handlers etc. 

Somente o contexto do aplicativo raiz carregado por **ContextLoaderListener**, se houver, será compartilhado. 

Na maioria dos casos, os aplicativos possuem apenas uma `DispatcherServlet` com a URL raiz (/), ou seja, todas as 
solicitações que chegam a esse domínio serão tratadas por ela.

A `DispatcherServlet` **usa classes de configuração do Spring** para descobrir os componentes delegados necessários para o mapeamento de requisições, view resolutions, tratamento de exceções etc.

**Fluxo: 

1. Tudo começa no momento em que uma requisição chega ao Dispatcher Servlet. 

2. A requisição terá sua assinatura analisada e enviada ao Mapeador de requisições (Handler Mapping), que é o componente responsável por descobrir qual controlador deve ser acionado.

3. Uma vez obtido o controlador alvo, este é executado e um nome lógico do template de visualização a ser renderizado como resposta ao usuário (view) é retornado ao Dispatcher Servlet e o conjunto de variáveis (model) que serão expostas nesta renderização.

4. Com o nome lógico da visualização e o modelo obtidos, entra em cena o Gerenciador de visualização (View Resolver), que possui a função de, com base no nome da view, retornar ao Servlet Dispatcher qual elemento de visualização - mais comumente uma página JSP - deverá ser renderizada de volta ao usuário que fez a requisição.

## 2. Application Context

Em resumo, é um **objeto** que carrega a configuração (geralmente baseada em anotação de arquivo XML). Vantagens para o Spring: 

* Beans declarados no package;
* Beans declarados via anotações;
* Autowiring de construtores e métodos
* Injestão de beans;
* Carregamento de arquivos de configurações, .properties and .yaml 
* etc.

No caso de aplicativos Java-web usando o Spring MVC, o DispatchServlet carregará o application context, portanto, você só precisará criar um arquivo springapp-servlet.xml na pasta WEB-INF do aplicativo.

[Properties Spring](https://docs.spring.io/spring-boot/docs/current/reference/html/appendix-application-properties.html)

## 3. DispatcherServlet XML

No código abaixo, o dispatcher-servlet-context.xml conterá todas as definições e associações de **beans** que estarão disponíveis para DispatcherServlet. Essas definições de bean substituirão as definições de quaisquer beans definidos com o mesmo nome no escopo global. 

Web.xml: 
~~~
<web-app>
 
  <listener>
    <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
  </listener>
 
  <context-param>
    <param-name>contextConfigLocation</param-name>
    <param-value>/WEB-INF/dispatcher-servlet-context.xml</param-value>
  </context-param>
 
  <servlet>
    <servlet-name>dispatcher-servlet</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <init-param>
      <param-name>contextConfigLocation</param-name>
      <param-value></param-value>
    </init-param>
    <load-on-startup>1</load-on-startup>
  </servlet>
 
  <servlet-mapping>
    <servlet-name>dispatcher-servlet</servlet-name>
    <url-pattern>/*</url-pattern>
  </servlet-mapping>
 
</web-app>
~~~ 

## 4. Configuração Java do DispatcherServlet

A partir do Servlet 3.0, além da configuração declarativa no web.xml, o DispatcherServlet pode ser configurado programaticamente, implementando ou estendendo uma dessas três classes de suporte fornecidas pelo Spring: 

* WebAppInitializer
* AbstractDispatcherServletInitializer
* AbstractAnnotationConfigDispatcherServletInitializer

## 5. Beans

Ao receber uma solicitação da Web, DispatcherServlet executa um conjunto de operações para o processamento da solicitação. 

| BEAN | RESPONSABILIDADE |
|--|--|
|`HandlerMapping`  | Mapeia solicitações da Web recebidas para handlers - pré/pós-processadores  |
|`HandlerAdapter`  |  Invoca o manipulador que resolve argumentos e dependências, como anotações para endpoints do mapped controller da URL|
|`HandlerExceptionResolver`  | Permite o tratamento programático de exceções e mapeia exceções para views 
|`ViewResolver`  | Resolve nomes de views para instâncias de view. |
|`LocaleResolver`  | Resolve a localidade do cliente para permitir a internacionalização |
|`LocaleContextResolver`  | Uma extensão mais rica de `LocaleResolver`, com informações de fuso horário |
|`ThemeResolver` | Resolve temas configurados no seu aplicativo para melhorar a experiência do usuário |
|`MultipartResolver` | Manipula uploads de arquivos com várias partes como parte de solicitações HTTP |
|`FlashMapManager`  |  Gerencia instâncias do FlashMap que armazenam atributos temporários do Flash entre solicitações redirecionadas uma da outra|
