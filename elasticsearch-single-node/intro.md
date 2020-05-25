# ELasticsearch Single Node with Kibana

In this scenario, you'll learn how to deploy a Elasticsearch and Kibana as a Docker Container.

Elasticsearch single is recommended for dev and monitoring but not for the production or primary store. 

If we have a proper backup strategy still we can risk running a single node in the production too but we don't get all the feature set like fault tolerance and distributed cluster, this is at high risk.

Let us understand how we can start the single node container in this scenario, expecting that you are familiar  with `docker` and `docker-compose` commands.

## Agenda

- Create the docker-compose
- Understand the properties used in Elasticsearch and Kibana
- Run the container
- Health check with 
    - Kibana Console UI 
    - `curl` Command 
- Create a simple document with 
    - mappings
    - settings
- Insert Data into the created index