## Helm Charts
- Package Manager for Kubernetes
- Helm has:
1. Helm local tool: CLI (Has to be installed)
2. Helm Charts: Packages available in remote/local repos

Add a repository<br>
`helm add <repo-name> <repo-url>`

Install a package<br>
`helm install <name> <repo-name>/<pkg-name>`

See installed packages <br>
`helm list`

See status of an app
`helm status <app-name>`

 - A Helm Charts contains templates to which values are applied
 - Values are stored in values.yaml file: Configurations
 
 See the values of a package <br>
 `helm show values <repo>/<chart>`
 
 Change config and deploy<br>
 - `helm pull <repo>/<chart>` 
 - `tar xvf <tarfile>` 
 - Edit `<folder>/values.yaml`
 - `helm install -f <path-to-values.yaml> <app-name> <path-to-folder>`
 
 Uninstall a Helm package <br>
 `helm uninstall <name>`
 
 
