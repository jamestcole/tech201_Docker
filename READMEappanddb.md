# Deploying the DB on docker

The db requires another addition to the dockerfile and the creation of a docker compose file.

```
version: "2"
services:
  mongo:
    image: mongo:4.4
    container_name: mongo
    #restart: always
    volumes:
     - ./app/mongod.conf:/etc/mongod.conf
    # - ./mongod.conf:/etc/mongod.conf
    # - ./logs:/var/log/mongod/
    # - ./db:/var/lib/mongodb
   
    ports:
     - "27017:27017"
    
    #command: node ./app/seeds/seed.js
   
  app:
    container_name: app
    #restart: always
    build: ./app
    ports:
      - "80:3000"
    links:
      - mongo
    environment:
      - DB_HOST=mongodb://mongo:27017/posts
    command: bash -c "node /usr/src/app/seeds/seed.js && cd /usr/src/app && npm start"
```

The dockerfile now goes in the app folder

```
FROM node:latest

# label
LABEL MAINTAINER=jcole@spartaglobal

#RUN mkdir -p /usr/src/app
#WRKDIR /usr/src/app
WORKDIR /usr/src/app
# copy data app folder
COPY . .

# install dependncies npm
RUN npm install -g npm@7.20.6
RUN npm install express

# expose port
EXPOSE 3000
```

## App and Mongodb on AWS

This can be accomplished by cloning the relevant files to github and then cloning them to your ubuntu instance that has been started in AWS. To start with , an 18.06 ubuntu instance must be deployed with usual security groups for your app.

ssh into your instance with the provided code from the connect tab in git-bash run as admin.

once succesfull do the following commands to set up your environment

```
sudo apt-get update
sudo apt-get upgrade
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo apt install docker-compose

```

Git clone your repository into your instance
```
git clone <githubhttpaddress>

```

go to the appropiate directory (with docker compose in) and then use the docker-compose file

```
sudo docker-compose up -d
```
