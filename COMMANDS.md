# Command List

## Docker

docker ps                                                               show all running containers

docker ps -a                                                            show all existing containers (also not running ones)

docker run -p 8080:8080 node-streamdream                                run streamdream container, map host port 8080 to container port 8080

docker run -it --name test1 -v ~/folder/data:/data ubuntu bash          run container interactive and mount folder data as volume in container under /data

## Logs

docker logs <container-id>

docker inspect <container-id>

docker inspect test-mysql | grep IPAddress

## Running with Env File

docker run -it --env-file ./env.list

## StreamDream node.js Container

docker build -t streamdream-node .

docker run -it -p 8888:8888 --name streamdream-node-ct --link streamdream-mysql-ct -e DATABASE_HOST=streamdream-mysql-ct streamdream-node

## MySQL - Run MySQL using Environment Variables from env.list file, MySQL v.5.7

> Needs MySQL v. 5.7, 8.0 doesn't work properly --> authentication error with node.js app

docker run -p 3306:3306 --name streamdream-mysql-ct -v /Users/yvokeller/Development/github/w901_/Volumes/mysql:/var/lib/mysql --env-file /Users/yvokeller/Development/github/w901_/Volumes/env.list -d mysql:5.7

docker run --name streamdream-mysql-ct -v /Users/yvokeller/Development/github/w901_/Volumes/mysql:/var/lib/mysql --env-file /Users/yvokeller/Development/github/w901_/Volumes/env.list -d mysql:5.7

docker run --name streamdream-mysql-ct -v ./data:/var/lib/mysql --env-file env.list -d mysql:5.7

## Enter bash of container

docker exec -it streamdream-mysql-ct bash
docker exec -it streamdream-node-ct bash

## Log in to mysql container

mysql -u root -p
pw1mysql!$

# Important:

- never copy npm_modules folder when creating docker container image
- give database host value with docker run command --> not localhost in server.js file!

# Links

https://www.youtube.com/watch?v=pOGVngLsaX4

https://haddad.cloud/2017/04/dockerizing-a-nodejs-app/

https://severalnines.com/blog/mysql-docker-containers-understanding-basics

https://stackoverflow.com/questions/50093144/mysql-8-0-client-does-not-support-authentication-protocol-requested-by-server
