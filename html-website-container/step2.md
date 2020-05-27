Dockerfile is the collection of instruction which describes the 

- Environment of the application 
- Set of layers which will help create the image and deploy

The current example we took is a very basic container two layers and a single-stage build. Lets us understand the layers

Layer One: `FROM nginx:1.17.10`

    Every Dockerfile starts with the base image. Base image is the one which provides the environment and supports the application framework for running application in it. Here in our example, we want to deploy HTML page we are using Nginx as a server to deploy.

Layer Two: `COPY . /usr/share/nginx/html`

    COPY command is to copy any files or folder from source to destination. Here the source is current folder and destination is `/usr/share/nginx/html`

These two layers will be triggered in the order, starts from the base image. Triggers one after the other when we build the docker images of our application.