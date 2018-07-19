## Otimizando análise de logs e rastreamento de usuários utilizando Grafos


----

## Hoje você vai saber como NoSQL mudou a minha vida de DevOps

e pode ajudar você a mudar a vida de outras pessoas.

----

# Por que você usa NoSQL?


----

<!-- .slide: data-background="#ff6d00" -->

# O meu problema

----


# Grandes quantidades de dados, pouco estruturados, em formato de texto, que deveriam ser interpretados.

----

# Quais informações precisavam ser extraídas?

----

<!-- .slide: data-background="#ff9e40" -->

# Quais usuários se conectam do mesmo computador?

----

<!-- .slide: data-background="#ff9e40" -->

# Qual serviço é o mais 'pesado' de uma aplicação?

----

<!-- .slide: data-background="#ff9e40" -->
# Quais são os perfis de usuário que acessam uma aplicação?

----

<!-- .slide: data-background="#ff9e40" -->
# Qual a linha do tempo de um erro reportado?

----

<!-- .slide: data-background="#ff9e40" -->
# Quais são os erros mais frequentes do sistema e com quem acontecem?


----

# Como modelar estes dados?

----

# Depois de alguns experimentos, escolhemos os Grafos

----


# O que são grafos?

Estrutura formada por um conjunto de vértices e arestas.


----

# Quais problemas podem ser resolvidos utilizando grafos?

* Problemas de caminho
* Relacionamentos

----

# Onde são mais utilizados?

Academicamente ?

----

## Teoria dos Grafos

<img src="palestras/2018/tdcsp-2018/img/borign-class.jpg">

----


# E se guardarmos algo nos vérticies e nas arestas?

<img src="palestras/2018/tdcsp-2018/img/neo4j-dados-propriedades.png" width = "50%">

----

# E os relacionamentos?

<img src="palestras/2018/tdcsp-2018/img/neo4j-dados-relacionamento.png" width = "50%">

----

# Ciclo básico de um BD

* Criar Modelo
* Carregar Dados
* Buscar Dados


----

# Dados

<img src="palestras/2018/tdcsp-2018/img/neo4j-dados-selecionados.png" width = "80%">

----

<img src="palestras/2018/tdcsp-2018/img/neo4j-dados-sql.png" width = "80%">

----

<img src="palestras/2018/tdcsp-2018/img/neo4j-dados-estrutura.png" width = "50%">
