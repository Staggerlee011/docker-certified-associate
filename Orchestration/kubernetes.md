# kubernetes

## get / labels

Get returns objects of a certain type (pods, deployments, configmaps etc).

You can filter on labels / selectors

``` c#
kubectl get pods -l environment=production,tier=frontend
kubectl get pods -l 'environment in (production),tier in (frontend)'
kubectl get pods -l 'environment in (production, qa)'
kubectl get pods -l 'environment,environment notin (frontend)'
```

`https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/`

## namespaces

Act as a logical seperator of applications. All commands can be filtered via namespaces.

``` c#
kubectl describe pods mypod-1231231 -n dos
kubectl get pods --all-namespaces
```

## deployments

Deployments consist of replicasets and pods.

``` c#

```

## services

An abstract way to expose pods. or link to external services. You could create a service for a RDS db, there for making the deployments the same for dev / stage / prod by just updating the connection string in the db service.

``` c#

```

## configMaps


``` c#

```

## secrets


``` c#

```


## troubleshooting

To troubleshoot a kubernetes deployment use the below commands:

### describe

``` c#
kubectl describe pods mypod-1231231 -n dos
```

### logs

``` c#
kubectl logs mypod-1231231 -n dos
```

### labels

use labels for filtering and management

``` c#
kubectl get pods --all-namespaces -label env=dev
```
