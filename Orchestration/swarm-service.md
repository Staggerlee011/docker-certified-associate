# docker swarm service

Service is used to an application in docker swarm.

``` c#
docker service create --name nginx --replicas 3 nginx
```

- Creates a service with name nginx from `--name nginx`
- Creates 3 replicas via `--replica 3`
- uses the nginx:latest image from `nginx`

## templates

can used to give dynamic values to some flags

- hostname
- mount
- env

``` c#
docker service create --name node-hostname --env NODE_HOSTNAME="{{.Node.Hostname}}" --replicas 3 nginx
```

## Managing services

list services

``` c#
docker service ls
```

list a service tasks

``` c#
docker service ps <NAME OF SERVICE>
```

inspect service

``` c#
docker service inspect <NAME OF SERVICE>
docker service inspect --pretty <NAME OF SERVICE>
```

- `--pretty` for readability

update service

``` c#
docker service update
docker service update --replicas 2 <NAME OF SERVICE>
```

delete service

``` c#
docker service rm <NAME OF SERVICE>
```

## Replicated vs Global Services

### --replicas

creates the specific number of containers you request

``` c#
docker service create --name nginx --replicas 3 nginx 
```

### -- global

Creates a node on each worker node. (will automatically create if a new worker node is brought up)

``` c#
docker service create --name nginx --replicas 3 nginx 
```

## Scaling replicas

It is possible to scale replicas via:

- achives the same thing as `--replica`

``` c#
docker service scale nginx=4
```

## service logs

are available via

``` c#
docker service logs <SERVICE NAME>
```