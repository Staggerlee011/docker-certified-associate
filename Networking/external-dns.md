# external dns

If you need to specify a specific external dns host you can do it via 2 ways

- [host](##Host)
- [container](##Container)

## Host

You can update the docker deamon.json file with external dns

### Update deamon.json

``` c#
sudo vi /etc/docker/daemon.json
```

``` c#
{
  "dns": ["8.8.8.8"]
}
```

### Restart Docker

``` c#
sudo systemctl restart docker
```

### Test your DNS by looking up an external domain

``` c#
docker run nicolaka/netshoot nslookup google.com
```

## Container

You can also override the external dns set up in deamon.json file at the container level via running them with `--dns <EXTERNAL DNS>`

``` c#
docker run --dns 8.8.4.4 nicolaka/netshoot nslookup google.com
```
