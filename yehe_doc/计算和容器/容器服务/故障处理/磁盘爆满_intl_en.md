This article describes the causes of the TKE cluster disk full issue. It also provides instructions on how to troubleshoot and solve this issue.

## Possible Causes
kubelet uses gc and the eviction mechanism, along with parameters such as `--image-gc-high-threshold`, `--image-gc-low-threshold`, `--eviction-hard`, `--eviction-soft`, and `--eviction-minimum-reclaim`, to control and implement disk space reclamation. If not properly configured or if a non-Kubernetes process continues to write data to the disk, the disk will run out of space.

A full disk impacts the operation of Kubernetes, specifically two of its major components: kubelet and container runtime. Refer to the following instructions for troubleshooting:
1. Run `df` to check for kubelet and container runtime directories on the disk in question. 
2. Use the results as a starting point for further troubleshooting.
 - [Container runtime directory is on a full disk](#ContainerRuntime)
 - [kubelet directory is on a full disk](#Kubelet)


## Troubleshooting
### Container runtime directory is on a full disk<span id="ContainerRuntime"></span>

If the container runtime directory is on a full disk, it may lead to a non-responsive container runtime. For example, if you are using dockerd, docker commands will hang and kubelet logs will show “PLEG unhealthy”. CRI will then invoke timeout which leads to container creation or termination failures. In this case, the user will see that the Pod remains in the ContainerCreating or Terminating status.

#### Default Docker directories
* `/var/run/docker`: used to store container runtime statuses. You can use dockerd `–exec-root` to specify a different directory.
* `/var/lib/docker`: used to store persistent container data, such as container images, container writable layer data, container standard log output, and volumes created through Docker.

#### Pod launch process
The following is a sample Pod launch process:
``` yaml
Warning  FailedCreatePodSandBox 53m kubelet, 172.22.0.44  Failed create pod sandbox: rpc error: code = DeadlineExceeded desc = context deadline exceeded
```

``` yaml
Warning  FailedCreatePodSandBox  2m (x4307 over 16h)  kubelet, 10.179.80.31  (combined from similar events): Failed create pod sandbox: rpc error: code = Unknown desc = failed to create a sandbox for pod "apigateway-6dc48bf8b6-l8xrw": Error response from daemon: mkdir  /var/lib/docker/aufs/mnt/1f09d6c1c9f24e8daaea5bf33a4230de7dbc758e3b22785e8ee21e3e3d921214-init: no space left on device
```
``` bash
  Warning  Failed   5m1s (x3397 over 17h)  kubelet, ip-10-0-151-35.us-west-2.compute.internal  (combined from similar events): Error: container create failed: container_linux.go:336: starting container process caused "process_linux.go:399: container init caused \"rootfs_linux.go:58: mounting \\\"/sys\\\" to rootfs \\\"/var/lib/dockerd/storage/overlay/051e985771cc69f3f699895a1dada9ef6483e912b46a99e004af7bb4852183eb/merged\\\" at \\\"/var/lib/dockerd/storage/overlay/051e985771cc69f3f699895a1dada9ef6483e912b46a99e004af7bb4852183eb/merged/sys\\\" caused \\\"no space left on device\\\"\""
```

#### Pod deletion process
The following is a sample Pod deletion process:
``` bash
Normal  Killing  39s (x735 over 15h)  kubelet, 10.179.80.31  Killing container with id docker://apigateway:Need to kill Pod
```

### kubelet directory is on a full disk<span id="Kubelet"></span>

#### Default kubelet directories
`/var/lib/kubelet`: used to store plugin information, Pod statuses, and mounted volumes, such as `emptyDir`, `ConfigMap`, and `Secret`. You can use kubelet `--root-dir` to specify a different directory.

#### Pod creation process
If the kubetlet directory is on a full disk (usually the system disk), the Pod creation process stops at mkdir, which means Sandbox cannot be created. The following is a sample Pod creation process:

``` yaml
  Warning  UnexpectedAdmissionError  44m kubelet, 172.22.0.44  Update plugin resources failed due to failed to write checkpoint file "kubelet_internal_checkpoint": write /var/lib/kubelet/device-plugins/.728425055: no space left on device, which is unexpected.
```

## Directions

If you use dockerd as the container runtime, a full disk causes dockerd to be unresponsive and hang when you try to stop it, which means you can’t restart dockerd to release storage space. In this case, you need to perform a manual cleanup to free up enough space for dockerd to restart. The procedure is as follows:

1. Manually delete some of the log files or files on the writable layer, as shown below:
``` bash
$ cd /var/lib/docker/containers
$ du -sh * # Find a directory that occupies a lot of space.
$ cd dda02c9a7491fa797ab730c1568ba06cba74cecd4e4a82e9d90d00fa11de743c
$ cat /dev/null > dda02c9a7491fa797ab730c1568ba06cba74cecd4e4a82e9d90d00fa11de743c-json.log.9 # Delete log files.
```
>
>- We recommend that you use `cat /dev/null >` to delete files rather than `rm`. Files deleted using `rm` are not released by docker processes and therefore the space they occupy is not released.
>- the larger the suffix number, the older the log file. We recommend that you delete older log files first.
2. Run the following command to mark the node as unschedulable and evict existing Pods to other nodes:
``` bash
kubectl drain <node-name>
```
This ensures that the containers in the Pod of the original node are deleted, as well as their logs (standard output) and container data (unmounted volumes and writable layer). 
3. Run the following command to restart dockerd:
``` bash
systemctl restart dockerd
# or systemctl restart docker
```
4. After dockerd is restarted and the Pod is scheduled to another node, find the cause for the full disk, perform a data cleanup, and take prevention measures.
5. Run the following command to remove the unschedulable mark from the node:
``` bash
kubectl uncordon <node-name>
```

## How to Prevent Disks from Filling Up
Make sure kubelet gc and eviction parameters are properly configured. Once you have done that, even if the disk becomes full, the Pods on the problematic node can be evicted automatically to other nodes, which prevents them from remaining in the ContainerCreating or Terminating status.
