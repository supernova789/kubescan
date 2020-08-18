Welcome! This guide will walk you through installing Kube-Scan into your Kubernetes cluster.

### Quickstart - For Local Setup

```
kubectl apply -f kube-scan.yaml
kubectl port-forward --namespace kube-scan svc/kube-scan-ui 8080:80
```

Then set your browser to http://localhost:8080


### Using a load-balancer service - Using Cloud Provider

This method assumes you are using a cloud provider that provides load balancers.

```
kubectl apply -f kube-scan-lb.yaml
```

Then get the load-balancer address by

```
kubectl -n kube-scan get service kube-scan-ui -o jsonpath={..ip}
```

or

```
kubectl -n kube-scan get service kube-scan-ui -o jsonpath={..hostname}
```

or

```
kubectl describe svc kube-scan-ui -n kube-scan
```

Depending on the load-balancer type, navigate your browser to the LoadBalancer address.



### Using the API

If you applied kube-scan to your cluster with the load balancer service:

"HOST" refers to the external ip of the service.

If you used port-forward:

"HOST" refers to "localhost:8080"

Getting all of the risks in your cluster:


```
GET http://HOST/api/risks
```

Requesting the kube-scan service to calculate again the risks (in case a resource was changed):


```
POST http://HOST/api/refresh
```

This might be a long operation - depending on the cluster size, so you can pull the refresh operation status:


```
GET http://HOST/api/refreshing_status
```


### Uninstall


```
kubectl delete -f kube-scan.yaml
```

In case of using a load-balancer:


```
kubectl delete -f kube-scan-lb.yaml
```
