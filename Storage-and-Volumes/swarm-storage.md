# swarm storage

similar to k8s, when wanting to using persistant storage across containers (ie access aws efs storage).

## view swarm storage

same as docker. you will see shared storage based on the driver `not` being `local`

``` c#
docker volume ls
```

## configure nodes

you will attach the shared storage to each node that will need this. This will include adding the plugins for

``` c#
docker plugin install --grant-all-permissions vieux/sshfs
```
