# Containers 

## 1. Modularidade

A abordagem do Docker para a containerização se concentra na habilidade de desativar uma parte de uma aplicação, seja para reparo ou atualização, sem interrompê-la totalmente. 

Além dessa abordagem baseada em microsserviços, é possível compartilhar processos entre várias aplicações da mesma maneira como na arquitetura orientada a serviço (SOA).

## 2. Camadas e controle de versão de imagens

1. Cada arquivo de imagem Docker é composto por uma série de camadas. 
2. As imagens são combinadas em uma única imagem. 
3. Uma nova camada é criada quando há alteração na imagem. 
4. Toda vez que um usuário especifica um comando, como executar ou copiar, uma nova camada é criada.

O Docker reutiliza essas camadas para a construção de novos containers, o que **torna o processo de criação muito mais rápido:**

1. As alterações intermediárias são compartilhadas entre imagens, o que melhora ainda mais a velocidade, o tamanho e a eficiência. 
2. O controle de versões é inerente ao uso de camadas. 
3. Sempre que é realizada uma nova alteração, é gerado um changelog integrado, o que fornece controle total sobre as imagens do container.

## 3. Reversão
Talvez a melhor vantagem da criação de camadas seja a habilidade de reverter quando necessário. 

Toda imagem possui camadas. Não gostou da iteração atual de uma imagem? Simples, basta reverter para a versão anterior. 

Esse processo é compatível com uma abordagem de desenvolvimento ágil e possibilita as práticas de integração e implantação contínuas (CI/CD) em relação às ferramentas.

## 4. Implantação rápida

Antigamente, colocar novo hardware em funcionamento, provisionado e disponível, levava dias e as despesas e esforços necessários para mantê-lo eram onerosas. 

Os containers baseados em docker podem reduzir o tempo de implantação de horas para segundos. Ao criar um container para cada processo, é possível compartilhar rapidamente esses processos similares com novos aplicativos.

Como não é necessário inicializar um sistema operacional para adicionar ou mover um container, o tempo de implantação é substancialmente menor. 

Além disso, com a velocidade de implantação, é possível criar dados e destruir os criados pelos containers sem nenhuma preocupação e com facilidade e economia.

Em resumo, a tecnologia Docker é uma abordagem mais granular, controlável e baseada em microsserviços que valoriza a eficiência.
