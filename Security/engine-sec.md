# Docker Engine security

- [docker security doc](https://docs.docker.com/engine/security/security/)

## Namespaces & Control groups (cgroups)

Provide isolation to containers processes. To stop them seeing and others seeing there actions.

To ignore cgroups protection you can run `--privileged`. by default all containers run in `--unprivileged`

`https://docs.docker.com/engine/reference/run/#runtime-privilege-and-linux-capabilities`

``` c#
docker run --privileged
```

## docker daemon

The docker daemon requires `root` privilages. With that it should be secured.

- only allow trusted users to access the daemon
- log actions around the daemon

## Linux kernel capabilities

Linux kernel capabilities allow linux to use fine-grained access to different root level systems. Docker uses capabilities to fine tune container processes.  

This means that a process can run as root inside a container but does not have access to full root priviliages on the host.

example docker uses `net_bind_service` capabilitiy to allow containers processes to bind to ports below 1024 without running them as `root`

## docker daemon http socket

On install the docker deamon is only accessable via the UDP localhost. To enable a `http` for the api you will need to:

- Create a CA
- Create a Server and Client cert
- Configure daemon to use `tlsverifiy` mode (via updating the `deamon.json` with values for the cert)
- configure the client to connect securely via the client cert

## docker run --privileged

https://medium.com/better-programming/docker-tips-mind-the-privileged-flag-d6e2ae71bdb4

``` c#
docker run --privileged
```
