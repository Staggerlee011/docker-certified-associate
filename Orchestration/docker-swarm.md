# docker swarm

- [Cluster management](##Cluster-Management)
- [Autolock](##Autolock)
- [labels](##labels)

## Cluster-Management

### Swarm managers

Uses the `Raft consensus algorithm` to maintain cluster state across swarm managers

### Quorum

majority (more than half) of managers in the swarm. must be maintained to keep the cluster state.

- Standard to have odd number of managers for quorum support
- If we lose quorum. You cannot update any tasks or systems on the cluster.
- spread masters across availailibty zones

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

## labels

- Labels help to specify objects management better. 

### Add node label

``` c#
docker node update --label-add environment=production
docker node update --label-add az=b
```

### View existing node labels

``` c#
docker node inspect
```

### --constaint


Ensure a service only runs a worker node and not a master node

``` c#
docker service create --name nginx-workers-only --constraint node.role==worker nginx
```

Add docker swarm service task to label node

``` c#
docker service create --constraint node.labels.environment==production nginx
```

`!=` (not) also works to host on a server without a tag

``` c#
docker service create --constraint node.labels.az!=a nginx
```

### placement-pref

`spread=`

Will spread the 3 replicas evenly (as possible) across any available labels of av (ie: 1 in a, 1 in b, 1 in c)

``` c#
docker service create --name nginx-scale --placement-pref spread=node.label.av --replicas 3 nginx
```