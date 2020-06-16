# Arquivos

* gradle: diretório que contém os arquivos do Gradle wrapper.
* gradlew: Gradle wrapper para sistemas baseados em Unix (Linux).
* gradlew.bat: Gradle wrapper para Windows.
* settings.gradle: configurações do projetos. 

## 1. Arquivo Build.gradle

Este arquivo é o equivalente à `POM.xml` do `Maven`. 

~~~ 
build.gradle

plugins {
    id 'java'
    id 'application'
}

java {
    sourceCompatibility = JavaVersion.VERSION_1_8
    targetCompatibility = JavaVersion.VERSION_1_8
}

version = '1.2.1'

repositories {
    jcenter() 
}

dependencies {
    implementation 'com.google.guava:guava:26.0-jre' 
    testImplementation 'junit:junit:4.12' 
}

mainClassName = 'demo.App' 
~~~ 

