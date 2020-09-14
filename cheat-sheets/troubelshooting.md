# troubleshooting cheat-sheet

## Gather details

list containers running

``` posh
docker container ls
```

list all containers including there status (excited, running etc)

``` posh
docker container ls --all
```

## logs

view logs of container

``` posh
docker container logs 88
```

- 88 = the first 2 lettrs of the containerId (needs to be unique)

view logs of container using container name

``` posh
docker container logs my-container
```

## inspect

view details of the container

``` posh
docker container inspect 88
```

- 88 = the first 2 lettrs of the containerId (needs to be unique)

## top

view processes running in the container

``` posh
docker container top 88
```

- 88 = the first 2 lettrs of the containerId (needs to be unique)

## stats

shows cpu, mem, betwork, disk the container is using. Locks prompt while running (ctrl + c to break out)

``` posh
docker container stats 88
```

## debug mode

`https://docs.docker.com/config/daemon/`

if you need to debug docker you can run either:

``` c#
There are two ways to configure the Docker daemon:

Use a JSON configuration file. This is the preferred option, since it keeps all configurations in a single place.
Use flags when starting dockerd.
```

### deamon.json

``` c#
{
  "debug": true
}
```

### dockerd

``` c#
dockerd --debug
```