
## Pods
- Basic unit in kubernetes
- Can contain one or more containers exposed by a single IP address
- Kubernetes manage pods not containers themselves

Create a simple pod running an image <br>
`kubectl run <NAME> --image=<IMAGE>`

Get pods <br>
`kubectl get pods [-o yaml] [-o wide]`

Inspect Pods <br>
`kubectl describe pod <POD_NAME>`

Open a shell in a pod <br>
`kubectl exec -it <POD NAME> -- [sh|/bin/bash]`
- To see running processes you can cd into /proc or use `ps` command if available
- Use `exit` to exit 

See Logs | Troubleshooting
- The entry point app doesn't connect to STDOUT
- Logs sent to kubernetes cluster
`kubect logs`
`kubectl describe`
- Check exit status
- CrashLoopBackoff: The app is crashing and kubernetes is representing a restart loop that is happening in a Pod.

### YAML files

To get help about properties <br>
`kubectl explain` <br>
Eg: `kubectl explain pods.spec`

1. apiVersion
2. Kind: Kind of object (Pods, Deployment)
3. metadata
4. spec: Specifications of the object

Container Specs
1. name
2. image
3. command
4. args
5. env

Create|delete|replace pod with yaml files<br>
`kubectl create -f <FILE.yaml>` // This throws an error if already exists <br>
`kubectl apply -f <FILE.yaml>` // This updates if already exists

Delete|Replace pod with yaml<br>
`kubectl delete|replace -f <FILE.yaml>`

Port Forward to access a Pod from your host computer <br>
`kubectl port-forward <POD NAME> 8080:80 &`
- Usually runs in forground. Adding `&` makes it run in background
- Use `fg` to bring it to foreground again

### Generate YAML Files
- These fit into the DevOps practices as you can commit the YAML files to your git repos
- DO NOT write YAML files. Always generate them. As you can make mistakes while writing <br>
`kubectl run buybox --image=busybox --dry-run=client -o yaml -- sleep 3600 > myfile.yaml` 

### Multi container Pods
- One container per Pod is a standard as it is easier to manage them
- To update one you'll have to bring both down
- Datasharing happens through a shared volume

1. Sidecar Container: Container used to enhance the primary app by adding looging for eg. (istio service mesh)
2. Ambassador Container: Container that represents the primnary container to the outside worlk such as a proxy (used for authorization)
3. Adapter Container: Container that matches/transforms the data pattern to other apllications in the cluster
4. Init Contianer: This is a container that runs or fetches something before the main container gets executed.
            - The main container won't run until the init containers are done executing


### Namespaces
- RBAC
- Security
- Resource Quotas

Create/See a namespace <br>
`kubectl create namespace <NAMESPACE NAME>` <br>
`kubectl describe ns <NAMESPACE NAME>`


