# clean-up

collection of commands to keep server / computer clean.

## Gather details

list containers running

``` posh
docker container ls
```

list all containers including there status (excited, running etc)

``` posh
docker container ls --all
```

## storage data

Returns the space used on node for images, containers and volumes etc

- use `-v` for details of each type

``` posh
docker system df -v
```

## remove containers

remove **ALL** containers on server

``` posh
docker container rm --force $(docker container ls --all --quiet)
```

remove specific container even if in a running state

``` posh
docker container rm --force 88
```

## image prune

prune images not taged or used by running container.

- use `prune -a` to remove ALL images not in a running container

``` posh
docker image prune
```


