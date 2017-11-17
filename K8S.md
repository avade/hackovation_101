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

###### access the Kubernetes Dashboard per Namespace / Team
Admin Dashboard for team can be accessed as a proxy as follows

`Get the Kubernetes Dashboard URL by running:`
```
 export NS=team-1
 kubectl get pods -n $NS -l "app=kubernetes-dashboard,release=dashboard-$NS" -o jsonpath="{.items[0].metadata.name}"
 export POD_NAME=$(kubectl get pods -n $NS -l "app=kubernetes-dashboard,release=dashboard-$NS" -o jsonpath="{.items[0].metadata.name}")
 echo http://127.0.0.1:9090/#!/deployment?namespace=$NS
 kubectl -n $NS port-forward $POD_NAME 9090:9090
 in Browser, replace the $NS
 http://127.0.0.1:9090/#!/deployment?namespace=$NS
```
  
## Demo App
--TODO

