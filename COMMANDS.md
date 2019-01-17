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

docker build -t streamdream-node --no-cache .

docker run -it -p 8888:8888 --name streamdream-node-ct --link streamdream-mysql-ct -e DATABASE_HOST=streamdream-mysql-ct streamdream-node

docker run -d -p 8888:8888 --name streamdream-node-ct --link streamdream-mysql-ct -e DATABASE_HOST=streamdream-mysql-ct streamdream-node

## Build and Push
docker build -t itsfrdm/streamdream-node:1.0.0 .
docker tag itsfrdm/streamdream-node itsfrdm/streamdream-node:1.0.0
docker login
docker push itsfrdm/streamdream-node:1.0.0

## MySQL - Run MySQL using Environment Variables from env.list file, MySQL v.5.7

> Needs MySQL v. 5.7, 8.0 doesn't work properly --> authentication error with node.js app

docker run -p 3306:3306 --name streamdream-mysql-ct -v /Users/yvokeller/Development/github/w901_/Volumes/mysql:/var/lib/mysql --env-file /Users/yvokeller/Development/github/w901_/Volumes/env.list -d mysql:5.7

docker run --name streamdream-mysql-ct -v /Users/yvokeller/Development/github/w901_/Volumes/mysql:/var/lib/mysql --env-file /Users/yvokeller/Development/github/w901_/Volumes/env.list -d mysql:5.7

docker run --name streamdream-mysql-ct -v /Users/yvokeller/Development/github/StreamDream-Virtualization/dockerized_apps/mysql/data/var/lib:/var/lib/mysql --env-file /Users/yvokeller/Development/github/StreamDream-Virtualization/dockerized_apps/mysql/env.list -d mysql:5.7

## Enter bash of container

docker exec -it streamdream-mysql-ct bash
docker exec -it streamdream-node-ct bash

## Log in to mysql container

mysql -u root -p
pw1mysql

## Kubernetes
Dashboard aktivieren (optional):
$ kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/master/src/deploy/recommended/kubernetes-dashboard.yaml

Proxy Starten:
$ kubectl proxy

Dashboard abrufen:
http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/

Create Namespace:
{
  "kind": "Namespace",
  "apiVersion": "v1",
  "metadata": {
    "name": "streamdream",
    "labels": {
      "name": "streamdream"
    }
  }
}

Apply changes to deployment:
$ kubectl apply -f depl.yaml

## Weave scope
Installieren:
kubectl apply -f "https://cloud.weave.works/k8s/scope.yaml?k8s-version=$(kubectl version | base64 | tr -d '\n')"

Port Forwarden:
kubectl port-forward -n weave "$(kubectl get -n weave pod --selector=weave-scope-component=app -o jsonpath='{.items..metadata.name}')" 4040

Abrufen:
http://localhost:4040

## Docker Volume (Tomcat)
docker volume create tomcat-vol
docker volume inspect tomcat-vol

docker run --name tomcat-ct -it -p 7777:8080 -v /Users/yvokeller/tmp/tomcat-volume:/usr/local/tomcat tomcat:8.0

docker run --name tomcat-ct -it -p 7777:8080 -v tomcat-vol:/usr/local/tomcat tomcat:8.0

docker run --name tomcat-ct -it -p 7777:8080 tomcat:8.0


run -v /Users/yvokeller/tmp/tomcat-volume:/test -it alpine:latest bash

docker run -v /Users/yvokeller/tmp/tomcat-volume:/test -it ubuntu:16.04 bash

docker run -v tomcat-vol:/Users/yvokeller/tmp/tomcat-volume -it ubuntu:16.04 bash


# Important:

- never copy npm_modules folder when creating docker container image
- give database host value with docker run command --> not localhost in server.js file!

# Links

https://www.youtube.com/watch?v=pOGVngLsaX4

https://haddad.cloud/2017/04/dockerizing-a-nodejs-app/

https://severalnines.com/blog/mysql-docker-containers-understanding-basics

https://stackoverflow.com/questions/50093144/mysql-8-0-client-does-not-support-authentication-protocol-requested-by-server

https://kubernetes.io/docs/tutorials/stateful-application/mysql-wordpress-persistent-volume/
