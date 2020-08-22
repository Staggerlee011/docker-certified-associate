# build images

## image build

Build an image from a `dockerfile` in the folder the command is run from

``` powershell
docker image build --tag web-ping .
```

build an image from a file called `securedockerfile` in a specific folder

``` powershell
docker image build --tag web-ping ./secure/securedockerfile
```

## build management

list all images

``` powershell
docker image ls
```

List all the images where the tag name starts with “w”

``` powershell
docker image ls 'w*'
```



