# docker inspect

returns detailed information around a docker object. In both docker CE and docker swarm.

``` c#
docker inspect <OBJECT>
```

Works on:

- docker containers
- swarm services

Can be called by:

``` c#
docker container inspect <CONTAINER ID>
docker service inspect <CONTAINER ID>
```

- `--pretty` only works on service

## --format

if you wish to retrieve specific information from the inspect you can filter via:

``` c#
docker inspect --format='{{.LogPath}}' $INSTANCE_ID
docker inspect --format='{{.Config.Image}}' $INSTANCE_ID
```
