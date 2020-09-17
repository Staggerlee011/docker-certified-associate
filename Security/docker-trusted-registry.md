# docker trusted registry

## Purpose

Allows you to host your own private dockerhub. (similar to ECR and azure alternatives).

- DTR is a feature in UCP
- Adds web ui
- HA through the use of nodes
- RBAC
- security vulnerability scanning

## install

- [ucp installed](universal-control-plane.md)
- in UCP web ui -> admin -> admin settings -> docker trusted registry
- gives a command to set up the install:

example:

``` c#
docker run -it --rm docker/dtr install \
  --ucp-node <DTR node hostname> \
  --ucp-username admin \
  --ucp-url https://<UCP Manager private IP> \
  --ucp-insecure-tls
```

- `when running it will ask for the UCP admin password`
- go to the https://<UCP Manager private IP>
- login with the ucp admin password

## sizing

|service | min | recommended |
|- |- |- |
| memnory | 16 | 16 |
| cpu | 2 | 4 |
| disk | 10gb | 25-100gb |

## backup restore

`https://docs.mirantis.com/docker-enterprise/v2.1/dockeree-products/dtr/dtr-admin/disaster-recovery/create-a-backup.html`

### backups

- copy/tar the dtr container mounted volumes on the host server
- taking a copy of the container image

### restores

- stop dtr
- restore voumes from tar
- deploy saved container image

## DTR Security

### security scanning

- runs scans like `clair`
- must be enabled to be used
- default is to manually run scans
- you can enable scans on new uploads

### managing certificates

You can deploy your own certificates for the UCP / DTR web ui instead of the self signed certs from install

- click System, General, then under Domain & Proxies select Show TLS settings

## DTR Settings

### Immutability

`works the same as ECR`

- Default is OFF
- Means that images can be saved to DTR and overwrite a image with the same tag

### Garbage collection

`https://docs.docker.com/registry/garbage-collection/`

In the context of the Docker registry, garbage collection is the process of removing blobs from the filesystem when they are no longer referenced by a manifest. Blobs can include both layers and manifests.

### Whitelist Insecure registry

If you use a private hosted registry that uses a self-signed cert or http instead of https. this can be achived via:

#### Update deamon.json

- `https://docs.docker.com/registry/insecure/`

Files default location is:

``` c#
/etc/docker/daemon.json
```

Add the `insecure-registries` with the address of the registry you want to use

``` c#
{
  "insecure-registries" : ["myregistrydomain.com:5000"]
}
```

#### DOCKER_OPS -insecure-registry

- `https://nickjanetakis.com/blog/docker-tip-50-running-an-insecure-docker-registry`

``` c#
DOCKER_OPTS="--insecure-registry registry.example.com"
```
