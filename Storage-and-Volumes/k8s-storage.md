# kubernetes storage

`Storage Class -> PersistentVolume (PV) -> PersistentVolumeClaim (PVC)`

## Storage Class

- ebs (default for aws, azure and gcp have defaults to)
- efs
- etc

## PersistentVolume (PV)

A PersistentVolume (PV) is a piece of storage in the cluster that has been provisioned by an administrator or dynamically provisioned using Storage Classes

## PersistentVolumeClaim (PVC)

A PersistentVolumeClaim (PVC) is a request for storage by a user. It is similar to a Pod. Pods consume node resources and PVCs consume PV resources.
