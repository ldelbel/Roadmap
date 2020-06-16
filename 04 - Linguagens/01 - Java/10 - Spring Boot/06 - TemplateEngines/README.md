# Template Engines

## 1. Sites estáticos e dinâmicos

### 1.1. Site estático

Um site estático é uma página da web que é entregue ao visitante exatamente da mesma forma que ela foi armazenada no servidor. Em outras palavras, em um site estático o conteúdo das páginas é o mesmo para todos os usuários que as visitam.

Estes sites são arquivos HTML armazenados em um computador e disponibilizados por meio de um servidor web. Assim, no caso de um site estático, você pode baixar os arquivos do site e simplesmente abri-los diretamente do seu navegador no seu computador.

São adequados para conteúdos que não precisam ser atualizados com frequência ou quase nunca mudam. 

Num site estático não há um sistema de banco de dados ou uma linguagem de programação no lado do servidor (tudo é feito no navegador), utilizando as tecnologias de front-end. 

O visitante utiliza as informações exibidas no site estático para suas ações, como fazer uma ligação ou enviar um e-mail.

Embora um site estático possa ser limitado nas suas funcionalidades, esse tipo de site ainda é bastante flexível no visual e aparência das páginas. Usando HTML e CSS é possível personalizar o estilo da página livremente, e com JavaScript é possível tornar o site ainda mais interativo.

**Vantagens do site estático**

* Mais barato para hospedar pois exige menos do servidor;
* Maior segurança, pois não está sujeito à vulnerabilidades em códigos ou bibliotecas;
* Não depende de banco de dados ou linguagem de programação para funcionar;
* Melhor desempenho, pois depende menos das requisições do servidor.

**Desvantagens do site estático**

* Menos intuitivo para gerenciar o conteúdo, exige a edição manual dos arquivos do site;
* Funcionalidade dinâmica é limitada, sendo necessário adicionar separadamente;
* Não possui banco de dados, o que dificulta o processamento de dados.

### 1.2. Site dinâmico

Um site dinâmico é uma página da web que é controlada por um servidor de aplicação com tecnologias que rodam ao lado do servidor. Por exemplo, um site que é gerado a partir de scripts PHP e **utiliza banco de dados para exibir informações** nas páginas é um site dinâmico.

Normalmente, os sites dinâmicos: 

* recebem uma entrada de dados dos visitantes;  
* processam esses dados no servidor; 
* devolvem como informação para o visitante. 

No entanto, sites que **modificam a página com tecnologias do próprio navegador**, como JavaScript, também podem ser um considerados sites dinâmicos.

Os sites dinâmicos são ideais para aplicações web e sistemas mais complexos, que mudam com frequência, exigem o processamento de dados do lado do servidor ou uma grande interatividade com o visitante, como e-commerce, portais de notícias, redes sociais, fóruns e até mesmo blogs.

**Vantagens do site dinâmico**

* Todas as informações inseridas ou parte delas são carregadas automaticamente, por meio de um tratamento no servidor de hospedagem.
* Permite a criação de lojas virtuais e aplicações complexas;
* Melhor para gerenciar blogs e sites de notícias;
* Permite controle total das funcionalidades e personalização.

**Desvantagens do site dinâmico**

* A hospedagem pode ser mais cara;
* Apresenta risco de lentidão (excesso de funcionalidades ou se não for bem desenvolvido);
* Leva mais tempo para desenvolver.

## 2. ViewResolver

O retorno de um método anotado com @RequestMapping deverá ser tratado por algum ViewResolver.

> View é a apresentação de dados, é a saída, é como o usuário irá ver o que foi produzido por uma ação da aplicação, e é a forma como uma entrada de dados ocorrerá e iniciará uma ação por parte do usuário.

### 2.1. Definição

O controlador Spring MVC retorna uma instância de `ModelAndView`. As `views` no Spring são endereçadas por um `view name` e são resolvidas por um `ViewResolver`. 

O `ViewResolver` é uma interface na estrutura do Spring, usada para **definir a extensão e o local das visualizações**. 
 
Esta interface será implementada por objetos que podem resolver `views` por nome. 

Como o controlador atualizará o modelo e chamada para a respectiva `view`, esse `ViewResolver` é ajudado a obter um caminho onde as `views` estão localizadas.

~~~
<bean id="viewResolver"
      class="org.springframework.web.servlet.view.UrlBasedViewResolver">
    <property name="viewClass" value="org.springframework.web.servlet.view.JstlView"/>
    <property name="prefix" value="/WEB-INF/jsp/"/>
    <property name="suffix" value=".jsp"/>
</bean>
~~~

Ao retornar o teste como um nome de exibição, esse `ViewResolver` entregará a solicitação ao `RequestDispatcher` que enviará a solicitação para `/WEB-INF/jsp/test.jsp`.

### 2.2. Tipos


|  ViewResolver| Descrição |
|:--:|--|
| AbstractCachingViewResolver | ViewResolver abstrata que armazena views em cache. Muitas vezes, as views precisam de preparação antes de poderem ser usadas. Estender esse ViewResolver fornece armazenamento em cache. |
| XmlViewResolver | Implementação do ViewResolver que aceita um arquivo de configuração gravado em XML com o mesmo DTD das BeanFactories XML do Spring. O arquivo de configuração padrão é `/WEB-INF/views.xml`. | 
|ResourceBundleViewResolver| Implementação do ViewResolver que usa definições de bean em um `ResourceBundle`, especificadas pelo nome base do pacote configurável. Normalmente, você define o pacote configurável em um arquivo de propriedades, localizado no `classpath`. O nome do arquivo padrão é `views.properties`.
| UrlBasedViewResolver  | Implementação simples da interface `ViewResolver` que afeta a resolução direta lógica de `view names` para URLs, sem uma definição de mapeamento explícita. Isso é apropriado se seus nomes lógicos corresponderem aos nomes de seus recursos das `views` de maneira direta, sem a necessidade de mapeamentos arbitrários. |
| InternalResourceViewResolver | Subclasse conveniente de `UrlBasedViewResolver` que suporta `InternalResourceView` (Servlets e JSPs) e subclasses como JstlView e TilesView. Você pode especificar a classe de `view` para todas as visualizações geradas por esse resolvedor usando `setViewClass` (..).
|VelocityViewResolver/FreeMarkerViewResolver| Subclasse conveniente de `UrlBasedViewResolver` que suporta `VelocityView` (com efeito, modelos Velocity) ou `FreeMarkerView`, respectivamente, e subclasses personalizadas deles.
| ContentNegotiatingViewResolver  | Implementação da interface `ViewResolver` que resolve uma exibição com base no nome do arquivo de solicitação ou no cabeçalho Accept. |

## 3. Template Engines

Dado que as preocupações em um aplicativo Spring MVC são claramente separadas, a troca de uma tecnologia de visualização para outra é principalmente uma questão de configuração.

Para **renderizar cada tipo de visualização**, precisamos definir um bean `ViewResolver` correspondente a cada tecnologia. Isso significa que podemos retornar os nomes de exibição dos métodos de mapeamento `@Controller` da mesma forma que retornamos arquivos JSP.

### 3.1. Thymeleaf

O Thymeleaf é um mecanismo de modelo Java que pode processar arquivos HTML, XML, texto, JavaScript ou CSS. Diferentemente de outros mecanismos de modelo, o Thymeleaf permite usar modelos como protótipos, o que significa que eles podem ser vistos como arquivos estáticos.

Inicialmente precisamos adicionar a configuração que requer um bean `SpringTemplateEngine`, bem como um `TemplateResolver` que especifique a localização e o tipo dos arquivos de exibição.

O `SpringResourceTemplateResolver` está integrado ao mecanismo de resolução de recursos do Spring:

~~~
@Configuration
@EnableWebMvc
public class ThymeleafConfiguration {
  
    @Bean
    public SpringTemplateEngine templateEngine() {
        SpringTemplateEngine templateEngine = new SpringTemplateEngine();
        templateEngine.setTemplateResolver(thymeleafTemplateResolver());
        return templateEngine;
    }
 
    @Bean
    public SpringResourceTemplateResolver thymeleafTemplateResolver() {
        SpringResourceTemplateResolver templateResolver 
          = new SpringResourceTemplateResolver();
        templateResolver.setPrefix("/WEB-INF/views/");
        templateResolver.setSuffix(".html");
        templateResolver.setTemplateMode("HTML5");
        return templateResolver;
    }
}
~~~

Além disso, precisamos de um `ViewResolver` do tipo `ThymeleafViewResolver`:

~~~
@Bean
public ThymeleafViewResolver thymeleafViewResolver() {
    ThymeleafViewResolver viewResolver = new ThymeleafViewResolver();
    viewResolver.setTemplateEngine(templateEngine());
    return viewResolver;
}
~~~ 

Agora podemos adicionar um arquivo HTML no local `/WEB-INF/views`:

~~~
<html>
    <head>
        <meta charset="ISO-8859-1" />
        <title>User Registration</title>
    </head>
    <body>
        <form action="#" th:action="@{/register}"
          th:object="${user}" method="post">
            Email:<input type="text" th:field="*{email}" />
            Password:<input type="password" th:field="*{password}" />
            <input type="submit" value="Submit" />
        </form>
    </body>
</html>
~~~ 

O Spring Boot fornecerá a configuração automática do Thymeleaf adicionando a dependência `spring-boot-starter-thymeleaf`. 

Nenhuma configuração explícita será necessária. Por padrão, os arquivos HTML devem ser colocados no local dos `resources/templates`. 
 
Quando o Thymeleaf encontra um erro ao processar a marcação Thymeleaf, ele lança uma exceção Java. Essa exceção não contém nenhuma informação (por exemplo, número de linha e caractere) sobre o que causou o erro. 

Isso pode tornar demorado e demorado encontrar e corrigir um erro de marcação do Thymeleaf, retardando o desenvolvimento do aplicativo.

### 3.2. Java Server Pages (JSP) 

O JSP é uma das tecnologias de visualização mais populares para aplicativos Java e é suportado pelo Spring. Para renderizar arquivos JSP, um tipo comum de bean `ViewResolver` é `InternalResourceViewResolver`

~~~
@EnableWebMvc
@Configuration
public class ApplicationConfiguration implements WebMvcConfigurer {
    @Bean
    public ViewResolver jspViewResolver() {
        InternalResourceViewResolver bean = new InternalResourceViewResolver();
        bean.setPrefix("/WEB-INF/views/");
        bean.setSuffix(".jsp");
        return bean;
    }
}
~~~ 

Se estamos adicionando os arquivos a um aplicativo Spring Boot, em vez de na classe `ApplicationConfiguration`, podemos definir as seguintes propriedades em um arquivo application.properties :

~~~
spring.mvc.view.prefix: /WEB-INF/views/
spring.mvc.view.suffix: .jsp
~~~ 

Em seguida, podemos começar a criar arquivos JSP no local /WEB-INF/views :

~~~ 
<%@ taglib prefix="form" uri="http://www.springframework.org/tags/form"%>
<html>
    <head>
        <meta http-equiv="Content-Type"
          content="text/html; charset=ISO-8859-1">
        <title>User Registration</title>
    </head>
    <body>
        <form:form method="POST" modelAttribute="user">
            <form:label path="email">Email: </form:label>
            <form:input path="email" type="text"/>
            <form:label path="password">Password: </form:label>
            <form:input path="password" type="password" />
            <input type="submit" value="Submit" />
        </form:form>
    </body>
</html>
~~~

Com base nessas propriedades, o Spring Boot configurará automaticamente o `ViewResolver` necessário.

### 3.3. FreeMarker

O FreeMarker é um template engine baseado em Java criado pela Apache Software Foundation. Ele pode ser usado para gerar páginas da Web, mas também código fonte, arquivos XML, arquivos de configuração, emails e outros formatos baseados em texto.

A geração é feita com base em arquivos de modelo gravados usando o FreeMarker Template Language.

Dependências necessárias: 

* Freemarker
* Spring Context Support

~~~
<dependency>
    <groupId>org.freemarker</groupId>
    <artifactId>freemarker</artifactId>
    <version>2.3.23</version>
</dependency>

<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context-support</artifactId>
    <version>4.3.10.RELEASE</version>
</dependency>
~~~ 

A integração do FreeMarker ao Spring MVC requer a definição de um bean `FreemarkerConfigurer` que especifica o local dos templates:

~~~ 
@Configuration
@EnableWebMvc
public class FreemarkerConfiguration {
  
    @Bean
    public FreeMarkerConfigurer freemarkerConfig() { 
        FreeMarkerConfigurer freeMarkerConfigurer = new FreeMarkerConfigurer(); 
        freeMarkerConfigurer.setTemplateLoaderPath("/WEB-INF/views/");
        return freeMarkerConfigurer; 
    }
}
~~~

Em seguida, precisamos definir um bean `ViewResolver` apropriado do tipo `FreeMarkerViewResolver`:

~~~
@Bean
public FreeMarkerViewResolver freemarkerViewResolver() { 
    FreeMarkerViewResolver resolver = new FreeMarkerViewResolver(); 
    resolver.setCache(true); 
    resolver.setPrefix(""); 
    resolver.setSuffix(".ftl"); 
    return resolver; 
}
~~~

Criando um template HTML wm  `/WEB-INF/views`: 

~~~ 
<#import "/spring.ftl" as spring/>
<html>
    <head>
        <meta charset="ISO-8859-1" />
        <title>User Registration</title>
    </head>
    <body>
        <form action="register" method="post">
            <@spring.bind path="user" />
            Email: <@spring.formInput "user.email"/>
            Password: <@spring.formPasswordInput "user.password"/>
            <input type="submit" value="Submit" />
        </form>
    </body>
</html>
~~~ 

### 3.4. Groovy

As views do Spring MVC também podem ser geradas usando o **Groovy Markup Template Engine**. Esse mecanismo é baseado em uma sintaxe do construtor e pode ser usado para gerar qualquer formato de texto.

A integração do Markup Template Engine ao Spring MVC requer a definição de um bean `GroovyMarkupConfigurer` e um `ViewResolver` do tipo `GroovyMarkupViewResolver`:

~~~
@Configuration
@EnableWebMvc
public class GroovyConfiguration {
  
    @Bean
    public GroovyMarkupConfigurer groovyMarkupConfigurer() {
        GroovyMarkupConfigurer configurer = new GroovyMarkupConfigurer();
        configurer.setResourceLoaderPath("/WEB-INF/views/");
        return configurer;
    }
     
    @Bean
    public GroovyMarkupViewResolver thymeleafViewResolver() {
        GroovyMarkupViewResolver viewResolver = new GroovyMarkupViewResolver();
        viewResolver.setSuffix(".tpl");
        return viewResolver;
    }
}
~~~

Os modelos são escritos na linguagem Groovy e têm várias características: 

* são compilados no bytecode; 
* contêm suporte para fragmentos e layouts;
* fornecem suporte para internacionalização;
* a renderização é rápida.

Criando um modelo Groovy para o formulário "Registro do usuário", que inclui ligações de dados:

~~~ 
yieldUnescaped '<!DOCTYPE html>'
html(lang:'en') {
    head {
        meta('http-equiv':'"Content-Type" ' +
          'content="text/html; charset=utf-8"')      
        title('User Registration')                                                            
    }
    body {
        form (id:'userForm', action:'register', method:'post') {
            label (for:'email', 'Email')
            input (name:'email', type:'text', value:user.email?:'')
            label (for:'password', 'Password')
            input (name:'password', type:'password', value:user.password?:'')
            div (class:'form-actions') {
                input (type:'submit', value:'Submit')
            }                             
        }
    }
}
~~~ 

O local padrão para os templates é  `/resources/templates`.
