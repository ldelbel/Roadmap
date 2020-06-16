# Java Task

* **sourceCompatibility**: especifica que a versão da linguagem de programação Java seja usada para compilar arquivos `.java`. 

Por exemplo, `sourceCompatibility = 1.6` especifica que a versão 1.6 da linguagem de programação Java seja usada para compilar arquivos `.java`.

Por padrão: 
* sourceCompatibility = versão da JVM atual em uso. 
* targetCompatibility = versão da sourceCompatibility. 

* **targetCompatibility**:  Esta opção garante que os arquivos de classe gerados sejam compatíveis com as VMs especificadas por targetCompatibility. Observe que, na maioria dos casos, o valor da opção -target é o valor da opção -source; nesse caso, você pode omitir a opção -target.

Os arquivos de classe serão executados no destino especificado por targetCompatibility e em versões posteriores, mas não nas versões anteriores da VM.
