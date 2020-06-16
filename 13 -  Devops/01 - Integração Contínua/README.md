# Continuous Integration (CI) - Integração contínua

Em resumo, o CI é um processo de automatização de Build e Testes de código. 

## 1. Passado

No passado, os desenvolvedores de uma equipe podiam trabalhar isoladamente por um longo período e só juntaavam suas alterações à ramificação `master` quando concluíssem seu trabalho. 

Dessa forma, a junção das alterações de códigos era difícil e demorada, além de resultar no acúmulo de erros sem correção por longos períodos. Estes fatores dificultavam uma distribuição de atualizações rápida para os clientes.

## 2. Hoje

A integração contínua é uma prática de desenvolvimento de software em que os desenvolvedores juntam suas alterações de código em um repositório central. Depois disso, criações e testes são executados. 

Geralmente, a integração contínua se refere ao estágio de criação ou integração do processo de lançamento de software, além de originar um componente de automação e um componente cultural. 

Os principais objetivos da integração contínua são encontrar e investigar bugs mais rapidamente, melhorar a qualidade do software e reduzir o tempo que leva para validar e lançar novas atualizações de software.

## 3. Funcionamento 

Com a integração continuada, os desenvolvedores frequentemente confirmam um repositório compartilhado usando um sistema de controle de versão, como o Git. 

Antes de cada confirmação, os desenvolvedores podem escolher executar testes de unidade locais em seus códigos como uma camada de verificação extra anterior à integração. 

Um serviço de integração contínua cria e executa automaticamente testes de unidade nas novas alterações de código para destacar imediatamente todos os erros.

## 4. Vantagens

1. Sistema de controle de versão.
2. Automatização de Build para novas versões, sem intervenção humana. 
3. Self-testing Build para encontrar inconsistências e Bugs. 
4. Integração de áreas para evitar que bugs só sejam encontrados depois do projeto entregue. 
