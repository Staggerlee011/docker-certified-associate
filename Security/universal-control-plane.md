# universal control plane (UCP)

An orchastration tool that sits ontop of docker ee (like istio ontop of k8s).

- You cannot turn swarm into UCP. It must be configured at the start
- Adds web portal to manage either docker swarm or kubernetes
- Add RBAC for docker / swarm management (services / nodes / containers etc)

## setup

- [install docker ee](docker-ee.md)
- install the ucp image: `docker image pull docker/ucp:3.1.5`
- access ucp via web browser
- upload docker ee license
- add worker nodes via the Add Node page (gives docker swarm or kubernetes command depending on orchestrator type)

example swarm command:

``` c#
docker swarm join --token 2341234123412342341234 <master node>
```

## securing ucp

### rbac

UCP offers RBAC to docker.

- `organization` group of users and teams
- `teams` a collection of users
- `user` a person who can authenticate with ucp

- `subject` a user team or organization that has the ability to do something
- `collection` a collection of cluster objects like nodes / containers / services
- `role` a permissiosn to to assigned to something to do something
- `grant` provides permission to a `role` for a `subject`

### managing certificates

You can deploy your own certificates for the UCP / DTR web ui instead of the self signed certs from install

- To upload your own certificates in UCP, go to admin, Admin Settings, then Certificates

### client bundles

allows you to manage and run UCP via the docker commandline with the proper authentication.

- UCP, go to admin, My Profile, Client Bundles

## sizing

### Minimum requirements

- 8GB of RAM for manager nodes
- 4GB of RAM for worker nodes
- 2 vCPUs for manager nodes
- 10GB of free disk space for the /var partition for manager nodes (A minimum of 6GB is recommended.)
- 500MB of free disk space for the /var partition for worker nodes

### Recommended production requirements

- 16GB of RAM for manager nodes
- 4 vCPUs for manager nodes
- 25-100GB of free disk space

## Backup restore

### backup

- run the backup ucp command (runs a container with a command to run a backup)

``` c#
docker container run \
  --log-driver none --rm \
  --interactive \
  --name ucp \
  -v /var/run/docker.sock:/var/run/docker.sock \
  docker/ucp:3.1.5 backup \
  --passphrase "secretsecret" \
  --id <Your UCP instance ID> > /home/cloud_user/ucp-backup.tar
```

### restore

- unstainll ucp from manager server

``` c#
docker container run --rm -it \
  -v /var/run/docker.sock:/var/run/docker.sock \
  --name ucp \
  docker/ucp:3.1.5 uninstall-ucp --interactive
```

- restore from backup

``` c#
docker container run --rm -i --name ucp \
  -v /var/run/docker.sock:/var/run/docker.sock  \
  docker/ucp:3.1.5 restore --passphrase "secretsecret" < /home/cloud_user/ucp-backup.tar
```
