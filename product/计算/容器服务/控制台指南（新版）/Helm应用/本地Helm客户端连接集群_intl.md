## Operation Scenario

This document explains how to connect to a cluster using local Helm client.

## Steps

### Downloading the Helm Client

Run the following command to download the Helm client.
```
curl -O https://storage.googleapis.com/kubernetes-helm/helm-v2.10.0-linux-amd64.tar.gz
tar xzvf helm-v2.10.0-linux-amd64.tar.gz
sudo cp linux-amd64/helm /usr/local/bin/helm
```

### Configuring Helm as Client-only

Run the following command to configure Helm as Client-only.
```
helm init --client-only
```

### Connecting to a Cluster Using the Helm Client on a Private Network

#### Target Cluster Node

You can use it directly.

#### Non-target Cluster Node

1. Run the following command to change the type of the target cluster's Tiller service to private network loadbalancer mode.
>! Replace the value of "service.kubernetes.io/qcloud-loadbalancer-internal-subnetid" in the following command with the subnet ID of the required production CLB.
 
 ```
kubectl patch svc $(kubectl get svc -l app=helm,name=tiller -n kube-system -o=jsonpath={.items[0].metadata.name}) -n kube-system -p '{"metadata":{"annotations":{"service.kubernetes.io/qcloud-loadbalancer-internal-subnetid":"subnet-88888888"}},"spec":{"type":"LoadBalancer"}}'
```
2. Run the following command to get $EXTERNALIP on the target cluster node.
```
  kubectl get svc -l app=helm,name=tiller -n kube-system -o=jsonpath={.items[0].status.loadBalancer.ingress[0].ip}
```
3. Run the following command to get $PORT on the target cluster node.
```
kubectl get svc -l app=helm,name=tiller -n kube-system -o=jsonpath={.items[0].spec.ports[0].port}
```
4. Run the following command to import the environment variable on the Helm client node.
```
export HELM_HOST=$EXTERNALIP:$PORT
```
5. Run the following command to verify the Helm client.
```
[centos ~]# helm ls
NAME     	REVISION	UPDATED                 	STATUS  	CHART          	APP VERSION	NAMESPACE
wordpress	1       	Mon Jan 21 14:22:30 2019	DEPLOYED	wordpress-5.0.1	5.0.1      	default
```



