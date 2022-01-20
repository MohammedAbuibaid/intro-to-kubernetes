# Introduction to Kubernetes

This is my version of intro to K8s. The original repo is [here](https://github.com/SUSE-Rancher-Community/intro-to-kubernetes)

## Slide Deck

The slide deck for the `Introduction to Kubernetes` course can be found in the *slide-deck* folder.


## Before doing the below labs, you need to Create Local Kubernetes Cluster with K3d

k3d is a lightweight wrapper to run k3s (Rancher Lab’s minimal Kubernetes distribution) in docker.

![K3d Logo](k3d-logo.png)

### K3d Requirements/Prerequisites

- [Docker](https://docs.docker.com/engine/install/)
- [Install K3d](https://k3d.io/v4.4.8/#installation)

### Provision Cluster with K3d

The first step is to ensure that the docker engine is running on your machine. Once you've verified that, you can proceed to create a cluster with the following command:

``` bash
k3d cluster create example-cluster --servers 3 --agents 2
```


# Lab 01: Create a pod using manifest file

1.	Create the pod using the below command:
```
kubectl create -f pod.yaml
```

2.	To see if the pod is in the Running:
```
kubectl get pod
```
 
3. Display information about the running pod nginx
```
kubectl describe pods nginx
```


4. To confirm that the NGINX server is actually working
```
kubectl exec -it nginx -- /bin/bash
```

From within the container inspect the NGINX service
```
service nginx status
exit
```

5. CleanUp
```
kubectl delete -f pod.yaml
```

# Lab 02: Create a Deployment using manifest file

1.	Create the Deployment using the below command:
```
kubectl create -f deployment.yaml
```

2.	List the Deployment on the node:
```
kubectl get deployment
```

3. Scale up your deployment
```
kubectl scale deployment.v1.apps/nginx-deployment --replicas=10 
kubectl get pods
```
4. CleanUp
```
kubectl delete -f deployment.yaml
```

# Lab 03: 
1.	Create the NodePort service using the below command:
```
kubectl create -f np_service.yaml
```
 
2. Observe the results
```
kubectl get service
kubectl get svc
```
3. View all the details of the service by running the below command:
```
kubectl describe svc nginx-service
```

# Lab 04: Ingress
1.	Create the Ingress using the below command:
```
kubectl create -f ingress.yaml
```
 
2. Observe the results
```
kubectl get ingress 
```
3. List the host(provided in the ingress.yaml) under the hosts 
``` vim /etc/hosts
```

3. View all the details of the service by running the below command:
```
kubectl describe ingress
```

# Lab 05: ConfigMaps Secrets
```
kubectl create -f configmap.yaml,secret.yaml,env-pod.yaml
kubectl logs env-pod
```
