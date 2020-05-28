### Create docker-compose

Deploy or run any service as a container best practice is to create a set of services into one `.yml` file defining the desired behavior of the service. 

Let's create `docker-compose.yml`

```
cat <<EOF >>docker-compose.yml
version: "3"
services:
  static-app:
    image: vibhuvi-static
    container_name: vibhuvi
    ports:
      - 8080:80
EOF
```{{execute}}

In the above example 

- We have defined single service
- Image name used that we created in the previous step
- We are trying to open the container port `80` on the host port `8080`, this mapping of ports will help us map to any available ports without conflicting with other containers. 

### Run the application

We run the application using the docker-compose up `docker-compose up -d`{{execute}}

### Custom compose file

Here `docker-compose up -d` default file is docker-compose.yml, if the file name is `vibhuvi.yml` then the above command will change like  `docker-compose -f vibhuvi.yml up -d`

Let's try with an example, 

- Stop the previously running container `docker-compose down`{{execute}}

- Create the new compose file from the docker-compose.yml `mv docker-compose.yml vibhuvi.yml`{{execute}}

- Run the container with custom compose file `docker-compose -f vibhuvi.yml up -d`{{execute}}

Now the application will be running on the server with the host port 8080. 

https://[[HOST_SUBDOMAIN]]-8080-[[KATACODA_HOST]].environments.katacoda.com

### Run same aplication on multiple ports

When we run multiple applications we may fall into the conflict situation where two applications may use same port. Docker provides freedom to set the HOST PORT as per our need.
So that we can change ports `8080:80` to `8081:80`