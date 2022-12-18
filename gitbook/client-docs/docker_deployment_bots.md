<!-- Docs for docker deployment arbitrage bot -->
# Bot Docker Setup
To easily manage multiple setups of the bot per chain we provided a simple `Dockerfile` to run the 
bot in a Docker Container. To do so, make sure that Docker is correctly installed:
*   [Install Docker](https://docs.docker.com/get-docker/)

The `Dockerfile` currently holds commands to start the `index.ts` file and install the required packages:
```docker
FROM node:16

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install

COPY . .

RUN npm run build
RUN mkdir /logs

VOLUME /logs
CMD ["node", "out/index.js"]
```

## Creating Image
The first step in running the bot in a Docker Container is to create the `image`, to do so, run in the root folder of the repository:
```bash
docker build . -t [name you want]
```
Make sure to replace `[name you want]` with whatever name you would like for the image. When the image is succesfully created you can view it with:
```bash
docker images

#results in:
REPOSITORY        TAG       IMAGE ID       CREATED       SIZE
skipmev/juno      latest    f03ce8ffe244   5 weeks ago   1.13GB
```

Make sure the image you just created is listed in the above result of the `docker image` command. 

## Starting the Container
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
docker ps
```
