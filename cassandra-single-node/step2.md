
We have many options to deploy HTML static pages, best practice is to create a Dockerfile for any application framework. So we'll create `Dockerfile` 

```
cat <<EOF >> docker-compose.yml
version: "3.7"
services:
  cassandra-one:
    image: cassandra:3.9
    # volumes:
    #     - cassandra-volume:/var/lib/cassandra/
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
# volumes:
#   cassandra-volume:
#     driver: local
#     driver_opts:
#       o: bind
#       type: none
#       device: /root/db/cassandra-volume/
```{{execute}}

Check the content of the Dockerfile
    `cat Dockerfile`{{execute}}


Dockerfile is the collection of instruction which describes the 

- Environment of the application 
- Set of layers which will help create the image and deploy

The current example we took is a very basic container two layers and a single-stage build. Lets us understand the layers

Layer One: `FROM nginx:1.17.10`

    Every Dockerfile starts with the base image. Base image is the one which provides the environment and supports the application framework for running application in it. Here in our example, we want to deploy HTML page we are using Nginx as a server to deploy.

    1.17.10 is the image tag, which will help identify the which version of the docker image we are using for this current deployment. Never use the default image tag `latest`

Layer Two: `COPY . /usr/share/nginx/html`

    COPY command is to copy any files or folder from source to destination. Here the source is current folder and destination is `/usr/share/nginx/html`

These two layers will be triggered in the order, starts from the base image. Triggers one after the other when we build the docker images of our application.

###  Create the docker image

We use the `docker build` command to create a docker image for our static html application `docker build -t vibhuvi-static:latest .`{{execute}} 

> -t is tag of the image, we can name the image as per our need, here I have created `vibhuvi-static:latest`. `vibhuvi-static` is the image name, `latest` is the tag


This will create a new image `vibhuvi-static:latest`, check the docker images in the image cache. `docker images`{{execute}}