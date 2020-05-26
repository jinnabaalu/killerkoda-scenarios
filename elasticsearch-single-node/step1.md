Create the `docker-compose.yml` with the following

```
cat <<EOF >>docker-compose.yml

version: "3"
services:
    elasticsearch:
        image: docker.elastic.co/elasticsearch/elasticsearch:7.7.0
        container_name: elasticsearch
        environment:
            discovery.type: single-node
            # ES_JAVA_OPTS: "-Xms256m -Xmx256m"
        volumes:
            - vibhuviesdata:/usr/share/elasticsearch/data
        ports:
            - 9200:9200
        networks:
            - elastic
        labels:
            - co.elastic.logs/module=elasticsearch
            - co.elastic.metrics/module=elasticsearch
    kibana:
        image: docker.elastic.co/kibana/kibana:7.7.0
        container_name: kibana
        ports:
            - 5601:5601
        depends_on:
            - elasticsearch
        environment:
            ELASTICSEARCH_URL: http://elasticsearch:9200
            ELASTICSEARCH_HOSTS: http://elasticsearch:9200
        networks:
            - elastic
networks:
    elastic:
      driver: bridge  
volumes:
    vibhuviesdata:
      driver: local

EOF
```{{execute}}


Check the content of `docker-compose.yml` file 


`cat docker-compose.yml`{{execute}}


