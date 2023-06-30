## Overview
This document describes how to use Kubernetes APIs to perform operations in Tencent Kubernetes Engine (TKE) clusters. For example, you can use the APIs to view all namespaces in a cluster, view all pods in a specified namespace, and add, delete, or query a pod in the specified namespace.

## Directions

### Obtaining the kubeconfig cluster access credential
1. Log in to the cluster node by referring to [Log into Linux Instance Using Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436).
2. Run the following command to obtain the location of the cluster access credential (kubeconfig) file:
```
ps -ef |grep kubelet|grep -v grep
```
The following figure shows the output of the command, where the location of the access credential file is `/etc/kubernetes/kubelet-kubeconfig`.
![](https://main.qcloudimg.com/raw/0dd677da751b8caf8501168c945ed760.png)
3. Run the following command to go to the `kubernetes` directory:
```
cd /etc/kubernetes
```
4. Run the following commands in sequence to obtain the CA, key, and apiserver information from the `kubeconfig` file, respectively:
```
cat  ./kubelet-kubeconfig |grep client-certificate-data | awk -F ' ' '{print $2}' |base64 -d > client-cert.pem
```
```
cat  ./kubelet-kubeconfig |grep client-key-data | awk -F ' ' '{print $2}' |base64 -d > client-key.pem
```
```
APISERVER=`cat  ./kubelet-kubeconfig |grep server | awk -F ' ' '{print $2}'`
```
Run the `ls` command. Then, you can find the generated `client-cert.pem` and `client-key.pem` files in the kubernetes directory, as shown in the following figure:
![](https://main.qcloudimg.com/raw/8d0741a5db89999eb23a757c6a3dda46.png)


### Calling Kubernetes APIs by using CURL commands
1. Run the following command to view all namespaces in the current cluster:
```
curl --cert client-cert.pem --key client-key.pem -k $APISERVER/api/v1/namespaces
```
>? If an error stating insufficient permissions occurs when you run the `curl` command, you can resolve the error by referring to [Granting cluster permissions](#Authority).
>
2. Run the following command to view all pods in the kube-system namespace:
```
curl --cert client-cert.pem --key client-key.pem -k $APISERVER/api/v1/namespaces/kube-system/pods
```



### Managing pod lifecycles
>? The files created in the following steps and their content are for demonstration purposes only. You can customize them based on your actual requirements.


#### Creating a pod in the JSON format
1. Run the following command to create and open a JSON file:
```
vim nginx-pod.json
```
2. Copy the following content into the JSON file:
```
     {
         "apiVersion":"v1",
         "kind":"Pod",
         "metadata":{
             "name":"nginx",
             "namespace": "default"
         },
         "spec":{
             "containers":[
                 {
                     "name":"nginx-test",
                     "image":"nginx",
                     "ports":[
                         {
                             "containerPort": 80
                         }
                     ]
                 }
             ]
         }
     }
```
3. Run the following command to create a pod:
```
curl --cert client-cert.pem --key client-key.pem -k $APISERVER/api/v1/namespaces/default/pods -X POST --header 'content-type: application/json' -d@nginx-pod.json
```

#### Creating a pod in the YAML format
1. Run the following command to create and open a YAML file:
```
vim nginx-pod.json
```
2. Copy the following content into the YAML file:
```
     apiVersion: v1
     kind: Pod
     metadata:
       name: nginx
       namespace: default
     spec:
       containers:
       - name: nginx-test
         image: nginx
         ports:
         - containerPort: 80
```
3. Run the following command to create a pod:
```
curl --cert client-cert.pem --key client-key.pem -k $APISERVER/api/v1/namespaces/default/pods -X POST --header 'content-type: application/yaml' --data-binary @nginx-pod.yaml
```



#### Querying the status of a pod
Run the following command to query the status of a pod:
```
curl --cert client-cert.pem --key client-key.pem -k $APISERVER/api/v1/namespaces/default/pods/nginx
```

#### Querying the logs of a pod
Run the following command to query the logs of a pod:
```
curl --cert client-cert.pem --key client-key.pem -k $APISERVER/api/v1/namespaces/default/pods/nginx/log
```

#### Querying the metrics of a pod
Run the following command to query the metrics of a pod through the metric-server API:
```
curl --cert client-cert.pem --key client-key.pem -k $APISERVER/apis/metrics.k8s.io/v1beta1/namespaces/default/pods/nginx
```

#### Deleting a pod
Run the following command to delete a pod:
```
curl --cert client-cert.pem --key client-key.pem -k $APISERVER/api/v1/namespaces/default/pods/nginx -X DELETE
```


## Relevant Operations
<span id="Authority"></span>
### Granting cluster permissions
If the following error occurs when you run the `curl` command, you must grant cluster [access permissions](https://kubernetes.io/zh/docs/reference/access-authn-authz/rbac/).
![](https://main.qcloudimg.com/raw/c50eca5e28b0cdbb4cf00a378a773205.png)
You can perform authorization by using the following two methods:
- Method 1 (recommended): perform RBAC authorization in the TKE console. For more information, see [Authorizing by using preset identities](https://intl.cloud.tencent.com/document/product/457/37368) and [Authorizing by using custom policies](https://intl.cloud.tencent.com/document/product/457/37369).
- Method 2: Run the following command to perform authorization. We recommend that you not grant an account the cluster-admin permissions in a production cluster.

```
kubectl create clusterrolebinding cluster-system-anonymous --clusterrole=cluster-admin --user=system:anonymous
```

