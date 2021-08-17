## Operation Scenarios

The metrics-server can realize the Resource Metrics API (metrics.k8s.io) of Kubernetes. Through this API, you can query some monitoring metrics of Pods and Nodes. The monitoring metrics of Pods are used in [HPA](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/), [VPA](https://github.com/kubernetes/autoscaler/tree/master/vertical-pod-autoscaler), and `kubectl top pods` commands, whereas the Node metrics are currently used only in `kubectl top nodes` commands. TKE itself realizes the Resource Metrics API, pointed towards the hpa-metrics-server, and currently TKE also provides monitoring metrics for Pods.

After installing the metrics-server to the cluster, you can run `kubectl top nodes` to obtain the monitoring overview of nodes to replace the realization of the Resource Metrics API. HPA created on the TKE console does not use Resource Metrics and only uses Custom Metrics. Therefore, installing the metrics-server does not affect HPA created on the TKE console. This document describes how to install the metrics-server on TKE.



## Directions

### Downloading the YAML deployment file

Run the following commands to download the latest deployment file components.yaml of the metrics-server.

```bash
wget https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```

### Modifying the metrics-server launch parameter

The metrics-server requests the kubelet API of each node to obtain monitoring data. The API is exposed via HTTPS, but as TKE node kubelet uses a self-signed certificate, if the metrics-server directly requests the kubelet API, an error of certification verification failure will occur. Therefore, you need to add the `--kubelet-insecure-tls` launch parameter in the components.yaml file.
Moreover, as the official image repository of the metrics-server is stored in `k8s.gcr.io`, users in China may not be able to directly pull images from the repository. You need to manually synchronize images to CCR or use the synchronized image `ccr.ccs.tencentyun.com/mirrors/metrics-server:v0.4.0`.

Below is a sample of modification of the components.yaml file:

```yaml
containers:
- args:
  - --cert-dir=/tmp
  - --secure-port=4443 # Please replace with 4443
  - --kubelet-preferred-address-types=InternalIP,ExternalIP,Hostname
  - --kubelet-use-node-status-port
  - --kubelet-insecure-tls # Add this launch parameter
  image: ccr.ccs.tencentyun.com/mirrors/metrics-server:v0.4.0 # For cluster in the Chinese mainland, please replace with this image address
  ports:
  - containerPort: 4443  # Please replace with 4443
    name: https
    protocol: TCP
```

### Deploying the metrics-server

After modifying components.yaml, run the following commands to implement one-click deployment to the cluster via kubectl:

```bash
kubectl apply -f components.yaml
```

>? Through the above step, you can install and deploy the metrics-server. Alternatively, you can run the following commands for one-click installation of the metrics-server, but this method cannot ensure synchronization with the latest version.
```bash
kubectl apply -f https://raw.githubusercontent.com/TencentCloudContainerTeam/manifest/master/metrics-server/components.yaml
```

### Checking the running status

1. Run the following commands to check whether the metrics-server starts normally. Below is a sample:
```bash
$ kubectl get pod -n kube-system | grep metrics-server
metrics-server-f976cb7d-8hssz         1/1     Running   0          1m
```
2. Run the following commands to check the configuration file. Below is a sample:
```bash
$ kubectl get --raw /apis/metrics.k8s.io/v1beta1  | jq
{
  "kind": "APIResourceList",
  "apiVersion": "v1",
  "groupVersion": "metrics.k8s.io/v1beta1",
  "resources": [
    {
      "name": "nodes",
      "singularName": "",
      "namespaced": false,
      "kind": "NodeMetrics",
      "verbs": [
        "get",
        "list"
      ]
    },
    {
      "name": "pods",
      "singularName": "",
      "namespaced": true,
      "kind": "PodMetrics",
      "verbs": [
        "get",
        "list"
      ]
    }
  ]
}
```
3. Run the following commands to check the node usage performance. Below is a sample:
```bash
$ kubectl top nodes
NAME    CPU(cores)   CPU%   MEMORY(bytes)   MEMORY%
test1   1382m        35%    2943Mi          44%
test2   397m         10%    3316Mi          49%
test3   81m          8%     464Mi           77%
```
