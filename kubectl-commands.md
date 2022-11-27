
## Pods
- Basic unit in kubernetes
- Can contain one or more containers exposed by a single IP address
- Kubernetes manage pods not containers themselves

Create a simple pod running an image <br>
`kubectl run <NAME> --image=<IMAGE>`

Get pods <br>
`kubectl get pods [-o yaml]`

### YAML files

To get help about properties <br>
`kubectl explain`

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

### Generate YAML Files
- These fit into the DevOps practices as you can commit the YAML files to your git repos
- DO NOT write YAML files. Always generate them. As you can make mistakes while writing
`kubectl run buybox --image=busybox --dry-run=client -o yaml -- sleep 3600 > myfile.yaml` 
