
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

### SecurityContext
- Lets you configure important security related parameters like 
            1. Run as root
            2. Run as user xxxx
            3. Disable privilege escalation (sudo)
- Available under pods.spec.SecurityContext and pods.spec.containers.SecurityContext

## Jobs

- Pods are meant to be kept around forever
- If you want them to be deleted after completion use Jobs instead
- Use spec.ttlaftercompletion to cleanup the jobs after finished

3 Types of Jobs <br>
1. Non-Parallel;  completion=1, parallelism=1
2. Parallel Jobs with fixed completion count; completion=n, parallelism=m
3. Parallel jobs with a work queue; completion=1, parallelism=m: Completed when one of the pods is completed

Run a Job <br>
`kubectl create job <JOB_NAME> --image=<IMG_NAME> -- <CMDs>`

Delete a Job <br>
`kubectl delete job <JOB_NAME>`
            
Get Jobs
`kubectl get jobs`

- job.spec.ttlSecondsAfterFinished: This specifies after how long after completion the job should be deleted. The default is forever.


## Cron Jobs
- jobs run on a schedule

Create Cron Job<br>
`kubectl create cronjob <JOB_NAME> --image=<IMAGE> --schedule="*/ * * * *"`
<br>.<br>
![image](https://user-images.githubusercontent.com/54491362/204773811-4ada8b08-fd29-4902-8eda-ee3944bd74ca.png)
![image](https://user-images.githubusercontent.com/54491362/204774499-7e8fd2db-3ca7-4701-9494-6a658c18dedf.png)

Delete Cron Jobs with the associated Jobs and Pods <br>
`kubectl delete cronjob <CRON_JOB_NAME>`


## Resource Limitations

- Putting resource limitations on containers: CPU(mcpus), Memory(MBs)
    - Request: The resources that have to be alloted at startup to the container
    - Limit: The maximum amount of resources the container can use.

- Can also apply quotas on namespaces
- Set it in <i> pods.spec.containers.resources </i>
- If the request is too high to satisfy, the deployment will be kept on <i> Pending </i> state until the resources are avb
- if the request is too low for the app and the oom killer will kick in and the tatus will be: OOMKILLED (Out of memory Killed)

## Cleaning up Resources

- Periodic cleanup using cronjobs might help

Delete all resources from all names<br>
`kubectl delete all --all`

Delete all without waiting for the resources to be deleted
`kubectl delete all --all --force --grace-period=-1`
