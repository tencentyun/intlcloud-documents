## Overview
This document describes how to restrict the Pod bandwidth in TKE. Currently, TKE does not support Pod speed restriction; however, you can modify the CNI plugin to achieve it based on your actual scenario.

## Notes
- TKE supports using the bandwidth plugin of the community to restrict the network speed. Currently, it can be used in GlobalRouter mode and VPC-CNI shared ENI mode.
- Currently, it is not supported for the VPC-CNI dedicated ENI mode.

## Directions
### Modifying CNI plugin
#### GlobalRouter mode
The GlobalRouter network mode is a routing policy for communication between the container network and VPC based on the global routing capabilities of the underlying VPC. It is suitable for common scenarios and seamlessly compatible with standard Kubernetes features. For more information, see [GlobalRouter Mode](https://intl.cloud.tencent.com/document/product/457/38968).
1. Log in to the Pod node as instructed in [Logging in to Linux Instance Using Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436).
2. Run the following command to view the configuration of `tke-bridge-agent`:
```
kubectl edit daemonset tke-bridge-agent -n kube-system
```
Add args ` --bandwidth` to enable the support for the bandwidth plugin.

#### VPC-CNI shared ENI mode
The VPC-CNI mode is container network capability implemented based on CNI and VPC ENI and is suitable for scenarios with high requirements for latency.   
The open-source bandwidth plugin supports traffic shaping at the Pod entry and exit as well as bandwidth control. For more information, see [VPC-CNI Mode](https://intl.cloud.tencent.com/document/product/457/38970).
1. Log in to the Pod node as instructed in [Logging in to Linux Instance Using Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436).
2. Run the following command to view the configuration of `tke-eni-agent`:
```
kubectl edit daemonset tke-eni-agent -n kube-system
```
Add args ` --bandwidth` to enable the support for the bandwidth plugin.  
>? You can enable this feature simply by adding the above parameters to `tke-eni-agent` and disable it by removing the parameters. Deployment, enablement, and disablement are supported, which take effect only for new Pods.

### Specifying annotation in Pod
You can configure in the method provided by the community:
- Use the `kubernetes.io/ingress-bandwidth` annotation to specify the inbound bandwidth cap.
- Use the `kubernetes.io/egress-bandwidth` annotation to specify the outbound bandwidth cap.

Sample:
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
You can verify whether the configuration succeeds in the following two methods:
- **Method 1:** log in to the Pod node and run the following command to check whether the caps have been added:
``` bash
tc qdisc show
```
If a result similar to the following is returned, the caps have been added successfully:
```
 qdisc tbf 1: dev vethc09123a1 root refcnt 2 rate 10Mbit burst 256Mb lat 25.0ms
 qdisc ingress ffff: dev vethc09123a1 parent ffff:fff1 ----------------
 qdisc tbf 1: dev 6116 root refcnt 2 rate 20Mbit burst 256Mb lat 25.0ms
```
- **Method 2:** run the following command to use iperf for testing:
```  bash
iperf -c <service IP> -p <service port> -i 1
```
If a result similar to the following is returned, the caps have been added successfully:
```
 ------------------------------------------------------------
 Client connecting to 172.16.0.xxx, TCP port 80
 TCP window size: 12.0 MByte (default)
 ------------------------------------------------------------
 [  3] local 172.16.0.xxx port 41112 connected with 172.16.0.xx port 80
 [ ID] Interval       Transfer     Bandwidth
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
