Run the following command to create the `docker-compose.yml`

## Cassandra Docker Compose Configuration

- Create the docker-compose file configuration for cassandra container

```
cat <<EOF >> docker-compose.yml
version: "3.7"
services:
  cassandra-one: 
    image: cassandra:3.9
    container_name: cassandra
    ports:
      - 7000:7000
      - 7001:7001
      - 7199:7199
      - 9042:9042
      - 9160:9160
    environment:
      - CASSANDRA_CLUSTER_NAME='sample-cluster'
      - CASSANDRA_NUM_TOKENS=256
      - CASSANDRA_ENDPOINT_SNITCH=GossipingPropertyFileSnitch
      - CASSANDRA_DC=sample-datacenter-one
      - CASSANDRA_RPC_ADDRESS=0.0.0.0
    restart: always
EOF
```{{execute}}

- Check the files available run `ls -l`{{execute}}
- Check the file configuration created `cat docker-compose.yml`{{execute}}
- Run the container `docker-compose up -d`{{execute}}

### What does the above commands do

1. Creates a network to run the container, meaning docker have its own network and a firewall, Creating network "root_default" with the default driver
2. Pull the docker image from the dockerhub, as we are running for the first time, otherwise it will pick the docker image from the local docker image cache.
3. Then start running the cassandra
4. Above  defined ports will be opened from the docker container to the host so that we can access it from the host machine network to docker network.


- Check the status of the container `docker ps -a`{{execute}}
- Check logs of the container `docker logs cassandra`{{execute}}
