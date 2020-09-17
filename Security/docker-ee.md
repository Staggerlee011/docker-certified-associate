# docker enterprise edition

| docker community edition (CE) | docker enterprise edition (EE) |
|- |- |
| All docker updates | All features of CE |
| Docker Swarm | UCP |
| Oracestration | DTR |
| Networking | Vulnerability scanning |
| Security | Federated applicaiton mangement |

## install EE

`NOTE THIS IS AN OLD VIDEO BEFORE MIRANTIS BROUGHT DOCKER EE! STEPS SHOULD BE REVIEWED!`

- sign up to docker-hub
- start docker ee trail
- Get unique docker EE url
- setup via `https://hub.docker.com/my-content`
- set environment variables for server:

``` c#
DOCKER_EE_URL=<your docker ee url>
DOCKER_EE_VERSION=18.09
```

- add pre-reqs

``` c#
sudo apt-get install -y \
  apt-transport-https \
  ca-certificates \
  curl \
  software-properties-common
```

- add gpg and apt repo

``` c#
curl -fsSL "${DOCKER_EE_URL}/ubuntu/gpg" | sudo apt-key add -

sudo add-apt-repository \
  "deb [arch=$(dpkg --print-architecture)] $DOCKER_EE_URL/ubuntu \
  $(lsb_release -cs) \
  stable-$DOCKER_EE_VERSION"
```

- install docker ee

``` c#
sudo apt-get update
sudo apt-get install -y docker-ee=5:18.09.4~3-0~ubuntu-bionic
sudo usermod -a -G docker cloud_user
```
