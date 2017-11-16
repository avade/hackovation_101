Getting started with Kubernetes
=========
Kubernetes is an open-source system for automating deployment, scaling, and management of containerized applications
 
## How to connect
In order to connect to the k8s API Server use the following endpoint: https://api.k8s.hackovation.io
More information on Kubernetes API: https://kubernetes.io/docs/api-reference/v1.7
Kubectl tool: https://kubernetes.io/docs/user-guide/kubectl/v1.7/

#### Example:
###### using curl
>NAMESPACE=team-1
> TOKEN=<token>
> curl -kD - -H "Authorization: Bearer $TOKEN" https://api.k8s.hackovation.io/api/v1/namespaces/$NAMESPACE/
  
###### using kubectl
> NAMESPACE=team-1
> TOKEN=<token>

`kubeconfig`
```
apiVersion: v1
clusters:
- cluster:
    insecure-skip-tls-verify: true
    server: https://api.k8s.hackovation.io
  name: k8s.hackovation.io
contexts:
- context:
    cluster: k8s.hackovation.io
    user: $NAMESPACE
  name: k8s.hackovation.io
current-context: k8s.hackovation.io
kind: Config
preferences: {}
users:
- name: $NAMESPACE
  user:
    token: $TOKEN
```

```
> export KUBECONFIG="$(pwd)/kubeconfig"
> kubectl config view
> kubectl config use-context k8s.hackovation.io
> kubectl get all -n $namespace
```
  
## Demo App
--TODO

