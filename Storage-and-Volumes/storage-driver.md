# Storage Driver

## Check

To find out what storage driver is use: `docker info | grep Storage`

## Standard Drivers

Default for ubunutu and centos8 is `overlay2`
  
If you need to do lots of read / writes then suggest using `devicemapper`

## Override / Update driver

Its possible to update the driver being used. `You must only change the value in 1 place` Options to update are

### update daemon.json

you can update daemon.json file located at: `/ect/docker/daemon.json`

Note unless manually created this file will not exist! 

add the follow data

``` json
{
    "storage-driver": "devicemapper"
}
```

followed by

``` console
sudo systemctl restart docker
sudo systemctl status docker
```

### flag at startup

This is not the recommened way.

`/usr/lib/systemd/system/docker.service`

Update section [Service] line:

`ExecStart=/usr/bin/dockerd -H`

to

`ExecStart=/usr/bin/dockerd --stroage-driver devicemapper -H`

update system:

``` console
systemctl daemon-reload
systemctl restart docker
```
