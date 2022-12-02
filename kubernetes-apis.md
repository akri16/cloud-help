## Kubernetes APIs

- APIs -> Core APIs that are extensible
- Custom Resource Definition (CRD)

`kubectl api-resorces`
`kubectl api-versions`
`kubectl version`

- kube-server is a daemon process on the server side that accepts secure requests only
- kube-proxy to make secure request using curl (not ssl by default)
- kube-proxy runs on your workstation and proxies your request to the server and uses the TLS certificates in the KUBE_CONFIG

Run kube-proxy <br>
`kubectl proxy --port=<PNO>`
`curl localhost:<PNO>`

- Api versions can be deprecated. Deprecated versions are supported for next 2 revisions
`kubectl explain --recursive deploy`

- Authentication
- Authorization
- Service Accounts
- RBAC
  - Role
  - User/Service Account
  - Role Mapping

Can I do something <br>
kubectl auth can-i [get pods]

- All pods have a default service account that they can use only to get information from the kubernetes API-Server: `default` service-account
- Service Accounts have secrets

Show a service account <br>
`kubectl get sa default -o yaml`

- Custom service accounts can be created
- You have to create role, service account, bind them together with a rolebinding 
- Once bound the secret for the service account are made avb in the pods at `/run/secrets/kubernetes.io/serviceaccount/token`

Set a service account to a deploy <br>
`kubectl set sa deploy <depname> <saname>`

Create a service account <br>
`kubectl create sa <saname>`
