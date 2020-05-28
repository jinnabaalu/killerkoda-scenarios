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

- Pull image from the dockerhub

    `docker pull ubuntu:16.04`{{execute}}

    Lets check the pulled ubuntu image is in the list?

    `docker images`{{execute}}

- Push the image

    `docker push <IMAGE_NAME:TAG>`, you can push the image to docker hub or any docker image registry or private registry with the access credentials.

- Stop the container

    `docker stop vibhuvi`{{execute}}

    Check the container exited status

    `docker ps -a`{{execute}}

- Remove the container

    `docker rm vibhuvi`{{execute}}

    Check the container removed

    `docker ps -a`{{execute}}

- Check the dangling images 

    `docker images -f dangling=true`{{execute}}

- List docker volumes

    `docker volume ls`{{execute}}

- List Danlging Volumes

    `docker volume ls -q -f dangling=true`{{execute}}

- Inspect Volumes 

    `docker volume inspect <VOLUME_ID>`

> In the above command vibhuvi is the container name. We can also check with the container id using `docker logs <CONTAINER_ID>`. 

