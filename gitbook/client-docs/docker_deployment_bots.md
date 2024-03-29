<!-- Docs for docker deployment arbitrage bot -->
# Bot Docker Setup
To run the bot in a containerized environment the repository provides a simple `Dockerfile`. It is possible to spin up containers one by one by using this docker file and chaning the `.env` file, however, it is also possible to spin up multiple instances of the bot using `docker-compose` mechanic from docker and the provided `docker-compose.yml` file (advised). Both of the options use the `Dockerfile` from the repository. </br>
First off, make sure that Docker is correctly installed:
*   [Install Docker](https://docs.docker.com/get-docker/)

The `Dockerfile` currently holds commands to start the `index.ts` file and install the required packages:
```docker
FROM node:19

ENV TERM=xterm
RUN mkdir /usr/src/app
WORKDIR /usr/src/app

COPY package*.json ./
RUN npm install

COPY tsconfig.json ./
COPY src ./src
RUN npm run build

CMD ["node", "out/index.js"]
```
# Docker Run method
This specific section describes how to run a single instance of the bot in a containerized environment. It utilizes the `Dockerfile` and requires a few manual operations. If you plan on spinning up multiple instance of the bot, it might be easier to use the `docker-compose` [method](#docker-compose-method).
### Creating Image
The first step in running the bot in a Docker Container is to create the `image`, to do so, run in the root folder of the repository:
```bash
docker build . -t [name you want]
```
Make sure to replace `[name you want]` with whatever name you would like for the image. 
{% hint style="info" %}
Note: the images will use the environment variable described in `.env`, you have to change these before creating the image.
{% endhint %}

When the image is succesfully created you can view it with:
```bash
docker images

#results in:
REPOSITORY        TAG       IMAGE ID       CREATED       SIZE
skipmev/juno      latest    f03ce8ffe244   5 weeks ago   1.13GB
```

Make sure the image you just created is listed in the above result of the `docker image` command. 

### Starting the Container
To start the previously created image in a Docker Container:
```bash
docker run -restart=always [name of your image]
```
Again, make sure to replace `[name of your image]` with the name of the previously created image. The `--restart=always` flag will make sure the bot will restart on an error. For example when we encounter a timeout by a RPC_ENDPOINT, the bot will restart and continue running. In our case the command would be:
```bash
docker run --restart=always skipmev/juno
```
The output will be the same as starting the bot with `npm start`. After executing the `run` command you will continue to see the logs in console, which you can safely close without the bot shutting down. 
To view all running containers:
```bash
docker ps -a
```
 # Docker Compose method
 If you plan on running multiple instances of the bot that use different `.env` files, it might be more suitable to use the `docker-compose` method. This is supported by the provided `docker-compose.yml` file in the repository that has to be altered to your needs. For example when spinning up two containers, one for terra and one for juno, using the `terra.env` and the `juno.env` respectively, the file looks like this: 
 ```docker
version: '3.9'

services:
  bot-terra:
    build: .
    image: white-whale-bot-terra
    container_name: white-whale-bot-terra
    env_file:
      - terra.env
    restart: always
    stdin_open: true
    tty: true
  
  bot-juno:
    build: .
    image: white-whale-bot-juno
    container_name: white-whale-bot-juno
    env_file:
      - juno.env
    restart: always
    stdin_open: true
    tty: true
    
 ```
Now to build an run both instances (services) we simply hit:
```docker
docker-compose up
```
and the containers should be running on completion, to check, hit:
```docker
docker ps -a
```