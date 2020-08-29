# docker storage

Volumes are how you manage storage for stateful applications when the data needs to be persistent. Volumes exist independently of containers and have their own life cycles, but they an be attached to containers.

## Attach Volumes

Volumes can be attached 2 ways:

## attach volume via dockerfile

If you use the `volume` command in a dockerfile. It will create a volume in the default location for docker (Windows is c:/data)

``` dockerfile
FROM diamol/dotnet-aspnet
WORKDIR /app

ENTRYPOINT ["dotnet", "ToDoList.dll"]
VOLUME /data
COPY --from=builder /out/ .
```

## docker volume create

To create a volume manually run `docker volume create <name of volume>` Note if you create a volume in the `docker container run` it will automatically run the `docker volume create`

``` c#
docker volume create app
docker container run --name mynginx --volumes=/app nginx:latest
## or create vol via run
docker container run -d -p 8011:80 --name mynginx -v todo-list:/data diamol/ch06-todo-list
```

## read only

you can mount the volume to be read only to the container

``` c#
docker run -v volume-name:/path/in/container:ro my/image
```

- Note the `:ro` at the end of the volume

## List Volumes

list volumes in docker

``` c#
docker volumes ls
```

## inspect

get details of driver, mountpoint etc

``` c#
docker volume inspect todo-list

[
    {
        "CreatedAt": "2020-08-22T19:45:17Z",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/todo-list/_data",
        "Name": "todo-list",
        "Options": null,
        "Scope": "local"
    }
]
```

## volume prune

WARNING! This will remove all local volumes not used by at least one container.
Are you sure you want to continue? [y/N]

``` c#
docker volume prune

# filter
???

# force prune
docker volume prune -f
docker volume prune --force
```

## volume rm

``` c#
docker volume rm todo-list
```

## mount

allows you to attach a external vlumne but to a specific location on the node storage instead of a docker managed storage location. 

``` c#
docker run --mount type=bind,source=/home/cloud_user/message,destination=/root,readonly busybox cat /root/message.txt
```

or 

``` c#
docker run --mount type=volume,source=my-volume,destination=/root busybox sh -c 'echo hello > /root/message.txt && cat /root/message.txt'
```



