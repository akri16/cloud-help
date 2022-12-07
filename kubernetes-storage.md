- File storage in a container is ephemeral
- Use volume mounts that can point to any storage type

### PVCs and PVs
- PV: Persistent Volume
- PVC: Persistent Volume Chain

- Storage type can be cluster specific, so to decouple this from the user, you can use PVCs 
- PVCs let you specify your storage needs and then finds the appropriate PV to match your needs
- If a PV can't be found, a StorageClass is created which in turn creates the PV for you
- Or, Admins can manually create PVs according to the PVCs, which won't be in accordance with DevOps
