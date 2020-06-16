# Log4J

Situações comum que precisamos de um LOG:

1.  Sua aplicação conecta à banco de dados e este está down, com certeza verá communication link failure como exceção e uma connection refused. Para que tudo isso não apareça na tela do usuário, mandamos para um arquivo de log e lá vamos investigar quando e que dia aquilo aconteceu;

2.  Sua aplicação vai ler um arquivo que é criado a partir de outra aplicação, se não encontrar o tal do arquivo teremos uma exceção e mandaremos ela para o arquivo de log. E daí vamos saber o dia, o horário que a outra aplicação parou de gerar aquele tal arquivo e daí iniciar uma investigação;

## Entendendo o Logger 

Para entender o framework, é preciso saber apenas três aspectos: Logger, Appender,Layout.

* **Logger**: é o cara que recebe as solicitações de log. Podemos criar um logger para cada classe da aplicação, porém o framework já fornece uma padrão caso não seja informado nenhum.

* **Appender**: os Loggers eles precisam saber para quem enviar as informações que recebeu, e ai os Appenders fazem o trabalho dele, dizendo : “Logger, passe as informações que você recebeu para mim, que eu saberei o que fazer com elas”.
Com o appender podemos decidir, salvar as informações de Logger em um arquivo, imprimir no console, enviar via e-mail etc.

* **Layout**: precisamos definir o formato que estas informações serão armazenadas para isso precisamos de layout. Podemos, organizar em um formato HTML, Simple text etc. Com o layout podemos definir data e hora, linha onde o log foi gerado etc.

## 1 - Maven e dependências

Crie um projeto com o Maven Archetype-generate.

	<dependency>
		<groupId>org.apache.logging.log4j</groupId>
		<artifactId>log4j-api</artifactId>
		<version>2.11.2</version>
	</dependency>
		
	<dependency>
		<groupId>org.apache.logging.log4j</groupId>
		<artifactId>log4j-core</artifactId>
		<version>2.11.2</version>
	</dependency>
	
## 2 - Crie o arquivo properties

O arquivo **properties** fica na pasta:

> src/main/resources

## 3 - Appenders

Crie um arquivo log4j2.xml na pasta resources e o configure com um dos seguintes appenders.

### 3.1 - Console Appender

~~~
<?xml version="1.0" encoding="UTF-8"?>
<Configuration status="DEBUG">
    <Appenders>
        <Console name="LogToConsole" target="SYSTEM_OUT">
            <PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"/>
        </Console>
    </Appenders>
    <Loggers>
		<!-- avoid duplicated logs with additivity=false -->
        <Logger name="com.atalhox" level="debug" additivity="false">
            <AppenderRef ref="LogToConsole"/>
        </Logger>
        <Root level="error">
            <AppenderRef ref="LogToConsole"/>
        </Root>
    </Loggers>
</Configuration>
~~~

### 3.2 - File Appender

~~~
<?xml version="1.0" encoding="UTF-8"?>
<Configuration status="DEBUG">
    <Appenders>
        <Console name="LogToConsole" target="SYSTEM_OUT">
            <PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"/>
        </Console>
        <File name="LogToFile" fileName="logs/app.log">
            <PatternLayout>
                <Pattern>%d %p %c{1.} [%t] %m%n</Pattern>
            </PatternLayout>
        </File>
    </Appenders>
    <Loggers>
        <Logger name="com.mkyong" level="debug" additivity="false">
            <AppenderRef ref="LogToFile"/>
            <AppenderRef ref="LogToConsole"/>
        </Logger>
        <Logger name="org.springframework.boot" level="error" additivity="false">
            <AppenderRef ref="LogToConsole"/>
        </Logger>
        <Root level="error">
            <AppenderRef ref="LogToFile"/>
            <AppenderRef ref="LogToConsole"/>
        </Root>
    </Loggers>
</Configuration>
~~~

### 3.3 - RollingFileAppender – Gire os arquivos de log diariamente ou quando o tamanho do arquivo for >10 MB.

~~~
<Configuration status="DEBUG">
    <Appenders>
        <Console name="LogToConsole" target="SYSTEM_OUT">
            <PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"/>
        </Console>
        <RollingFile name="LogToRollingFile" fileName="logs/app.log"
                    filePattern="logs/$${date:yyyy-MM}/app-%d{MM-dd-yyyy}-%i.log.gz">
			<PatternLayout>
				<Pattern>%d %p %c{1.} [%t] %m%n</Pattern>
			</PatternLayout>
			<Policies>
				<TimeBasedTriggeringPolicy />
				<SizeBasedTriggeringPolicy size="10 MB"/>
			</Policies>
		</RollingFile>
    </Appenders>
	
    <Loggers>
        <!-- avoid duplicated logs with additivity=false -->
        <Logger name="com.mkyong" level="debug" additivity="false">
            <AppenderRef ref="LogToRollingFile"/>
        </Logger>
        <Root level="error">
            <AppenderRef ref="LogToConsole"/>
        </Root>
    </Loggers>
</Configuration>
~~~

### 3.4 - AsyncAppender – Tornar appender assíncrono. Aumenta o desempenho.

~~~
<Configuration status="DEBUG">
    <Appenders>
        <Console name="LogToConsole" target="SYSTEM_OUT">
            <PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"/>
        </Console>

        <RollingRandomAccessFile name="LogToRollingRandomAccessFile" fileName="logs/app.log"
               filePattern="logs/$${date:yyyy-MM}/app-%d{MM-dd-yyyy}-%i.log.gz">
            <PatternLayout>
                <Pattern>%d %p %c{1.} [%t] %m%n</Pattern>
            </PatternLayout>
            <Policies>
                <TimeBasedTriggeringPolicy/>
                <SizeBasedTriggeringPolicy size="1 MB"/>
            </Policies>
            <DefaultRolloverStrategy max="10"/>
        </RollingRandomAccessFile>

        <Async name="Async">
			<!-- reference to other appenders -->
            <AppenderRef ref="LogToRollingRandomAccessFile"/>
        </Async>

    </Appenders>
    <Loggers>
        <!-- avoid duplicated logs with additivity=false -->
        <Logger name="com.mkyong" level="debug" additivity="false">
            <AppenderRef ref="Async"/>
        </Logger>
        <Root level="error">
            <AppenderRef ref="LogToConsole"/>
        </Root>
    </Loggers>
</Configuration>
~~~

## 4 - Crie o Log

Para registrar uma mensagem, crie um **final static logger** e defina um nome para o logger. Normalmente, usamos o nome completo da classe do pacote.

`final static Logger logger = Logger.getLogger(classname.class);`

Em seguida, registre mensagens com prioridades diferentes, por exemplo, depuração, informações, aviso, erro e fatal. 

## 5 - Configurando mensagens de erro

Os níveis vão ajudar para saber que tipo de informação deseja gravar no seu LOG, por exemplo: 

> Você define que apenas os erros igual ou maior que WARN serão salvo no seu arquivo LOG. Isso é importante, pois às vezes não importa ter DEBUG,INFO em seu arquivo de LOG quando está em produção. 

Você pode criar, por exemplo, dois arquivos de LOG:

* um para DEV e lá você põe todas as info desde DEBUG 

* um para o log que vai junto com aplicação a partir de INFO.

A ordem hierarquica é: DEBUG < INFO < WARN < ERROR < FATAL.

Leitura simples: se você configura para WARN, somente será enviado mensagem **igual ou acima** de WARN. Quem é maior que WARN? (ERROR).

``` 
//logs a debug message
if(logger.isDebugEnabled()){
	logger.debug("This is debug");
}

//logs an error message with parameter
logger.error("This is error : " + parameter);

//logs an exception thrown from somewhere
logger.error("This is error", exception);
``` 

