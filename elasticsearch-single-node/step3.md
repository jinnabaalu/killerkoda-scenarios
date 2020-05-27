We have Elasticsearch running, let's try to interact with elaticsearch APIs

We have two options to intearct with Elasticsearch `curl` and `Kibana Console UI`

### Curl

- Cluster health API 

    `curl -X GET "localhost:9200/_cluster/health?pretty"`

- Cluster state API

    `curl -X GET "localhost:9200/_cluster/state/_all?pretty"`

- Cluster Stats API
    `curl -X GET "localhost:9200/_cluster/stats"`

- Cluster Settings API

    `curl -X GET "localhost:9200/_cluster/settings"`


### Kibana UI

- Cluster health API - GET /_cluster/health

- Cluster state API - GET /_cluster/state/_all

- Cluster Stats API - GET /_cluster/stats

- Cluster Settings API - GET /_cluster/settings

