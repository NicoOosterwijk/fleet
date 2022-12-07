# Multi-Cluster Kustomize Example

This example will deploy a GO-application using kustomize. 
The app will be deployed into the `go-app` namespace.

The application will be customized as follows per environment:

* speeltuin cluster: Using the AMD64 architecture image.
* raspberry-pi cluster: Using the ARM64 architecture image.

```yaml
kind: GitRepo
apiVersion: fleet.cattle.io/v1alpha1
metadata:
  name: go-app-multi-cluster
  namespace: fleet-default
spec:
  branch: main
  clientSecretName: gitrepo-auth-kb2mc
  repo: https://github.com/NicoOosterwijk/private-repo.git
  paths:
  - multi-cluster
  
  targets:
  - name: speeltuin
    clusterSelector:
      matchLabels:
        name: speeltuin
        
  - name: raspberry-pi
    clusterName: raspberry-pi
```