# Storage Driver

## Check Docker Storage

To find out what storage driver is use: `docker info | grep Storage`

## Check Container / Image Storage

you can check individual images / containers via:

``` c#
docker container inspect storage_nginx
```

Look down to the `GraphDriver` -> `Name` for the storage driver

## Standard Drivers

Default for ubunutu and centos8/RHEL is `overlay2`
  
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

## Storage Models

Presistant data storage can be managed use several storage models.

### file system storage

`overlay2` / `aufs`

data is stored in a form of a file on the system. This is standard storage

### block storage

`devicemapper`

better for heavy writes

data stored in blocks.

### Object storage

stores data in a external object. Application must be designed to use object storage. flexible and scaleable

## Device Mapper

- default storage for centos7 and earlier.
- it can be configured via the `daemon config file

device mapper supports 2 modes

### loop-lvm

- default mode used.
- loopback simulates another phy disk to allow file system storage to act like block storage.
- this is not recommend for production services

### direct-lvm

- is a direct connection to real block storage

#### configure direct-lvm

- add block storage
- stop docker `sudo systemctl disable docker && systemctl stop docker`
- Update the daemon.json `/etc/docker/daemon.json`

``` c#
{
  "storage-driver": "devicemapper",
  "storage-opts": [
    "dm.directlvm_device=/dev/nvme1n1",
    "dm.thinp_percent=95",
    "dm.thinp_metapercent=1",
    "dm.thinp_autoextend_threshold=80",
    "dm.thinp_autoextend_percent=20",
    "dm.directlvm_device_force=true"
  ]
}
```

- stack docker `sudo systemctl enable docker && sudo systemctl start docker`

