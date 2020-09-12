# network commands

## List networks

``` c#
docker network ls
```

## Inspect network

- details the network type
- whats connected to the network
- labels
- etc

``` c#
docker network inspect my-net
```

## Create a network

Creates a new network called `my-net` as no network type is specificed it will be a `bridge` network.

``` c#
docker network create my-net
```

Create a specific type of network based on driver

``` c#
docker network create --driver overlay NETWORK
```

## remove a network

Creates a new network called `my-net` as no network type is specificed it will be a `bridge` network.

``` c#
docker network rm my-net
```

## Connect to a network

``` c#
docker run -d --name my-net-busybox --network my-net radial/busyboxplus:curl sleep 3600
```

## Update running container to connect to different network

``` c#
docker network connect my-net my-net-nginx
```

## disconnect network

Remove a container from the network

``` c#
docker network disconnect my-net
```

## Embedded DNS

Allows you to create alias for container to use with either container to container communication or container to host

``` c#
docker run -d --name my-net-nginx2 --network my-net --network-alias my-nginx-alias nginx
docker exec my-net-busybox curl my-net-nginx2:80
docker exec my-net-busybox curl my-nginx-alias:80
```

