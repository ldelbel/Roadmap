# Devops

Devops é um termo criado para descrever um conjunto de práticas para integração entre: 
* equipes de desenvolvimento de softwares; 
* operações (infraestrutura ou sysadmin); 
* apoio (como controle de qualidade); 

Estes processos apoiam a adoção de processos automatizados para produção rápida e segura de aplicações e serviços. 

O conceito propõe novos pensamentos sobre o trabalho para a valorização da diversidade de atividades e profissionais envolvidos e atitudes colaborativas. 

É um processo que torna possível o desenvolvimento ágil de aplicações em um modelo de gestão de infraestrutura definido sob regras rígidas e burocráticas.

Como o DevOps é destinado a ser um modo de trabalho inter-funcional, em vez de uma única ferramenta DevOps, existem conjuntos (ou "cadeia de ferramentas") de várias ferramentas. 

Espera-se que essas ferramentas DevOps se encaixem em uma ou mais destas categorias citadas abaixo, refletidas de aspectos-chave do processo de desenvolvimento e entrega de sistemas:

**1. Planejamento/Codificação**: desenvolvimento e revisão de código, ferramentas de gerenciamento de código-fonte, fusão (merge) de código

**2. Criação/Compilação:** ferramentas de integração contínua, estado de compilação

**3. Teste/Verificação:** ferramentas de teste contínuo que fornecem feedback sobre riscos do negócio

**4. Pacote :** repositório de artefato, etapa de pré-implantação de aplicação

**5. Liberação:** gerenciamento de mudança, aprovações de liberação, automação de liberação

**6. Configuração:** configuração e gerenciamento de infraestrutura, ferramentas de Infraestrutura como Código

**7. Monitoramento:** monitoramento de desempenho de aplicações, experiência do usuário final.

**8. Planejamento/Codificação...**

![Devops](https://upload.wikimedia.org/wikipedia/commons/0/05/Devops-toolchain.svg)

## 1. Membros de um time 

* PO/PM
* Developers: Front e backend
* Tester
* Designer

## 2. Ambientes

### 2.1. Desenvolvimento

Ambiente de desenvolvimento é o ambiente que os desenvolvedores utilizam para construir o software. Pode ser a sua máquina ou uma máquina virtual que você utilize para programar.

### 2.2. Homologação 

O ambiente de homologação é o ambiente de teste, o desenvolvedor irá produzir o software no ambiente de desenvolvimento e então irá publica-lo no ambiente de homologação. Neste ambiente o cliente apenas verifica se o que foi executado atende ao solicitado. Não é obrigação do cliente fazer testes na aplicação.

### 2.3. Produção 

O ambiente de produção é onde os usuários finais acessarão o software, pode ser um servidor web. Após homologação(aceite do cliente), o sistema é liberado em produção.

### 2.4. Utilização dos ambientes

Em resumo, quem usa o quê: 

* Amb. Desenvolvimento = utilizado pelo desenvolvedor.
* Amb. Homologação = utilizado para testes da aplicação.
* Amb. Produção = utilizado pelo usuário final.
