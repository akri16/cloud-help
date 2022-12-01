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

- Pod names in a Deployment: <deploy_name>-<replicaset_id>-<pod_id>

## Labels and Annotations
- Labels add metadata to resources
- Selectors can be used to select all resources with a label
- Labels are automatically added for deploy and services ('app=<App_NAME>')
- Labels are not inherited

Add a label to a deployment<br>
`kubectl label deployment <depname> <Label_Key>=<Label_Value>`

Select deployments with a label<br>
`kubectl get deployments --selector <Label_Key>=<Label_Value>`

Get Deployment with labels <br>
`kubectl get deploy <DEP_NAME> --show-labels`

- Annotations can be used for informational purposes (in older resource types) and for specifiying additional features (in newer resource types)

Remove a label <br>
`kubectl label <RES_TYPE> <RES_NAME> <KEY>-`


