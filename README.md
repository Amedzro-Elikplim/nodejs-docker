# DOCKER 
> This is a documentation on how to build a docker image from Docfile and start a container / a dev-mode container

### Follow the steps below
- Navigate into the root directory of your app ```cd getting-started/app```
- Check if ```Docfile``` is available. The Docfile contains the instruction to build the image docker image your app. Docker contains so many images. Check it out on https://hub.docker.com/. This project is using a node:12-alpine image
- Run the command ```docker build -t <image-name>```. The ```image-name``` can be any name you prefer. The command ```docker build -t first-docker-image``` will build a docker image with the name ```first-docker-image```