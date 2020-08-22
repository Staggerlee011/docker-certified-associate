# docker registry



## Docker trusted Registry (DTR)

### immutable images

stops the possiblity of overwritting a image tag by another person. (Doesnt apply to latest?).

``` c#
Example:
- user1 tags myimage:1
- user2 tries commit there branch of code to myimage:1

- If Immutable images it TURNED ON! this will succed
- If Immutable imagse is TURNED OFF! this will fail
```

## Connect to a non tls registry

`--insecure.-registry`

## Content Trust

- [Offical Doc](https://docs.docker.com/engine/security/trust/content_trust/)

Ensures the image is signed by the creator of the image (via Notery).

- It is possible for creators to DCT only certain images. It is not fixed to all images being tagged. Or fixed to a specific tag

### Configure DTC

### Client enforcement

To enable a client to only download trusted content. you need to set variables:

``` c#
export DOCKER_CONTENT_TRUST=1
export DOCKER_CONTENT_TRUST_SERVER=https://<notary-server-hostname>
```

## Backup Operation

- Access control to repos and iamges
- metadata
- DRT configurations

What isnt backed up:

- Image blobs

