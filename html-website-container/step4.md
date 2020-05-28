These are the very basic and important commands used in the container life cycle.

- Check the containers running

    `docker ps`{{execute}}

- Check the containers existed and running both

    `docker ps -a`{{execute}}

- Check the logs of the container

    `docker logs vibhuvi`{{execute}}

- Inspect the the container

    `docker inspect vibhuvi`{{execute}}

- SSH into the container just like VM

    `docker exec -it vibhuvi`{{execute}}

> In the above command vibhuvi is the container name. We can also check with the container id using `docker logs <CONTAINER_ID>`. 


Now the application will be running on the server with the host port 8080. 

https://[[HOST_SUBDOMAIN]]-8080-[[KATACODA_HOST]].environments.katacoda.com