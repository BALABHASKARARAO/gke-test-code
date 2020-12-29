* We create PVCs to claim PVs
```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: my-readonly-pv
spec:
  storageClassName: ""
  capacity:
    storage: 10Gi
  accessModes:
    - ReadOnlyMany
  claimRef:
    namespace: default
    name: my-readonly-pvc
  gcePersistentDisk:
    pdName: my-test-disk
    fsType: ext4
    readOnly: true
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-readonly-pvc
spec:
  # Specify "" as the storageClassName so it matches the PersistentVolume's StorageClass.
  # A nil storageClassName value uses the default StorageClass. For details, see
  # https://kubernetes.io/docs/concepts/storage/persistent-volumes/#class-1
  storageClassName: ""
  accessModes:
    - ReadOnlyMany
  resources:
    requests:
      storage: 10Gi
```
