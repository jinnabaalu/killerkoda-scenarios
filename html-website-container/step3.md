### Create docker-compose

Deploy or run any service as a container best practice is to create a set of services into one `.yml` file defining the desired behavior of the service. 

Let's create `docker-compose.yml`

```
car <<EOF >>docker-compose.yml
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

    `docker-compose up -d`{{execute}}

Now the application will be running on the server with the host port 8080. 

https://[[HOST_SUBDOMAIN]]-8080-[[KATACODA_HOST]].environments.katacoda.com