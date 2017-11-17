Getting started with Kubernetes
=========
Kubernetes is an open-source system for automating deployment, scaling, and management of containerized applications

## Requirements
Download and install the _kubectl_ utility for your platform:
* https://kubernetes.io/docs/tasks/tools/install-kubectl/

## Login credentials
In order to connect to the k8s API Server use the following endpoint: https://api.k8s.hackovation.io

We will provide you with the following credentials via VAULT:
* `Username` - The username/namespace to use, e.g. _team-1_
* `Token` - The secret token used to authenticate, e.g. _eyJhbGciOiJSUzI1NiIs_

#### Setup your environment
```
export NAMESPACE=team-<team number>
export TOKEN=<token>
alias kubectl="kubectl --namespace $NAMESPACE"
```
_Hint:_ If you omit the _alias_, you have to specify _--namespace_ for every _kubectl_ command.

#### Connect using curl
Run curl:
```
curl -kD - -H "Authorization: Bearer $TOKEN" https://api.k8s.hackovation.io/api/v1/namespaces/$NAMESPACE/
```

#### Connect using kubectl
Create the following file in your working directory:

`kubeconfig`
```
echo -n "
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
    token: $TOKEN" > kubeconfig
```

Configure _kubectl_
```
export KUBECONFIG="$(pwd)/kubeconfig"
kubectl config view
kubectl config use-context k8s.hackovation.io
```

List all resources:
```
kubectl get all
```

#### Access the Kubernetes Dashboard per Namespace / Team
Admin Dashboard for team can be accessed as a proxy as follows

Get the Kubernetes Dashboard URL by running:
```
export POD_NAME=$(kubectl get pods -n $NAMESPACE -l "app=kubernetes-dashboard,release=dashboard-$NAMESPACE" -o jsonpath="{.items[0].metadata.name}")
```

Forward the Dashboard webserver to your local machine:
```
kubectl -n $NAMESPACE port-forward $POD_NAME 9090:9090 &
```

Now access the Dashboard in your Browser, replace the $NAMESPACE with the NAMESPACE from your environment (=team), e.g.:

 http://127.0.0.1:9090/#!/deployment?namespace=team-4

## Example deployment
In the following example, you deploy a stateless application on your kubernetes namespace.

This is based largely on: https://kubernetes.io/docs/tasks/run-application/run-stateless-application-deployment/

#### Create the deployment YAML
```
echo -n "
apiVersion: apps/v1beta1 # for versions before 1.8.0 use apps/v1beta1
kind: Deployment
metadata:
  name: nginx-deployment
  namespace: $NAMESPACE
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 2 # tells deployment to run 2 pods matching the template
  template: # create pods using pod definition in this template
    metadata:
      # unlike pod-nginx.yaml, the name is not included in the meta data as a unique name is
      # generated from the deployment name
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.7.9
        ports:
        - containerPort: 80" > deployment.yaml
```

#### Deploy the service
```
kubectl apply -f deployment.yaml
```

#### View information about your Deployment
```
kubectl describe deployment nginx-deployment
```

#### View information about the created Pods
```
kubectl describe pods
```

#### Delete your deployment
```
kubectl delete -f deployment.yaml
```


## Documentation
* Kubectl User Guide: https://kubernetes.io/docs/user-guide/kubectl/v1.7/
* Kubernetes API: https://kubernetes.io/docs/api-reference/v1.7
