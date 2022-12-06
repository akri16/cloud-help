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
2. Recreate: Has downtime

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

## Deployment History
- MaxSurge: Max num of pods during an update to satisfy the minimum requirements
- MaxUnavailable: Max num of pods taken down at a time during an update
- These can be percentages or hard nos

See the history <br>
`kubectl rollout history deploy [<depname>] [--revision=<revision-no>]`

Describe a rollout <br>
`kubectl describe deployments.apps <depname>`

Rollback a deployment
`kubectl rollout undo deployment <depname> --to-revision=<revision_history>`

- Change to the replicas won't get added to the history


## DaemonSets
- Runs a pod with the app on every node on the cluster

Show the Daemons ets <br>
`kubectl get ds`

## Horizontal Pod Autoscaler
- Uses the Metrics Server

`kubectl -n workloaddb autoscale deployment <DEP_NAME> --cpu-percent=50  --min=1 --max=10`
