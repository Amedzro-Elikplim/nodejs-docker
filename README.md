# DOCKER 
> This is a documentation on how to build a docker image from Docfile and start a container / a dev-mode container

### Follow the steps below
- Navigate into the root directory of your app ```cd getting-started/app```

- Check if ```Docfile``` is available. The Docfile contains the instruction to build the image docker image your app Docker contains so many images. Check it out on https://hub.docker.com/. This project is using the node:12-alpine image

- Run the command ```docker build -t <image-name> .``` The ```image-name``` can be any name you prefer. The command ```docker build -t first-docker-image``` will build a docker image with the name ```first-docker-image``` The ```.``` in the command is telling docker to look for the Docfile in the current directory. That is why it is very important that you are in the root directory of your app. Now when you open your docker desktop app, you will see the image under the images tab.

- Now that you have your docker image set up, the next step is to create a container. All the dependencies, configurations etc of your will be installed in this container. Run the command ```docker run -d -p <host-port>:<container-port> <image-name>``` The ``-d`` will run the new container in a detached mode (in the background and the -p will create both host-port and container-port and map them together. Without the ports we cannot access our app. Do not forget to add the image-name you previously created to the command. For example ``docker run -d -p 3000:3000 first-docker-image`` This command will use the first-docker-image, create a container, load our app into it and serve it on port 3000. When you visit the ``localhost:3000`` you will access the app.

- You have successfully created a docker image and build your first containerized app. Hooray!!!
- 