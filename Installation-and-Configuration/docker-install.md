# docker install

Install docker community edition

## pre-reqs

### Centos

``` c#
sudo yum install -y device-mapper-persistant-data lvm2
```

### Ubuntu

``` c#
sudo apt-get -y install \
  apt-transport-https \
  ca-certificates \
  curl \
  gnupg-agent \
  software-properties-common
```

## Install docker

- Add docker repo

### Centos

``` c#
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
```

### Ubuntu

``` c#
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo apt-key fingerprint 0EBFCD88

sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```

- Install docker

### Centos

``` c#
sudo yum install -y docker-ce-18.09.5 docker-ce-cli-18.09.5 containerd.io
```

### Ubuntu

``` c#
sudo apt-get update
sudo apt-get install -y docker-ce=5:18.09.5~3-0~ubuntu-bionic docker-ce-cli=5:18.09.5~3-0~ubuntu-bionic containerd.io
```

- Enable service (if needed)

### Centos

``` c#
sudo systemctl start docker
sudo systemctl enable docker
```

- Add users to docker group

On install of docker a new group is created "docker" this group has full access to the docker engine for management. Ensure users managing docker are added  to the group

### Centos & Ubuntu

``` c#
sudo usermod -a -G docker cloud_user
```

- Test docker is running and connecting to dockerhub repository

### Centos & Ubuntu

``` c#
docker version
docker run hello-world
```


``` c#

```


``` c#

```
