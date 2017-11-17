Getting started with Kubernetes
=========
Kubernetes is an open-source system for automating deployment, scaling, and management of containerized applications

## Requirements
Download and install the _kubectl_ utility for your plattform: https://kubernetes.io/docs/user-guide/kubectl/v1.7/

## Login credentials
In order to connect to the k8s API Server use the following endpoint: https://api.k8s.hackovation.io

We will provide you with the following credentials:
* `Username` - The username/namespace to use, e.g. _team-1_
* `Token` - The secret token used to authenticate, e.g. _eyJhbGciOiJSUzI1NiIs_

#### Setup your environment
```
export NAMESPACE=team-<team number>
export TOKEN=<token>
```
#### Connect using curl
Run curl:
```
curl -kD - -H "Authorization: Bearer $TOKEN" https://api.k8s.hackovation.io/api/v1/namespaces/$NAMESPACE/
```

#### Connect using kubectl
Create the following file in your working directory:

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

Configure _kubectl_
```
export KUBECONFIG="$(pwd)/kubeconfig"
kubectl config view
kubectl config use-context k8s.hackovation.io
```

List all resources:
```
kubectl get all -n $namespace
```

#### Access the Kubernetes Dashboard per Namespace / Team
Admin Dashboard for team can be accessed as a proxy as follows

Get the Kubernetes Dashboard URL by running:
```
kubectl get pods -n $NAMESPACE -l "app=kubernetes-dashboard,release=dashboard-$NAMESPACE" -o jsonpath="{.items[0].metadata.name}"
```

Set the _pod_ name:
```
export POD_NAME=$(kubectl get pods -n $NAMESPACE -l "app=kubernetes-dashboard,release=dashboard-$NAMESPACE" -o jsonpath="{.items[0].metadata.name}")

echo http://127.0.0.1:9090/#!/deployment?namespace=$NAMESPACE
```

Forward the Dashboard webserver to your local machine:
```
kubectl -n $NAMESPACE port-forward $POD_NAME 9090:9090
```

Now access the Dashboard in your Browser, replace the $NAMESPACE with the NAMESPACE from your environment (=team)
 http://127.0.0.1:9090/#!/deployment?namespace=$NAMEPSACE

## Demo App
--TODO

## Documentation
* Kubernetes API: https://kubernetes.io/docs/api-reference/v1.7
