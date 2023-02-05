# Kubernetes with Multiple Paths Express

This repo is all about routing two or more services in Kubernetes cluster by different path. There are two Docker containers deployed in the cluster. Each containers can be access thru different paths, /foo and /bar. Both containers running an image of Express server. 

To create the Docker image, you can refer my [k8s-basic-express](https://github.com/farhannafis/k8s-basic-express) repo. In this repo we will jump into Kubernetes cluster setup.

## Create Kubernetes Cluster

### Enable Ingress in Minikube

```bash
minikube addons enable ingress
```

### Verify NGINX Ingress controller is running

```bash
kubectl get pods -n ingress-nginx
```

The output is similar to

```
NAME                                        READY   STATUS      RESTARTS    AGE
ingress-nginx-admission-create-g9g49        0/1     Completed   0          11m
ingress-nginx-admission-patch-rqp78         0/1     Completed   1          11m
ingress-nginx-controller-59b45fb494-26npt   1/1     Running     0          11m
```

### Add Service definition into the cluster

``bash
kubectl apply -f kube/foo.yaml
kubectl apply -f kube/bar.yaml
```

### Add Ingress definition into the cluster

```bash
kubectl apply -f kube/ingress.yaml
```

### Verify the Ingress service

```bash
kubectl get service ingress-nginx-controller -n ingress-nginx
```

### Run Ingress using Minikube

```bash
minikube service ingress-nginx-controller -n ingress-nginx
```

## References

1. https://matthewpalmer.net/kubernetes-app-developer/articles/kubernetes-ingress-guide-nginx-example.html
2. https://kubernetes.github.io/ingress-nginx/deploy/
3. https://github.com/kubernetes/minikube/issues/13872
4. https://patroware.medium.com/how-to-direct-different-urls-to-different-services-in-kubernetes-646438ece73a
5. https://kubernetes.io/docs/concepts/services-networking/ingress/
6. https://kubernetes.io/docs/tasks/access-application-cluster/ingress-minikube/
7. https://spacelift.io/blog/kubernetes-ingress