# docker commands

collection of docker commands

- [docker commit](##commit)
- [docker save](##save)
- [docker load](##load)
- [docker system COMMAND](##system)

## commit

`https://docs.docker.com/engine/reference/commandline/commit/`

Commit allows you to save changes to a running container creating a new image. can be good interactive way to learn and develop a new container

``` c#
## run an interactive ubuntu image
docker run -it ubuntu bin/bash

## from interactive shell run
apt-get update
apt-get -y install nmap

## check nmap is installed
nmap --version
exit

## get containerid ubuntu image
docker ps -a

## commit
docker commit 2b41dd385cc8 ubunut-nmap

## check for new image
docker images

REPOSITORY                             TAG                 IMAGE ID            CREATED             SIZE
ubunut-nmap                            latest              21240ecaa442        27 seconds ago      128MB

## run new container from new image
docker run -it ubuntu-nmap bin/bash

## check nmap is installed
nmap --version
exit
```

## save

creates a tar file of a docker image.

``` c#
docker save ubuntu > ubuntu_save.tar
docker save ubuntu -o ubuntu_save.tar
docker save ubuntu -output ubuntu_save.tar
```

You can use gzip to save the image file and make the backup smaller.

``` c#
docker save myimage:latest | gzip > myimage_latest.tar.gz
```

## load

load can be used to load an image from a tar (ie the output of a `docker save`)

``` c#
docker load < ubuntu_save.tar
docker load -i ubuntu_save.tar
docker load --input ubuntu_save.tar
```

## system

### events

real time events from the server.

Open command line:

``` c#
docker system events
```

Open second command line:

``` c#
docker create --name test alpine:latest top
```

View first command line:

``` c#
2020-09-14T21:44:32.777261100+01:00 container create b6cd3f6ed1a471e55a1e3d0c6c372993c78c0fc677ef7062cb4134d0be3f32a9 (image=alpine, name=test)
```

### df

returns disk space info related to docker (images, containers, local volumes etc)

``` c#
docker system df
TYPE                TOTAL               ACTIVE              SIZE                RECLAIMABLE
Images              13                  7                   2.113GB             1.519GB (71%)
Containers          11                  1                   53.74MB             53.74MB (99%)
Local Volumes       2                   2                   12.29kB             0B (0%)
Build Cache         0                   0                   0B                  0B
```

run `docker system df --verbose` or `docker system df -v` to get break down of each type

### prune

Remove all unused containers, networks, images (both dangling and unreferenced), and optionally, volumes.

``` c#
docker system prune

WARNING! This will remove:
        - all stopped containers
        - all networks not used by at least one container
        - all dangling images
        - all build cache
Are you sure you want to continue? [y/N] y

Deleted Containers:
b6cd3f6ed1a471e55a1e3d0c6c372993c78c0fc677ef7062cb4134d0be3f32a9
40780914016f003c8b49fd7a2c14b3920deb1bd3f5a815eef02758caca66d1ff
2b41dd385cc81d075c211b4fed4b1d6452a98442346370eb34a391994b93841f
2c19193906ff091db2771abb34b9b13f3dd4b16432558d4802e03299338f4f04
8be5d785291c135df7647c0ddac4ba19b1bed870cb222a6df9d76bf876288ee1
149c40bd4b411f8daf84ca0c9a9332e070433dd64c9e2f2e24f6566b7b573c2f
5acbd57ed08f2fe7facccea2deb2b5e3fdc9dd39088acd3b82aa1dda1e65fc51
df0b36aa9a7901292cf3b430b827f19412e07479c88331358ce2a5831c32df3e
5e80bd2d739b4bfbc30cd9a89bbdb74419b5634352ac5bf4a8188cbe4b44ce61
a7151fae74de93d9f6ddd48b4a5051bec5fb656a6b9eff2d760a519d5c00390f

Total reclaimed space: 53.74MB
```

### info

returns the same as `docker info` whici is the server configuration of docker

``` c#
docker system info

Client:
 Debug Mode: false
 Plugins:
  app: Docker Application (Docker Inc., v0.8.0)
  buildx: Build with BuildKit (Docker Inc., v0.3.1-tp-docker)
  mutagen: Synchronize files with Docker Desktop (Docker Inc., testing)

Server:
 Containers: 11
  Running: 1
  Paused: 0
  Stopped: 10
 Images: 13
 Server Version: 19.03.12
 Storage Driver: overlay2
  Backing Filesystem: extfs
  Supports d_type: true
  Native Overlay Diff: true
 Logging Driver: json-file
 Cgroup Driver: cgroupfs
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local logentries splunk syslog
 Swarm: inactive
 Runtimes: runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: 7ad184331fa3e55e52b890ea95e65ba581ae3429
 runc version: dc9208a3303feef5b3839f4323d9beb36df0a9dd
 init version: fec3683
 Security Options:
  seccomp
   Profile: default
 Kernel Version: 4.19.104-microsoft-standard
 Operating System: Docker Desktop
 OSType: linux
 Architecture: x86_64
 CPUs: 12
 Total Memory: 25.04GiB
 Name: docker-desktop
 ID: IINU:W3F2:BTVC:FDGI:WS5G:OHEA:HIYD:X7VV:RKVZ:Y2AU:JJ63:6J5L
 Docker Root Dir: /var/lib/docker
 Debug Mode: true
  File Descriptors: 46
  Goroutines: 56
  System Time: 2020-09-14T20:49:28.1491905Z
  EventsListeners: 3
 Registry: https://index.docker.io/v1/
 Labels:
 Experimental: false
 Insecure Registries:
  127.0.0.0/8
 Live Restore Enabled: false
 Product License: Community Engine

WARNING: bridge-nf-call-iptables is disabled
WARNING: bridge-nf-call-ip6tables is disabled
```