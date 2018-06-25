# NoSQL

[Diego Silva](http://github.com/diego91964)

----

## SQL - O que são?

Os bancos SQL utilizam o modelo de tabelas e relacionamento entre tabelas para armazenar os dados.

----


## SQL - Por que usar?

Os bancos de dados SQL garantem, obrigatoriamente, as propriedades de atomicidade, consistência, isolamento e durabilidade.


----

## SQL - Atomicidade

Se uma parte da transação falhar, toda transação falhará.


----

## SQL - Consistência


Se uma transação violar a consistência do BD, toda ela será desfeita. Se uma transação for executada com sucesso, o banco atingirá um novo ponto de consistência.


----

## SQL - Isolamento

Múltiplas transações que estejam ocorrendo de forma concorrente, não podem interferir uma nas outras.

----

## SQL - Durabilidade

Garante que uma transação não será perdida, isto é garantido através de logs e políticas de backup.


----

## NoSQL - O que são ?

Bancos de dados NoSQL são bancos de dados não relacionais, otimizados para performance escalável e modelos de dados sem esquema (Fonte:[AWS](https://aws.amazon.com/pt/nosql/)).

----


## NoSQL - Por que usar ?


Os bancos de dados NoSQL são ideais para aplicativos, que exigem maior escalabilidade, maior capacidade de resposta e melhores formas de busca que as oferecidas pelos bancos de dados relacionais tradicionais.


----



## NoSQL - Como funcionam ?

Esses bancos de dados usam diversos modelos de dados, incluindo colunas, documentos, grafos e chave-valor.

----

## NoSQL - Colunas

Um esparso, distribuído e multidimensional map ordenado.

----

## NoSQL - Colunas (BigTable)

<img src="palestras/2018/nosql-iftm/img/bigTable.png">

----


## NoSQL - Documentos

Um banco de dados de documentos é projetado para armazenar dados semiestruturados como documentos. Normalmente, um banco de dados de documentos armazena dados nos formatos JSON ou XML [AWS DynamoDB](https://aws.amazon.com/pt/nosql/document/).


----

## NoSQL - Chave-Valor

Um banco chave-valor é um banco de dados NoSQL otimizado para cargas de trabalho de aplicativos com alto consumo de leitura  [Redis](https://aws.amazon.com/pt/elasticache/what-is-redis/).


----

## NoSQL - Grafos

Os bancos de dados orientados a grafo utilizam o conceito entre vértices e arestas para representar os dados e relacionamento entre eles. É recomendado para dados com alto índice de relacionamento (grafo denso).


----


## NoSQL

<img src="palestras/2018/nosql-iftm/img/nosql-f.jpg">


----  ----

# Prática


<img src="palestras/2018/nosql-iftm/img/checklist-1.png">


----


# Prática - InfluxDb

O InfluxDb é um tipo especial de banco de dados, chamado de Time Series Db.


----

## Time Series Database (TSDB)


Um TSDB é otimizado para dados com registro de data e hora ou séries temporais. Séries temporais são simplesmente medições ou eventos que são rastreados, monitorados, reduzidos e agregados ao longo do tempo.

----

## TSDB - Quando usar?

 São utilizados para armazenar métricas de servidor, monitoramento de desempenho de aplicativos, dados de rede, dados de sensores, eventos, cliques, negociações em um mercado e muitos outros tipos de dados de análise.


----


## TSDB - Qual o diferencial?



A principal diferença de um TSDB com os DB tradicionais é que tudo terá como base a relação cronológica.


----

## TSDB - Como instalar ?

A forma mais simples de criar uma instância de um influxDb é utilizando Docker.

```
docker network create influxdb

docker run -d -p 8083:8083 -p 8086:8086 --net=influxdb -v $PWD/influxdb:/var/lib/influxdb -e INFLUXDB_ADMIN_ENABLED=true -e INFLUXDB_ADMIN_USER=root influxdb:1.0


```

----


## InfluxDb - Rest API

O InfluxDB possui uma api rest que permite executar todos os comandos através do curl.


```

## Ping

curl -sl -I localhost:8086/ping

## Escrita de dados

curl -i -XPOST 'http://localhost:8086/write?db=mydb' --data-binary 'cpu_load_short,host=server01,region=us-west value=0.64 1434055562000000000'

## Buscas

curl -i -XPOST 'http://localhost:8086/query?q=select+host+from+microservice_status&db=mydb'

curl -i -XPOST 'http://localhost:8086/query?q=select+threads+from+microservice_status&db=influxdb1'

```

----

## Influxdb - Web API


<img src="palestras/2018/nosql-iftm/img/influxdb-web.png">


----

## Visualização dos Dados


<img src="palestras/2018/nosql-iftm/img/checklist-2.png">

----

## Visualização dos Dados

A web api do influxDb permite uma visualização muito básica dos dados. Então, precisamos de alguma ferramenta de exibição de Time Series, para este exemplo utilizaremos a ferramenta [Grafana](https://grafana.com/).

```
wget https://s3-us-west-2.amazonaws.com/grafana-releases/release/grafana-5.1.4.linux-x64.tar.gz
tar -zxvf grafana-5.1.4.linux-x64.tar.gz

```

----

## Grafana - O que é?

Grafana é uma ferramenta Open Source para visualização de métricas, ela permite gerar gráficos e índices a partir de Time Series.


----

## Grafana - Como funciona ?


<img src="palestras/2018/nosql-iftm/img/grafana-demo.png">


----


## Grafana - Como funciona ?

<img src="palestras/2018/nosql-iftm/img/grafana-sample.png">


----

## Prática - checklist


<img src="palestras/2018/nosql-iftm/img/checklist-3.png">


----

## Gerar Dados


Vamos utilizar métricas de aplicações Java.

----


## Gerar Dados - Cenário

Vamos utilizar uma série de microserviços gerando dados, para isto, vamos utilizar
a api [Netflix Eureka](https://github.com/Netflix/eureka) para realizar o service discovery.



----

## Eureka Service Discovery


<img src="palestras/2018/nosql-iftm/img/eureka-diagram.jpg">

Fonte: [HowToDoInJava](https://howtodoinjava.com/spring/spring-cloud/spring-cloud-service-discovery-netflix-eureka/)



----

## Projeto de Teste


Para executar os projetos a seguir é necessário a instalação do [Apache Maven](https://maven.apache.org/download.cgi)

```
$ git clone https://github.com/diego91964/demo-influx-springboot.git
$ cd demo-influx-springboot
$ mvn clean install -f service-discovery
$ mvn clean install -f service-metrics-influx
$ mvn clean install -f mservice-1
$ mvn clean install -f mservice-2
$ mvn clean install -f mservice-3
$ java -jar service-discovery/target/service-discovery.jar
$ java -jar mservice-1/target/mservice-1.jar
$ java -jar mservice-2/target/mservice-3.jar
$ java -jar mservice-3/target/mservice-2.jar
$ java -jar service-metrics-influx/target/service-metrics-influx.jar

```

----

## Criando Datasource Grafana

<img src="palestras/2018/nosql-iftm/img/grafana-datasource.png">

----

## Importando o Dashboard

Importar arquivo grafana/dashboard.json no grafana

<img src="palestras/2018/nosql-iftm/img/grafana-import.png">

Créditos: [ypvillazon](https://github.com/ypvillazon)

----

## Demo Dashboard

<img src="palestras/2018/nosql-iftm/img/grafana-demo-2.png">

----  ----

# Prática - Neo4j


Pense no seguinte cenário: Você elaborou uma aplicação extremamente segura, mas, como parte desta segurança fez um sistema de logs capaz de armazenar grande parte dos estados da aplicação.


----


## Problema

Ter uma grande massa de dados é algo muito bom, desde que você nunca precise dela...

----

## Dados armazenados


<img src="palestras/2018/nosql-iftm/img/neo4j-dados-selecionados.png">


----

## Perguntas - Parte 1

* Qual ip um determinado usuário utilizou para acessar um app específico?
* Quais usuários utilizaram um ip?
* Quais serviços foram utilizados de uma aplicação?

----

## Perguntas - Parte 2

* Qual o maior tempo de resposta de uma requisição?
* Qual serviço é o mais 'pesado' de uma aplicação?
* Quais são os parâmetros passados para um serviço?


----

## Como ficaria em SQL ?

<img src="palestras/2018/nosql-iftm/img/neo4j-dados-sql.png" width = "50%">

----

## Como ficaria utilizando grafo?



<img src="palestras/2018/nosql-iftm/img/neo4j-dados-estrutura.png" width = "50%">
