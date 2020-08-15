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

## remove containers

remove **ALL** containers on server

``` posh
docker container rm --force $(docker container ls --all --quiet)
```

remove specific container even if in a running state

``` posh
docker container rm --force 88
```
