# kubernetes

## deployments

## services

## configMaps

## secrets

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
