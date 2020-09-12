# exposing containers

exposing a container maps ports to the host

## docker

``` c#
docker run -p HOST_PORT:CONTAINER_PORT
```

``` c#
docker run -d -p 8080:80 --name nginx_pub nginx
```
## swarm

``` c#
docker service create -p HOST_PORT:CONTAINER_PORT
```

## docker port

Shows the ports that open to an existing container

``` c#
docker port nginx_pub
```

Outputs

``` c#
80/tcp -> 0.0.0.0:8080
```

## ps

docker ps list all containers. It also shows ports they are exposed on

``` c#
docker ps
```
Outputs

``` c#
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES    
03e20b8a02ab        nginx               "/docker-entrypoint.…"   36 seconds ago      Up 35 seconds       0.0.0.0:8080->80/tcp   nginx_pub
```

## Host vs ingress

Docker Swarm supports two modes of publishing ports for services!

### ingress

- unless specificed `ingress` is used by default

### Host

- publishes ports directly to the host where the task (container) is running
