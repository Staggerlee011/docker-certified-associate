# docker swarm

distrubted cluster to run docker. Add enterprise level features to docker.

## Swarm manager

manages and control the worker nodes (similar to k8s design).

### install swarm manager

- [install docker](docker-install.md)

By running swarm init you configure that server as a "manager".

*The advertise-addr is the private ip address! not the public!*

``` c#
docker swarm init --advertise-addr <swarm manager private IP>
```

### Add swarm manager to cluster

- [install docker](docker-install.md)

from a current swarm `master` run the below command and copy the output to the new master server

``` c#
docker swarm join-token manager
```
Example output of `join-token` below

``` c#
docker swarm join --token <token> <swarm manager private IP>:2377
```

The output will then get an output saying the node has joined the swarm.


## install swarm node

- [install docker](docker-install.md)

from a swarm `master` run the below command and copy the output to the node server

``` c#
docker swarm join-token worker
```

Example output of `join-token` below

``` c#
docker swarm join --token <token> <swarm manager private IP>:2377
```

The output will then get an output saying the node has joined the swarm.

## Check status of docker swarm

running docker info now shows more information including details about the swarm

``` c#
docker info
```

example details:

``` c#
Swarm: active
    NodeId: asdfasdfasdfasdf
    Is Manager: true
    ClusterID: werwerwerwera
    Managers: 2
    Nodes: 5
    ...
```

### List nodes in cluster

Run node ls to list out nodes in the cluster (includes master and nodes)

``` c#
docker node ls
```

## Leave a cluster

To leave a cluster as master or node, run the below command on the server you wish to de-activate

``` c#
docker swarm leave
```

## cluster management

standard quorum rules apply (splitbrain etc), so follow normal 3 = good 2 = bad. 

## Backup and restore 

Backup and restores are only completed on `master` nodes. As the worker nodes just run the containers. 

### backup 

on any manager: 

``` c#
sudo systemctl stop docker
sudo tar -zvcf backup.tar.gz -C /var/lib/docker/swarm .
sudo systemctl start docker
```

## restore

``` console
sudo systemctl stop docker
sudo rm -rf /var/lib/docker/swarm/*
sudo tar -zxvf backup.tar.gz -C /var/lib/docker/swarm/
sudo systemctl start docker
docker node ls
```
