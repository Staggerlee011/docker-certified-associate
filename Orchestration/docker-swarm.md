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

#### Check status of docker swarm

running docker info now shows more information including details about the swarm

``` c#
docker info
```

example details:

``` c#
Swarm: active
    NodeId: asdfasdfasdfasdf
    Is Manager: trie
    ClusterID: werwerwerwera
    Managers: 2
    Nodes: 5
    ...
```

##### List nodes in cluster

Run node ls to list out nodes in the cluster (includes master and nodes)

``` c#
docker node ls
```

