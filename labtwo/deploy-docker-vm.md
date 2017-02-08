# Getting Started with Docker #
This lab will build off of the work completed in [Lab 1](../labone/deploy-simple-linux.md), and assumes that you have an Ubuntu VM running in Azure with Docker installed.

## Docker Hello-World ##
Now that we have a docker engine to run with, let's do the defacto hello-world app...

    docker run hello-world

It's that simple... Docker went out to docker hub and downloaded the image called hello-world and ran it. You should see this output:

    Hello from Docker.
    This message shows that your installation appears to be working correctly.
    
    To generate this message, Docker took the following steps:
     1. The Docker client contacted the Docker daemon.
     2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
     3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
     4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.
    
    To try something more ambitious, you can run an Ubuntu container with:
     $ docker run -it ubuntu bash
    
    Share images, automate workflows, and more with a free Docker Hub account:
     https://hub.docker.com
    
    For more examples and ideas, visit:
     https://docs.docker.com/engine/userguide/

## Docker and NGINX
Next we'll run the docker image for NGINX. NGINX is an HTTP server and reverse proxy.

    docker run -d -p 80:80 nginx

This should download the image and start the container and setting up the port forwarding on port 80. To test, from your browser navigate to the url of your machine (this is the same as the SSH server).

> http://DNS-LABLE-YOU-CREATED.eastus.cloudapp.azure.com

You should see the "Welcome to NGINX" default page.

## Create your own Docker Image ##
Use the Docker Docs and create your own image... A good place to start is:

* [Build your own images](https://docs.docker.com/engine/userguide/containers/dockerimages/)

Well that's it for this lab... Time to clean up.

## Delete the Resource Group ##
This command will remove everything you just created!

    azure group delete {RESOURCE GROUP NAME} -q