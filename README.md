# DOCKER 
> This is a documentation on how to build a docker image from Docfile and start a container / a dev-mode container

### Follow the steps below
- Navigate into the root directory of your app ```cd getting-started/app```

- Check if ```Docfile``` is available. The Docfile contains the instruction to build the docker image of your app. Docker contains so many images. Check it out on https://hub.docker.com/. This project is using the node:12-alpine image

- Run the command ```docker build -t <image-name> .``` The ```image-name``` can be any name you prefer. The command ```docker build -t first-docker-image``` will build a docker image with the name ```first-docker-image``` The ```.``` in the command is telling docker to look for the Docfile in the current directory. That is why it is very important that you are in the root directory of your app. Now when you open your docker desktop app, you will see the image under the images tab.

- Now that you have your docker image set up, the next step is to create a container. All the dependencies, configurations etc of your will be installed in this container. Run the command ```docker run -d -p <host-port>:<container-port> <image-name>``` The ``-d`` will run the new container in a detached mode (in the background and the -p will create both host-port and container-port and map them together. Without the ports we cannot access our app. Do not forget to add the image-name you previously created to the command. For example ``docker run -d -p 3000:3000 first-docker-image`` This command will use the first-docker-image, create a container, load our app into it and serve it on port 3000. When you visit the ``localhost:3000`` you will access the app.

- You have successfully created a docker image and build your first containerized app. Hooray!!!

- Open your app and make a change. When you refresh your browser, you will realize that the app has not updated. For you to see the change, you have to stop the container, remove it and build a new one. This is not an efficient way for developers since it is repetitive and takes too much time. In the next following steps we will look at how to set up a dev-mode container that will update anytime we make changes.

- Firstly install nodemon as a dev dependency in you app and update your add this to your script package.json file `` "dev": "nodemon src/index.js"``


- Make sure you don't have any previous containers running. Run ``docker ps`` to get the container ``id`` Run ``docker rm -f <id>`` to remove the container. For example ``docker rm -f 736788336ccd383`` or you can simple use the docker desktop app to delete the container.

- Make sure you are in the root directory and run the following command ``docker run -dp 3000:3000 -w /app -v "$(pwd):/app" node:12-alpine sh -c "yarn install && yarn run dev"`` This command is likely for fail on windows because ``$(pwd)`` is a linux command to get the absolute path of the root dir. A workaround is to copy the absolute path of your file and replace ``$(pwd)`` with the absolute path eg ``C:\Users\projects\app``. 

- If you are using a Macbook or any ARM64 device then use this command ``docker run -dp 3000:3000 -w /app -v "$(pwd):/app" node:12-alpine sh -c "apk add --no-cache python2 g++ make && yarn install && yarn run dev"``

- You are likely to get a error message ``cannot find image: install latest: locally``. This means that you do not have the node:12-alpine image locally installed. Open a new cmd and run ``docker pull node:12-alpine`` This will install the image and run the command again

- You can watch the logs using ``docker logs -f <container-id>`` You'll know you're ready to go when you see this.

    ```
        $ nodemon src/index.js
        [nodemon] 1.19.2
        [nodemon] to restart at any time, enter `rs`
        [nodemon] watching dir(s): *.*
        [nodemon] starting `node src/index.js`
        Using sqlite database at /etc/todos/todo.db
        Listening on port 3000
    ```

- Make changes in your app and refresh your browser. Hooray!, you have setup a docker development workflow. Happy coding

- Want to dive deeper into docker?....visit https://docs.docker.com/get-started/overview/