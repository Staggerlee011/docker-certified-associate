# docker networking

## Container-Networking-Model-(CNM)

the CNM is based on:

- `sandbox` an isolated unit containging a network components asspcoiated with a single container
- `endpoint` connects a sandbox to a network
- `network` a collection fo endpoints

![mirantis-networking-diag](https://success.mirantis.com/api/images/.%2Frefarch%2Fnetworking%2Fimages%2Fcnm.png)

## Built-In Network Drivers

There are a collection of native drivers CNM (container network model)

- [Host](###Host)
- [Bridge](###Bridge)
- [Overlay](###Overlay)
- [MACVLAN](###MACVLAN)
- [None](###None)

### Host

containers use the host network stack directly

``` c#
docker run -d --net host --name host_nginx nginx
```

- all containers on the same host network use the same namespace
- no 2 containers can use the same ports
- Can connect to container using `host driver` from the host without the need of `-port`
- good for simple app / setup
- no isolation between containers on the same host driver
- no isolation between containers and the host

### Bridge

- Default option for docker on a single host
- DOESNT WORK FOR DOCKER SWARM
- Creates a `bridge0` network in linux

``` c#
docker network create --driver bridge my-bridge-net
```

### Overlay

Default Swarm network driver

- uses VXLAN data plane to allow traffic between containers without needing more information
- automatically configures the interfaces, bridges for each host to talk to each other

``` c#
docker network create --driver overlay my-overlay-net
```

### MACVLAN

Lightweight implementation connecting containers to hosts

- Uses linux interfaces instead of bridge interface
- harder to configure dependency between MACVLAND and external network
- good for less latency if used correctly
- good if you need ip from external subnet from host

``` c#
docker network create -d macvlan --subnet 192.168.0.0/24 --gateway 192.168.0.1 -o parent=eth0 my-macvlan-net
```

### None

No network driver provider

- Each container is completely isolated from host or containers
- if you want a container to connect to a network is must be configured manually
- creates a seperate network namespace for ecah container but has no endpoint

``` c#
docker run --net none -d --name none_nginx nginx
```

## UDP

to create a network or publish to udp / tcp / sctp use

``` c#
--p 8080:80/tcp
--p 8080:80/udp
--publish 8080:80/sctp
```

if you wish to use mulitple types you will need to call publish twice

``` c#
docker service create \
  --replicas 3 \
  --network my-network \
  --name my-web \
  --publish 8080:80/tcp \
  --publish 8080:80/udp \
  nginx
```
