This article describes the causes of health check failures and how to troubleshoot them. Refer to the following instructions to troubleshoot and solve these issues.


## Error Description
Kubernetes health checks include readiness checks (readinessProbe) and liveness checks (livenessProbe). Different health check failures have different symptoms:
* Pod IP addresses are removed from Service and traffic is not directed to the Pods that failed readiness check.
* kubelet stops a Pod and tries to restart it.

There are many reasons why health checks may fail. For example, the application may have a bug that prevents it from responding to health checks. If a Pod becomes `Unhealthy`, following these instructions to troubleshoot it:


## Possible Causes
- Improper health check configuration 
- Node overload
- Container process stopped by a trojan
- The listening port of a container internal process fails
- SYN backlog setting too low

## Troubleshooting
### Checking your health check configuration

An improper health check configuration may cause health checks to fail. For example, if `initialDelaySeconds` (the period of time to wait before probing a container for the first time after the container starts) is too low and a container is slow to start, this will cause the probe to start before the container finishes startup. If, at the same time `successThreshold` is set to 1, then the health check is performed once and stopped. As a result, the Pod is stuck in a loop where it is repeatedly stopped and restarted.

### Checking if the node is overloaded
High CPU usage (such as 100%) causes the process to be unable to send or receive packets, which leads to timeout and health check failures. See [High Workload](https://intl.cloud.tencent.com/document/product/457/35754) for more information on how to troubleshoot this issue.

### Checking if the container process was stopped by a trojan

See [Using Systemtap to Troubleshoot Pod Exceptions](https://intl.cloud.tencent.com/document/product/457/35757) for more information on how to troubleshoot this issue.

### Checking if the listening port of the container internal process stopped working
Use `netstat -tunlp` to check if the port is still listening. From the results we can conclude: if the port stops listening, health check probe requests are reset, as shown by the following:
```bash
20:15:17.890996 IP 172.16.2.1.38074 > 172.16.2.23.8888: Flags [S], seq 96880261, win 14600, options [mss 1424,nop,nop,sackOK,nop,wscale 7], length 0
20:15:17.891021 IP 172.16.2.23.8888 > 172.16.2.1.38074: Flags [R.], seq 0, ack 96880262, win 0, length 0
20:15:17.906744 IP 10.0.0.16.54132 > 172.16.2.23.8888: Flags [S], seq 1207014342, win 14600, options [mss 1424,nop,nop,sackOK,nop,wscale 7], length 0
20:15:17.906766 IP 172.16.2.23.8888 > 10.0.0.16.54132: Flags [R.], seq 0, ack 1207014343, win 0, length 0
```
As shown above, health check probe request exceptions lead to health check failure. Possible causes are:
If a node has multiple Pods that use `hostNetwork` to listen on the same host port, only one Pod will be able to listen while the other Pods will fail to listen but do not exit. That means they will all be probed by health checks and all Pods but one will fail the health check.

### Checking if SYN backlog value is too low
#### Error description
The value of SYN backlog is the size of the SYN queue. If this value is set too low and many new connection requests are received in a short time, the majority of the requests will fail. You can use `netstat -s | grep TCPBacklogDrop` to get the number of failed requests.

#### Solution
Once you are sure the requests failed due to the value of SYN backlog, increase the value. The kernel parameter to use is `net.ipv4.tcp_max_syn_backlog`.
