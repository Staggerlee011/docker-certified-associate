# Docker Swarm Security

## Docker MTLS

Mutually Authenticated Transport Layer Security  

Allows docker swarm to encrypt traffic between all swarm nodes (master and worker nodes).  

- MTLS is enabled by default!
- CA for network communications is set up during swarm `init`

## --opt encrypted

To enable a encrypted network, when creating a swarm networking add the `--opt encrypted`. This means that all containers network traffic on this network would be encrypted

``` c#
docker netwwork create --opt encrypted --driver overlay my-secure-network
```
