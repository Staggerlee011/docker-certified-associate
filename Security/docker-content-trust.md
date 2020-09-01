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
