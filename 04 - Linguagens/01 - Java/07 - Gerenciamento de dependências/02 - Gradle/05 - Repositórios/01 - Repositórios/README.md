# Repositórios

São repositórios para buscar dependências. 

Os três principais são: 

~~~
repositories {
    mavenCentral()
    jcenter()
    google()
}
~~~

Para declarar repositórios em links personalizados: 

~~~
repositories {
    jcenter()
    maven {
        url "https://maven.springframework.org/release"
    }
    maven {
        url "https://maven.restlet.com"
    }
}
~~~

