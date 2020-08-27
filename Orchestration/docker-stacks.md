# docker stacks

Allows you to deploy multiple containers and scale them on a docker swarm.

## docker stack vs docker compose

- compose works for a single docker service
- stacks work across a cluster

## Stack file

### example

Example stack for deploying wordpress

``` docker
version: '3'

networks:
   frontend:
   backend:

volumes:
     db_data: {}
     wordpress_data: {}

services:
    db:
      image: mysql:5.7
      volumes:
        - db_data:/var/lib/mysql
      environment:
        MYSQL_RANDOM_ROOT_PASSWORD: '1'
        MYSQL_DATABASE: wordpress
        MYSQL_USER: wordpress
        MYSQL_PASSWORD: wordpressPASS
      networks:
        - backend

    wordpress:
      depends_on:
        - db
      image: wordpress:latest
      volumes:
        - wordpress_data:/var/www/html/wp-content
      environment:
        WORDPRESS_DB_HOST: db:3306
        WORDPRESS_DB_USER: wordpress
        WORDPRESS_DB_PASSWORD: wordpressPASS
        WORDPRESS_DB_NAME: wordpress
      networks:
        - frontend
        - backend

    nginx:
      depends_on:
        - wordpress
        - db
      image: nginx:latest
      volumes:
        - ./nginx.conf:/etc/nginx/nginx.conf
        - /etc/letsencrypt/:/etc/letsencrypt/
      ports:
        - 80:80
        - 443:443
      networks:
       - frontend
```

### networking

- stacks services can speak to each other by default (the same as k8s)
- You can create networks via setting the `networks` command. Only objects tagged into that network can then speak to each other
- it is possible to be attached to multiple networks

``` c#
    wordpress:
      depends_on:
        - db
      image: wordpress:latest
      networks:
        - frontend
        - backend
```

### scaling stacks

You can scale any service via setting the `deploy` `replica`

``` c#
    nginx:
      image: nginx:latest
      deploy:
        replicas: 3
```

### setting dependencies

it is possible to tell a service not to start until another service is up and ready (same as docker-compose) using the `depends_on`

``` c#
wordpress:
      depends_on:
        - db
      image: wordpress:latest
```

## docker stack commands

Collection of popular commands

### list

list current stacks

``` c#
docker stack ls
```

### tasks

list associated tasks to the stack

``` c#
docker stack ps <STACK NAME>
```

### services

list services in the stacks

``` c#
docker stack services <STACK NAME>
```




### Deploy a stack

``` c#
docker stack deploy -c simple-stack.yml simple
```

- deploys as stack from a file `simple-stack.yml`
- names the stack `simple`

### Delete a stack

``` c#
docker stack rm simple
```

- removes the stack named `simple`

## docker-compose

allows you to run 1 or more containers from a single file to create an application.

**DOCKER COMPOSE IS NOT NEEDED FOR DOCKER STACK TO RUN ON A DOCKER SWARM**

### install

docker-compose is not installed as part of docker CE or swarm and needs to be installed seperately

``` c#
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose version
```
