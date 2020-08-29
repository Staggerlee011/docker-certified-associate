# image cleanup 

connection of commands to find out about and mangae storage for docker images

## system df

reports on storage based used by docker

``` c#
docker system df
```

example output

``` c#
TYPE                TOTAL               ACTIVE              SIZE                RECLAIMABLE
Images              39                  3                   14.6GB              14.2GB (97%)
Containers          7                   4                   2.436kB             0B (0%)
Local Volumes       2                   2                   12.29kB             0B (0%)
Build Cache         0                   0                   0B                  0B
```

Use `-v` to return even more information breaking down each type with individual objects and each of there storage details

``` c#
docker system df -v
```
example output

``` c#
Images space usage:

REPOSITORY                             TAG                 IMAGE ID            CREATED             SIZE                SHARED SIZE         UNIQUE SIZE         CONTAINERS
mcr.microsoft.com/dotnet/core/sdk      3.1-buster          925a86b607a3        5 weeks ago         704.9MB             0B                  704.9MB             0
mcr.microsoft.com/dotnet/core/aspnet   3.1-buster-slim     5d7a95ed1660        5 weeks ago         207.4MB             0B                  207.4MB             0
mcr.microsoft.com/dotnet/core/sdk      3.1-alpine          a3a43191d31d        6 weeks ago         422.1MB             422.1MB             0B                  0
mcr.microsoft.com/dotnet/core/aspnet   3.1-alpine          e4ede6c1c5d4        6 weeks ago         105MB               105MB               0B                  0
alpine                                 latest              a24bb4013296        3 months ago        5.575MB             5.575MB             0B                  0
diamol/base                            latest              78a2ce922f86        4 months ago        5.546MB             0B                  5.546MB             0
diamol/ch02-hello-diamol-web           latest              b53f1d1cbbf0        4 months ago        107.4MB             0B                  107.4MB             4
diamol/ch06-todo-list                  latest              2cfb40526077        4 months ago        225.5MB             0B                  225.5MB             2
diamol/ch03-web-ping                   latest              451f0e4e7a1b        6 months ago        75.3MB              0B                  75.3MB              1

Containers space usage:

CONTAINER ID        IMAGE                          COMMAND                  LOCAL VOLUMES       SIZE                CREATED             STATUS                   NAMES
2c19193906ff        diamol/ch06-todo-list          "dotnet ToDoList.dll"    1                   1kB                 7 days ago          Up 7 days                mynginx
8be5d785291c        diamol/ch06-todo-list          "dotnet ToDoList.dll"    1                   1kB                 7 days ago          Up 7 days                todo2
149c40bd4b41        diamol/ch03-web-ping           "docker-entrypoint.s…"   0                   0B                  13 days ago         Up 13 days               vigilant_fermat

Local Volumes space usage:

VOLUME NAME                                                        LINKS               SIZE
17abca416fcb98208864e03777cadbcbe855b79742ac6ede48bf989046397abe   1                   0B
todo-list                                                          1                   12.29kB

Build cache usage: 0B

CACHE ID            CACHE TYPE          SIZE                CREATED             LAST USED           USAGE               SHARED
```

## image prune

prune images not taged or used by running container.

- use `prune -a` to remove ALL images not in a running container

``` posh
docker image prune
```
