## Services
- An API resource used to expose a logical set of pods
- Rotes traffic to the pods of a replica set in a round robin fashion
- Kube-Controller-Manager continously scans for pods that match a selector and includes them in the service
- Services exist independently from  the applications they provide access to
- One Service can route to multiple deployments: Canary Deployments
- The kube-proxy agent working in the background on the nodes watches for new services and endpoints
- Types of service:
    1. NodePort: Exposes externally
    2. ClusterIP: Exposes internally
    3. LoadBalancer
- Ports while working with services:
    1. targetport: The port on the container/application that the service addresses
    2. port: The port on which the service is accessible
    3. nodeport: The port thats exposed on the node when using NodePort service type: generated automatically

- Endpoints: These are the pod IPs that a service keeps track of (Managed by the controller) to route traffic <br>
`kubectl get endpoints`

Create a service <br>
`kubectl expose deploy <DEPLOY_NAME> --port=<PORT>`

Edit a Service <br>
`kubectl edit svc <Service_Name>`

- KubeDNS allows you to access the services from withing the Cluster network by the service name. 
