# Docker content trust

provides a secure way to verify the integrity of the image before you pull or run the image.

## Create Content Trusted Repository

connect to registry (dockerhub)

``` c#
docker trust key generate <Username>

Enter a passphase:
```

Add yourself as a signer to the registry

``` c#
docker trust signer add --key <file created from last command> <Username> <reponame>
docker trust signer add --key mykey.pub staggerlee011 staggerlee011/secure-content

Enter your passphase for key:
Enter a passphase for your new repo:
```

## Upload to trusted Repository

Create the image you wish to sign in the example below the build created a image called: staggerlee/mycontainer:signed

``` c#
docker trust sign staggerlee/mycontainer:signed

Enter passphase (used for docker trust key gen...)
```

If you have `DOCKER_CONTENT_TRUST=1` set on the build server you can also upload via the standard push command:

``` c#
docker push staggerlee/mycontainer:signed
```

## Download only Trusted Images

``` c#
DOCKER_CONTENT_TRUST=1
```

Setting this stops you from downloading any container image that does not use DCT!  

- For `docker ee` you can also configure DCT via the `deamon.json`
- if `DOCKER_CONTENT_TRUST=0` you can download both DCT enabled and disabled images (this is the default setting)

## Whitelist Insecure registry

If you use a private hosted registry that uses a self-signed cert or http instead of https. this can be achived via:

### Update deamon.json

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

### DOCKER_OPS -insecure-registry

- `https://nickjanetakis.com/blog/docker-tip-50-running-an-insecure-docker-registry`

``` c#
DOCKER_OPTS="--insecure-registry registry.example.com
```
