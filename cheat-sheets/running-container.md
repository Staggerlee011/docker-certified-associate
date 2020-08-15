# Running a docker container

Collection of commands to run against containers 

- standard run command
- interactive commands
  - interactive (-i)
  - exec
- copy

## standard http image

``` powershell
docker run -d -p 8080:8080 --name myapp alpine:latest
```

- -d = detached (starts the container in the background and doesnt lock out the command prompt)
- -p = port (publishes the port <computer port>:<container port>)
- -name = name of container
- alpine:latest = name of the image to use and tag to pull

## Interact with container

### Interactive

Run a new alpine:latest and create a stdin interactive session

``` powershell
docker container run --interactive --tty alpine:latest
```

- --interactive = open connection to container (stdin)
- --tty = connect to a terminal session inside the container

Run a new dos-web:latest and run a singe command then close the container

``` powershell
echo "hello" | docker run -i alpine cat
```

### exec

connect to an already running container (gather name from `docker container ls`)

``` powershell
docker container exec 5a ls /usr
```

### copy files to container

copy a file to a running container

``` powershell
docker container cp index.html 86b:/usr/local/apache2/htdocs/index.html
```

- cp = copy
- index.html = file being copied from current server/computer directory
- 86b: = name of container to copy file to
- /usr/local/apache2/htdocs/index.html = directory and name of file to copy into
