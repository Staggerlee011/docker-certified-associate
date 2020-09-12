# troubleshooting networks

## Logs

Read logs

``` c#
docker run --name log-container busybox echo Here is my container log!
docker logs log-container
```

Docker swarm uses the same commands for reading logs

``` c#
docker service create --name log-svc --replicas 3 -p 8080:80 nginx
curl localhost:8080
docker service logs log-svc
```

## Read Deamon log

Return logs for docker deamon

``` c#
sudo journalctl -u docker
```

## netshoot

netshoot is a container image that contains lots of network tools on it

- `https://github.com/nicolaka/netshoot`

``` c#
docker run --rm --network custom-net nicolaka/netshoot curl custom-net-nginx:80
```

You can also run the image in the sandbox of another container! (ie k8s sidecar)

``` c#
docker run --rm --network container:custom-net-nginx nicolaka/netshoot curl localhost:80
```
