## Overview
Currently, Tencent Kubernetes Engine (TKE) does not support pod throttling, but the CNI plug-in can be modified to support this feature. This document explains how to limit the bandwidth on pods in TKE. You can do this if needed in your actual business scenario.


## Use Limits
- Currently, throttling is supported only in Global Router mode. After this mode is enabled, the HostPort feature is not supported. In this case, you can replace the feature with HostNetwork.
- Currently, the VPC-CNI mode is not supported.


## Directions
### Modifying the CNI plug-in
1. To log in to the node where a pod is located, refer to [Log into Linux Instance Using Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436).
2. Run the following command to query the `tke-cni-agent` version.
```
kubectl edit daemonset tke-cni-agent -n kube-system
```
If the `tke-cni-agent` version is earlier than v0.0.6, run the following command to replace the image.
```
ccr.ccs.tencentyun.com/tkeimages/tke-cni-agent:v0.0.7
```
3. Run the following command to query the `tke-bridge-agent` version.
```
kubectl edit daemonset tke-bridge-agent -n kube-system
```
If the version is not v0.0.5, run the following command to replace the image and add args `--port-mapping=false --bandwidth`.
```
ccr.ccs.tencentyun.com/tkeimages/tke-bridge-agent:v0.0.5
```


### Configuring annotations for pods
You can configure bandwidth limits by using the method provided by the community:
- Use the `kubernetes.io/ingress-bandwidth` annotation to specify the ingress bandwidth limit.
- Use the `kubernetes.io/egress-bandwidth` annotation to specify the egress bandwidth limit.
The following shows an example:
``` yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
      annotations:
        kubernetes.io/ingress-bandwidth: 10M
        kubernetes.io/egress-bandwidth: 20M
    spec:
      containers:
      - name: nginx
        image: nginx
```

## Configuration Verification
You can verify the configuration by using the following two methods:
- Log in to the node where the pod is located and run the following commands to check whether the limits have been successfully added.
``` bash
tc qdisc show
```
If a result similar to the following is returned, the limits have been added successfully.
```
 qdisc tbf 1: dev vethc09123a1 root refcnt 2 rate 10Mbit burst 256Mb lat 25.0ms
 qdisc ingress ffff: dev vethc09123a1 parent ffff:fff1 ----------------
 qdisc tbf 1: dev 6116 root refcnt 2 rate 20Mbit burst 256Mb lat 25.0ms
```
- Run the following commands to use iperf for testing.
``` bash
iperf -c <Service IP address> -p <Service port> -i 1
```
If a result similar to the following is returned, the limits have been added successfully.
```
 ------------------------------------------------------------
 Client connecting to 172.16.0.xxx, TCP port 80
 TCP window size: 12.0 MByte (default)
 ------------------------------------------------------------
 [  3] local 172.16.0.xxx port 41112 connected with 172.16.0.xx port 80
 [ ID] Interval           Transfer     Bandwidth
 [  3]  0.0- 1.0 sec   257 MBytes  2.16 Gbits/sec
 [  3]  1.0- 2.0 sec  1.18 MBytes  9.90 Mbits/sec
 [  3]  2.0- 3.0 sec  1.18 MBytes  9.90 Mbits/sec
 [  3]  3.0- 4.0 sec  1.18 MBytes  9.90 Mbits/sec
 [  3]  4.0- 5.0 sec  1.18 MBytes  9.90 Mbits/sec
 [  3]  5.0- 6.0 sec  1.12 MBytes  9.38 Mbits/sec
 [  3]  6.0- 7.0 sec  1.18 MBytes  9.90 Mbits/sec
 [  3]  7.0- 8.0 sec  1.18 MBytes  9.90 Mbits/sec
 [  3]  8.0- 9.0 sec  1.18 MBytes  9.90 Mbits/sec
 [  3]  9.0-10.0 sec  1.12 MBytes  9.38 Mbits/sec
 [  3]  0.0-10.3 sec   268 MBytes   218 Mbits/se
```

   
