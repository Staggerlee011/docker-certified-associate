# docker swarm

## Autolock

On a new clean install of docker swarm autolock is off. This means that encprytion keys used to communicate between nodes in a cluster are stored unencrypted.

stores keys in encrpyted. Means that a key is needed to restart any cluster node on restart of the docker server.

### Turn on/off autolock

When you inintalize a cluster you can run the below to create a autolock enabled system:

``` c#
docker swarm init --autolock
```

To enable autolock on a cluster run the below from a master node:

``` c#
docker swarm update --autolock=true
```

**BOTH COMMNADS WILLOUT A KEY NEEDED TO RESTART ANY SWARM NODE**

To disable autolock run

``` c#
docker swarm update --autolock=false
```



``` c#

```


### Working with autolock

If autolock is enabled when a the docker service is restarted you will get the below message if you try and run a command without putting in the key:

``` c#
Error responce from daemon: Swarm is encryptred and needs to be unlocked before it can be used. Please use "docker swarm unlock" to unlock it.
```

#### start docker service

When you want to start the service with autolock enabled you will need to run:

``` c#
docker swarm unlock
```

**you will then be asked to put in the key!**

#### Genereate key

If you lose the key and have an active instance still you can run:

``` c#
docker swarm unlock-key
```

#### Rotate key

to update the key to a new value

``` c#
docker swarm inlock-key --rotate
```

