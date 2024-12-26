# Kubernetes
Kubernetes stuff

## Configure alias
```bash
# Session alias
alias k=kubectl

# Terminal alias
alias k=/opt/homebrew/bin/kubectl

```

## Imperative commands

### Keys
`--dry-run` : By default as soon as the command is run, the resource will be created. If you simply want to test your command , use the --dry-run=client option. This will not create the resource, instead, tell you whether the resource can be created and if your command is right.

`-o yaml`: This will output the resource definition in YAML format on screen.

### Useful

Create a Pod
```bash
k create nginx --image=nginx

# add labels
k run redis --image=redis:alpine --labels="tier=db"

# change port
k run custom-nginx --image=nginx --port=8080

```

Create a Deployment

```bash
k create deployment nginx --image=nginx --replicas-2
```

Scale
```bash
# Deployment
k scale deployment nginx --replicas=3

# ReplicaSet
k scale replicaset nginx-rc --replicas=3
``

Generate a manifest
```bash
k create nginx --image=nginx --dry-run=client -o yaml
```

Create Services
```bash

k create service clusterip web-service --tcp=80:80 # assume labels app:web-service and doesn't support selectors from command line
k create service nodeport web-service --tcp=80:80 --node-port=30080

# Using expose
k expose pod nginx --port=80 --name web-service

# Expose based on deployment
k expose deployment nginx --port=80 --name web-service # assume app:nginx

# Expose NodePort service
k expose deployment nginx --port=80 --name web-svc --type=NodePort # can't specify the nodeport
```

Port-forward
```bash
k port-forward deployment/nginx 8080:80
```

Jobs
```bash
# create a Job which prints "Hello World"
kubectl create job hello --image=busybox:1.28 -- echo "Hello World"
```
### Specific kubectl

Config
```bash
# Show Merged kubeconfig settings.
kubectl config view
kubectl config view --raw

```



### References
* https://kubernetes.io/docs/reference/kubectl/
* https://kubernetes.io/docs/reference/kubectl/quick-reference/
