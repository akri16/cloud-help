## Deployment

- Scaling
- Right way of running applications
- Rolling Updates
- Automatic restart
- Replica Set (Managed resource: Managed directly by Deployments)

Create a deployment<br>
`kubectl create deploy <Deployment Name> --image=<Image Name> [--replicas=<No of replicas>]`

Scale a deployment <br>
`kubectl scale deploy <DEP_NAME> --replicas=<REPLICA_NO>`

See all Api-Version <br>
`kubectl api-versions`

See all Api-Resources <br>
`kubectl api-resources`

Edit a deployment<br>
- Cannot edit everything
- Can change replicas
`kubectl edit deploy <Deploy_Name>`

Get all the resources of a particular label<br>
`kubectl get all --selector app=<LABEL>`

### Updates
- The replica set is replaced with a new one. 
- There is version history that holds the past n(=10 by default) replicasets so that you can rollback 
1. Rolling Updates: No downtime
2. Replace: Has downtime

Set an update
`kubectl set image deploy <DEP_NAME> <OLD_IMAGE>=<NEW_IMAGE>`
