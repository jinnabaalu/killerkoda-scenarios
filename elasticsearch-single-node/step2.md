As mentioned in the intro hope you are familiar with the docker container commands, expecting that we proceed with the environment we have configured for the elasticsearch. 

In the docker-compose we have defined two services `elasticsearch` and `kibana`. Let's look at the other properties defined.

### Elasticsearch 

- `image: docker.elastic.co/elasticsearch/elasticsearch:7.7.0` - Image of version `7.7.0`
- `container_name` - Custom name of the container 
- `environment` -  To run the single need we need to set the container environment with `discovery.type: single-node` and Optional but important when we are running in dev machine `ES_JAVA_OPTS: "-Xms512m -Xmx1024m"`
- `volumes` to maintain the persistancy on restarting the container else we loose the data when we restart the container. Here we have host volume `vibhuviesdata` and container volume `/usr/share/elasticsearch/data`. Host Volume maintains the data for multiple restarts of the container.
- `ports` - Elasticsearch will use port 9200 for requests and port 9300 for communication between nodes within the cluster.
- `networks` - To maintain the security from the other networks in the docker we have created a common network for both kibana and elasticsearch

### Kibana

- `image: docker.elastic.co/kibana/kibana:7.7.0` - We have to use the same version as elasticsearch after `4.6.*`. Check the [Kibana Compatibility with Elasticsearch Matrix](https://www.elastic.co/support/matrix#matrix_compatibility)
- `container_name` - Custom name of the container 
- `environment` -  Kibana is connecting to the container elasticsearch with teh service name and port.
- `ports` - Kibana will use port 9200 for visualising the elasticsearch
- `depends_on` - The property tell the Kibana service to run after elasticsearch

## Run the container

`docker-compose up -d`{{execute}}

### Docker Commands

- Check the status of the container - `docker container ls`{{execute}} 

- Check the logs of the Elasticsearch - `docker logs elasticsearch`{{execute}}

- Check the logs of the Kibana - `docker logs kibana`{{execute}}

- Output contains  

    - Elasticsearch - `"message": "Cluster health status changed from [YELLOW] to [GREEN]`

    - Kibana - `"message":"http server running at http://0:5601"`

This means that both containers are running successfully