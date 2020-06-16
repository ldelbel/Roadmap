# Diagrama UML

## 1. Elementos

Estes são os elementos mais utilizados. 

### 1.1. Class (Classe) 

É a classe propriamente dita. Usamos este elemento quando queremos demostrar visualmente a classe no diagrama 

### 1.2. Association (Associação – conector sem pontas) 

É um tipo de relacionamento usado entre classes. 

Aplicável a classes que são independentes (vivem sem dependência umas das outras), mas que em algum momento no ciclo de vida do software (enquanto ele está em execução) podem ter alguma relação conceitual.

### 1.3. Generalization (Herança – conector com seta em uma das pontas) 

É um tipo de relacionamento onde a classe generalizada (onde a “ponta da seta” do conector fica) fornece recursos para a classe especializada (herdeira). 

Excetuando conceitos mais avançados (como padrões de projeto, interfaces, visibilidades específicas etc.), tudo que a classe mãe (generalizada) tem, a filha (especializada) terá.

### 1.4. Compose (Composição – conector com um “diamante” hachurado na ponta) 

É um tipo de relacionamento onde a classe composta depende de outras classes para “existir”. 

Por exemplo, a classe `CorpoHumano` possui um composição com a classe `Coracao`. Sem a classe `Coracao`, a classe `CorpoHumano` não pode existir.

### 1.5. Aggregate (Agregação – conector com um “diamante” vazado na ponta) 

É um tipo de relacionamento onde a classe agregada usa outra classes para “existir”, mas pode viver sem ela. 

Por exemplo, a classe `CorpoHumano`possui uma agregação com a classe `Mão`. Sem a `Mão`, a classe `CorpoHumano` pode existir. 

## 2. Diagrama

![Diagrama](https://www.ateomomento.com.br/wp-content/uploads/2018/06/diagrama-classes-compartimentos-classes-atributos-operacoes-completo.png)

* Cozinha pode ter ou não uma PortaCozinha, podendo existir se não tiver. (Agregação)

* PortaCozinha generaliza Porta, possuindo todas as características que Porta têm, além das suas específicas. (Generalização)

* Quarto deve ter PortaQuarto, não podendo existir se não tiver. (Composição)

* PortaQuarto generaliza Porta, que tem todas as características que Porta têm, além das suas específicas. (Generalização)

* Sala deve ter PortaSala, não podendo existir se não tiver. (Composição)

* PortaSala generaliza Porta, que tem todas as características que Porta têm, além das suas específicas. (Generalização)

* Sala pode ter ou não uma Porta que não seja uma PortaSala, mas se tiver ou não isso não fará diferença, pois Porta pode existir sem Sala, e Sala pode existir sem Porta. (Associação).

## 3. Ferramentas

http://creately.com/
Visual Paradigm
https://www.lucidchart.com/

