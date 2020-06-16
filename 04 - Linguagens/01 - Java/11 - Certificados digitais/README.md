# InstallCert Configuration

### Baixar o certificado X509 pelo navegador

Preferencialmente, fazer o download do certificado pelo formato base64. 

### Access server, and retrieve certificate (accept default certificate 1)

`java InstallCert [HOST]:[port]`

* HOST sem o schema (http ou https)

Portas: 

* 80 : se http.
* 443: se https.

### Extract certificate from created jssecacerts keystore

`keytool -exportcert -alias [HOST]-1 -keystore jssecacerts -storepass changeit -file [HOST]-1.cer`

### Import certificate into system keystore

`keytool -importcert -alias [HOST]-1 -keystore "/c/Program Files/Java/jdk-9/lib/security/cacerts" -storepass changeit -file [HOST]-1.cer`

Pode ocorrer uma falha por causa da linguagem. Force a linguagem em inglês: 

`keytool -J-Duser.language=en -importcert -alias [HOST]-1 -keystore "/c/Program Files/Java/jdk-9/lib/security/cacerts" -storepass changeit -file [HOST]-1.cer`

### Delete Alias

`keytool -delete -noprompt -alias [HOST]-1  -keystore "/c/Program Files/Java/jdk-8/lib/security/cacerts" -storepass changeit`

