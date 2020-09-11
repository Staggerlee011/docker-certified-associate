# docker registry

## Connect to a non tls registry

`--insecure.-registry`

## Content Trust

- [Offical Doc](https://docs.docker.com/engine/security/trust/content_trust/)

Ensures the image is signed by the creator of the image (via Notery).

- It is possible for creators to DCT only certain images. It is not fixed to all images being tagged. Or fixed to a specific tag

### Configure DCT

### Client enforcement

To enable a client to only download trusted content. you need to set variables:

``` c#
export DOCKER_CONTENT_TRUST=1
export DOCKER_CONTENT_TRUST_SERVER=https://<notary-server-hostname>
```

## Backup Operation

- Access control to repos and images
- metadata
- DRT configurations

What isnt backed up:

- Image blobs

