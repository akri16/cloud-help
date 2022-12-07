- File storage in a container is ephemeral
- Use volume mounts that can point to any storage type outside the Pod

### PVCs and PVs
- PV: Persistent Volume
- PVC: Persistent Volume Claim
- StorageClass

- Storage type can be cluster specific, so to decouple this from the user, you can use PVCs 
- PVCs let you specify your storage needs and then finds the appropriate PV to match your needs
- If a PV can't be found, the StorageClass creates the PV for you
- Or, Admins can manually create PVs according to the PVCs, which won't be in accordance with DevOps
- PVs are exclusive, once a PVis bound by a PVC it cannot be bound by any other PVC
- PV Access Modes:
    1. ReadOnly
    2. ReadWriteOnce: Only by one pod
    3. ReadWriteMany: by multiple pods

### Local Site Specific Storage
- Use can configure the volumes in pods.spec.volumes and mount them in pod.spec.containers.volumeMounts
- For testing purposes you can use non-portable site-specific storage using `hostpath` and `emptydir`
