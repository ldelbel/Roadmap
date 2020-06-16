# Módulos Spring - Visão Geral

![spring overview](https://docs.spring.io/spring-framework/docs/5.0.0.M1/spring-framework-reference/html/images/spring-overview.png)

## 1.1. Core Container

### 1.1.1. Core e Bean

Os módulos `Core` e `Bean` proveem as partes fundamentais do framework, incluindo o princípio de IoC (Inversion of Control), mais conhecido como injeção de dependências.

> Inversão de controle é uma prática ou um padrão que prevê o desacoplamento ou a forma como uma classe enxerga outra, gerando menos dependências e manutenções futuras.

O módulo `Bean` provê a BeanFactory, que é um implementação sofisticada do padrão Factory. Essa implementação desacopla a configuração e a especificação das dependências a partir da lógica do software.

> Bean é uma classe onde o programador determina que o spring container vai gerenciar as instâncias dessa classe (criar, usar e destruir). O programador não precisará mais usar um `new` por exemplo.

### 1.1.2. Context

O módulo `Context` baseia-se nos módulos Core e Beans. 

É um meio para acessar qualquer objeto definido e configurado. Este módulo **estende** do Bean Factory e suporta internacionalização (i18N), EJB, JMS e Remoting básico. 

Também atua como facilitador para integração do Spring com outros frameworks.

### 1.1.3. SpEL

O módulo `SpEL` fornece uma linguagem de expressão poderosa para consultar e manipular objetos durante o tempo de execução. 

As anotações `@Value` facilitam a criação de novos objetos. 

## 1.2. Data Acess / Integration Modules

### 1.2.1. JDBC

`JDBC` (Java DataBase Connectivity) fornece uma camada de abstração, reponsável pelo envio de instruções SQL para ao banco de dados.

[JDBC - Tutorial](https://github.com/atalhox/jdbc-tutorial) - Ainda não escrito. 

### 1.2.2. ORM

`ORM` (Object-Relational Mapping) provê a integração com APIs de mapeamento de objetos-relacionais, como, JPA, JDO, Hibernate, etc..

* O principal objetivo da integração do ORM da Spring é a clara criação de camadas de aplicativos, com qualquer acesso a dados e tecnologia de transações e o livre acoplamento de objetos de aplicativos, para que sejam mais reutilizáveis. 

* Não há mais dependências de serviços de negócios no acesso a dados ou na estratégia de transações, não há mais pesquisas de recursos codificadas, não há singletons difíceis de substituir, não há mais registros de serviços personalizados.

### 1.2.3. OXM

`OXM` (Object/XML Mapping) fornece suporte via camada de abstração a implementação de Objetos mapeados via XML.

Para converter um documento XML para e de um objeto, chamado de XML Marshalling ou XML Serialization. 

### 1.2.4. JMS

`JMS`  (Java Messaging Service) dá suporte a produção e consumo de mensagem sejam elas síncrona ou assíncronas.

Java Message Service, ou JMS, é uma API da linguagem Java para middleware orientado a mensagens. Através da API JMS, duas ou mais aplicações podem se comunicar por mensagens.

### 1.2.5. Transactions

`Transactions` provê suporte a  gerenciamento de classes de transação.

* Atomicidade: A transação deve ser tratada como uma operação singular, isso significa que todos os comandos presentes neste transação podem ser concluídos com sucesso ou sem sucesso. Nada será salvo se pelo menos 1 comando de 100 der errado, todos devem executar com sucesso, sem erros.

* Consistência: Este representa a consistência de integridade da base de dados, são elas: chaves primarias únicas e etc.

* Isolação: Muitas transação podem ser executadas ao mesmo tempo, a isolação garante que cada transação é isolada da outra, prevenindo corrupção de dados.

* Durabilidade: Uma transação depois de persistida deve continuar persistida e não pode ser apagada por falhas no sistema.

## 1.3 Web Modules

### 1.3.1. Web

`Web` provê recursos de integração básico orientados para a web, como inicialização do container IoC usando listeners de Servlets e contexto para aplicação web.

### 1.3.2. Sockets

`Sockets` fornece suporte para comunicação bidirecional baseada em WebSocket entre o cliente e o servidor.
Portlet provê a implementação do MVC a ser usada em um ambiente de portlet e espelha a funcionalidade do módulo do Servlet.

### 1.3.3. Servlet

`Servlet` contém a implementação do MVC (Model-View-Controller) e do Web Services REST do Spring.

## 1.4 AOP e Instrumentation

### 1.4.1. AOP

`AOP`  fornece uma implementação de programação orientada a aspectos, permitindo separar as preocupações transversais da lógica de negócios.

### 1.4.2. Aspects

`Aspects` é um módulo separado que fornece integração com AspectJ.

### 1.4.3. Instrumentation

`Instrumentation` fornece o suporte de instrumentação de classe e implementações do classloader
 
## 1.5 Messaging

Provê o suporte para aplicações baseadas em mensagens instantâneas, e inclui um conjunto de anotações para mapear mensagens para métodos, semelhante ao modelo de programação baseado em anotações do Spring MVC.

## 1.6 Test

O módulo de teste dá suporte aos teste de unitários e de integração utilizando JUnit ou TestNG. Ele fornece carregamento consistente de Spring ApplicationContexts e armazenamento em cache desses contextos. Bem como, fornece  mock objects para facilitar e isolar os testes unitários.
