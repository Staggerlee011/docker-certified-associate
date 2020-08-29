# Storage Layers

- docker storage consists of layers
- you can see the layers of a container when they are created via the steps taken.

## image layers

you can see where docker has stored the image layers via

``` c#
docker image inspect nginx
```

Look down to the `GraphDriver` `Data` will show the location of each layer. and the `Name` of the storage driver

## container layers

you can also see where docker has stored a containers layers via inspect

``` c#
docker container inspect storage_nginx
```

Again look down to the `GraphDriver` `Data` will show the location of each layer. and the `Name` of the storage driver