This article describes the reasons that may cause a Pod to fail and enter the CrashLoopBackOff status and how to troubleshoot the issues. Refer to the following instructions to troubleshoot and solve these issues.

## Error Description

If a Pod’s status is `CrashLoopBackOff`, this means the Pod was launched but exited with exceptions. When this happens, unless the Pod’s [restartPolicy](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#restart-policy) is `Never`, the Pod will be restarted and the `RestartCounts` of the Pod will usually be greater than 0. In this case, first see [Using Exit Code to Troubleshoot Pod Exiting with Exceptions](https://intl.cloud.tencent.com/document/product/457/35758) for information on using the exit code to narrow down the range of possible problems. 

## Possible Causes
- Container process exited
- System OOM
- cgroup OOM
- Node memory fragmentation
- Health check failed

## Troubleshooting

### Making sure the containers are not killed

When a container exits, the exit code usually is between 0 and 128. The cause of the exception may be a bug or other reason.
Refer to [Container Exits](https://intl.cloud.tencent.com/document/product/457/35767) for more information on how to further troubleshoot such problems.

### Checking for system OOM
#### Analysis
If system OOM occurs, the exit code of the containers will be 137, indicating they exited due to the `SIGKILL` signal. The kernel will display the following error message:
```
Out of memory: Kill process ...
```
This can occur when other non-Kubernetes processes deployed on the node use too much memory, or not enough memory was assigned to kubelet using `--kube-reserved` and `--system-reserved`, leaving too little headroom for other non-container processes.
>? The total memory usage of all Pods on a node will not exceed the value of `cgroup` defined in `/sys/fs/cgroup/memory/kubepods` (`cgroup = capacity - "kube-reserved" - "system-reserved"`). In most cases, if memory is properly divided and the non-container processes (such as kubelet, dockerd, kube-proxy and sshd) on the same node do not use up the reserved memory, system OOM should not occur.

#### Solution
Adjust memory allocation according to your needs to avoid this issue.

### Checking for cgroup OOM
#### Error description
If the Pod exited due to cgroup OOM, the value of `Reason` under Pod events will be `OOMKilled`, indicating the actual usage of the container memory exceeded the limit. The kernel log will show the `Memory cgroup out of memory` error message.

#### Solution
Adjust limit according to your needs.

### Node memory fragmentation
If node memory is severely fragmented or lacks large page memory, requests for more memory will fail even though there is plenty of memory left. For instructions on troubleshooting and solutions, refer to [Memory Fragmentation](https://intl.cloud.tencent.com/document/product/457/35755). 

### Health check failures
For information on how to troubleshoot this issue, see [Health Check Failures](https://intl.cloud.tencent.com/document/product/457/35765).
