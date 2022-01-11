# sync-elasticsearch-mysql
Using Logstash to synchronize an Elasticsearch index with MySQL data

> This project is described in details in this article: [How to synchronize Elasticsearch with MySQL](https://towardsdatascience.com/how-to-synchronize-elasticsearch-with-mysql-ed32fc57b339)

````
ssh -L 5601:127.0.0.1:5601 -N bruno@35.239.213.74
````

## Introduction

This project is a working example demonstrating how to use Logstash to link Elasticsearch to a MySQL database in order to:
- Build an Elasticsearch index from scratch
- Continuously monitor changes on the database records and replicate any of those changes to Elasticsearch (`create`, `update`, `delete`)

It uses:
- MySQL as the main database of a given business architecture (version 8.0)
- Elasticsearch as a text search engine (version 7.9.3)
- Logstash as a connector or data pipe from MySQL to Elasticsearch (version 7.9.3)
- Kibana for monitoring, data visualization, and debuging tool (version 7.9.3)

![Architecture of this project](./docs/sync-elasticsearch-mysql.png)

This repo is a valid prototype and works as it is, however it is not suitable for a production environment. Please refer to the official documentation of each of the above technologies for instructions on how to go live in your production environment.

## Deployment
On your development/local environment, run the following commands on a terminal:

> Note: Make sure to install [Docker](https://docs.docker.com/get-docker/) and [Docker Compose](https://docs.docker.com/compose/install/)

```bash
# Clone this project and cd into it
git clone https://github.com/redouane-dev/sync-elasticsearch-mysql.git && cd sync-elasticsearch-mysql

# Start the whole architecture
docker-compose up # add -d for detached mode

# To keep an eye on the logs
docker-compose logs -f --tail 111 <service-name>
```

To start services separately or in a different order, you can run:
```bash
docker-compose up -d mysql
docker-compose up -d elasticsearch kibana
docker-compose up logstash
```

## Testing
Please refer to the above article for testing steps.

## Resources
- Inspiration by [How to keep Elasticsearch synchronized with a relational database using Logstash and JDBC](https://www.elastic.co/blog/how-to-keep-elasticsearch-synchronized-with-a-relational-database-using-logstash). However the article does not deal with indexing from scratch and deleted records.
- Data used for this project is available in the Kaggle dataset [Goodreads-books](https://www.kaggle.com/jealousleopard/goodreadsbooks)
- [Logstash JDBC input plugin](https://www.elastic.co/guide/en/logstash/current/plugins-inputs-jdbc.html)
- [Logstash Mutate filter plugin](https://www.elastic.co/guide/en/logstash/current/plugins-filters-mutate.html)
- [Logstash Elasticsearch output plugin](https://www.elastic.co/guide/en/logstash/current/plugins-outputs-elasticsearch.html)

## References

- [Como manter o Elasticsearch sincronizado com um banco de dados relacional usando o Logstash e o JDBC](https://www.elastic.co/pt/blog/how-to-keep-elasticsearch-synchronized-with-a-relational-database-using-logstash)
- [Sincronizando dados do PostgreSQL no Elasticsearch](https://blog.4linux.com.br/sincronizando-dados-do-postgresql-no-elasticsearch/)
- [Stream your data changes in MySQL into ElasticSearch using Debezium, Kafka, and Confluent JDBC Sink Connector](https://towardsdatascience.com/stream-your-data-changes-in-mysql-into-elasticsearch-using-debizium-kafka-and-confluent-jdbc-b93821d4997b)
- [How to integrate ElasticSearch with MySQL?](https://stackoverflow.com/questions/36152152/how-to-integrate-elasticsearch-with-mysql)
- [Importing Data from MySQL to Elasticsearch to Visualize it with Kibana](https://datascience-enthusiast.com/Miscellaneous/MySQL_to_ELK.html)
- [Configuring Logstash to push MySQL data into Elasticsearch](https://faun.pub/configure-logstash-to-push-mysql-data-into-elasticsearch-fbeb1b5cb2ae)
- [Lifecycle Management rotate on a daily basis](https://discuss.elastic.co/t/lifecycle-management-rotate-on-a-daily-basis/174263)
- [Deploy a Single Node Elastic Stack Cluster on Docker Containers](https://kifarunix.com/deploy-a-single-node-elastic-stack-cluster-on-docker-containers/)
- [Replicating MySQL data into Elastic search using Logstash JDBC Plugin on Linux/Unix](https://github.com/chaitanyavangalapudi/devops-scripts/wiki/LogStash-JDBC-Plugin)
- [sync-elasticsearch-mysql](https://github.com/redouane-dev/sync-elasticsearch-mysql)
- [How to synchronize Elasticsearch with MySQL](https://towardsdatascience.com/how-to-synchronize-elasticsearch-with-mysql-ed32fc57b339)
- [logstash-schooldb.conf](https://github.com/chaitanyavangalapudi/devops-scripts/blob/master/logstash-jdbc-plugin/logstash-schooldb.conf)
- [Logstash for Synchronize Elasticsearch with DBs](https://mohaamer5.medium.com/logstash-for-synchronize-elasticsearch-with-dbs-e5dda7cea930)
- [Logtash mysql cofiguration file](https://pretagteam.com/question/logtash-mysql-cofiguration-file)
- [elasticsearch-7.15. 2 mysql8. 0.26 logstash input JDBC data full index construction](https://javamana.com/2021/12/202112110716461883.html)
- [Logstash com.mysql.jdbc.Driver não carregado](https://www.ti-enxame.com/pt/jdbc/logstash-com.mysql.jdbc.driver-nao-carregado/808520449/)