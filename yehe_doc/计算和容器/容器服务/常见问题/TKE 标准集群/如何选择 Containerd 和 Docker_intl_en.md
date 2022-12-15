
## How to Choose Containerd and Docker

### How do I select a runtime component?

As one of the most important components of Kubernetes (K8s), a container runtime manages the lifecycle of images and containers. Kubelet interacts with the containerd through the `Container Runtime Interface (CRI)` to manage images and containers.

You can choose Containerd and Docker as container runtime components:
- (Recommended) Containerd has a shorter calling chain and fewer components, and features higher stability and lower node resource consumption.
- Docker should be used as the runtime component in the following situations:
 - You need to use docker in docker;
 - You need to use commands such as docker build/push/save/load in the TKE node;
 - You need to call the docker API;
 - You need the docker compose or docker swarm.


### How do I modify a runtime component?
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2/cluster/startUp) and click **Cluster** in the left sidebar.
2. On the **Cluster Management** page, click the target cluster ID to enter the cluster basic information page.
3. Modify the runtime component in the **Basic information** section. See the figure below:
>? Modifications on the runtime component and version only take effect for added nodes that are not assigned to any node pool. The existing nodes are not affected.
>![](https://qcloudimg.tencent-cloud.cn/raw/8830078644bb26a123fd41342d2da82d.png)


### What are the commands commonly used in Containerd and Docker?
Containerd does not support docker API or docker CLI. However, you can get these features with cri-tool commands.

### Image related commands
| Image Feature     | Docker                  | Containerd              |
| :--------------- | :---------------------- | :---------------------- |
| Display the local image list | docker images | crictl images |
| Download an image         | docker pull             | crictl pull             |
| Upload an image         | docker push             | None                      |
| Delete a local image     | docker rmi              | crictl rmi              |
| View image details | docker inspect IMAGE-ID | crictl inspect IMAGE-ID |


#### Container related commands

| Container Feature | Docker | containerd |
| :----------- | :------------- | :------------- |
| Display the container list | docker ps | crictl ps |
| Create a container | docker create | crictl create |
| Start a container | docker start | crictl start |
| Stop a container | docker stop | crictl stop |
| Delete a container | docker rm | crictl rm |
| View container details | docker inspect | crictl inspect |
| attach       | docker attach  | crictl attach  |
| exec         | docker exec    | crictl exec    |
| logs         | docker logs    | crictl logs    |
| stats        | docker stats   | crictl stats   |

#### POD related commands
| Pod Feature | Docker | Containerd |
| :------------ | :----- | :-------------- |
| Display the pod list | None | crictl pods |
| View pod Details | None | crictl inspectp |
| Run a pod | None | crictl runp |
| Stop a pod | None | crictl stopp |

### What are the differences between the calling chains of Containerd and Docker?
- When Docker is used as the K8s container runtime, the calling chain is as follows:
`kubelet --> docker shim (in the kubelet process) --> dockerd --> containerd`
- When Containerd is used as the K8s container runtime, the calling chain is as follows:
`kubelet --> cri plugin (in the containerd process) --> containerd`

Although Docker offers more features such as swarm cluster, docker build, and docker API, it may also introduce some bugs and requires one more calling step than Containerd,
including exec, preStop, ipv6, and log stdout formats.


## Stream Service Related Differences
Commands such as `kubectl exec` and `kubectl logs` require Kubelet to establish a stream forwarding channel between the apiserver and container runtime.

### How does a stream service work?

You can learn how CRI's stream service works by understanding how the 'kubectl exec' command works:
1. Dockershim or Containerd listens on a port to run a stream service when it is started.
2. When a command such as `kubectl exec` is run, the request finds the node corresponding to Pod through kube-apiserver and forwards it to Kubelet.
3. Kubelet requests the GetExec API of CRI-Service (dockershim or containerd-cri). The CR-Server generates a random token for the request, combines the token and the CRI Stream server listening port to form a URL, and returns it to Kubelet.
4. Kubelet upgrades the HTTP request sent by kube-apiserver to WebSocket and works as the proxy between the apiserver and CRI Stream server to forward data.

### How do I use and configure stream services in Containerd?

The docker API itself provides a stream service, and the docker-shim inside the Kubelet has its default configuration as `127.0.0.1:0`.

The stream service of Containerd needs to be configured separately:

```
[plugins.cri]
  stream_server_address = "127.0.0.1"
  stream_server_port = "0"
  enable_tls_streaming = false
```

### What are the configuration differences between versions before and after K8s v1.11?
The stream service of Containerd has different configurations for different versions of K8s.
- Before K8s v1.11:
Kubelet performs redirection but not stream proxying. That is, Kubelet sends the stream server address opened by containerd to the apiserver which then directly accesses the stream service of containerd. You need to authenticate the stream service forwarder for security purposes.
- After K8s v1.11:
 K8s v1.11 introduced [kubelet stream proxy](https://github.com/kubernetes/kubernetes/pull/64006), so that the stream service of containerd only needs to listen to the local address.

## Container Exec Differences

Docker and Containerd differ slightly in the implementation of Exec, mainly in the implementation of Execsync, which is the execution of a single command.

Therefore, the `kubectl exec` command without specifying the `-it` parameter and the ExecProbe in `pod lifecycle` may behave slightly differently on a node of a different runtime type.

### kubectl exec

- Docker exec: **The end of the first process of the current `exec`** marks the end of `exec`.
- CRI exec: **The end of all processes of the current `exec`** marks the end of `exec`.

Take the command `kubectl exec <pod-id> -- bash -c "nohup sleep 10 &"` as an example. On a runtime Docker node, the command will end about two seconds after exection, while on a Containerd node, the command will not end until the sleep process exits.

### pod exec probe

Kubelet uses the ExecSync API of CRI Runtime when implementing `exec probe`. Therefore, `exec probe` works the same as `kubectl exec # no -t -i`:

- On a Docker node, `exec probe` will still exit normally even if there are residual sub-processes.
- On a Containerd node, `exec probe` will not end until all probe processes exit.

The main impact of this difference will be postStartHook and preStopHook of `pod lifecycle`. If `exec probe` is used in hooks and residual sub-processes occur, you may encounter the case where Pods are stuck in the `containerCreating` state for a long time on Containerd nodes. The reason is that Kubelet will pull up containers one by one during `syncPod` and execute probe. If a probe is blocked due to the above reason, subsequent containers will fail to start.

Pulling up child processes and exiting the parent process in ExecProbe is a behavior not defined in K8s. The specific actions may vary depending on the runtime version and type. Therefore, it is recommended not to perform overly complex operations on probe.

## Container Network Differences

Under normal circumstances, containers in a Pod share the same network namespace, so the Pod needs to have the network ready when the sandbox container is created. To better illustrate the differences, the following briefly introduces the Pod network initialization process:

1. Kubelet calls the CRI runtime (dockershim or containerd) to create a sandbox container for the Pod.
2. The CRI runtime calls the underlying Docker or Containerd to create a pause container (now, the pause process is not started yet but the network namespace has been initialized).
3. The CRI runtime calls CNI to perform network initialization operations such as creating a Veth ENI in the network namespace and adding the cbr0 network bridge.
4. The CRI runtime starts the pause container, and the pause process is started.
5. Kubelet continues to call the CRI runtime to perform subsequent operations such as container creation.

Docker and Containerd act differently in the following two steps: **creating a pause container and initializing the network namespace** and **calling CNI to initialize the Veth ENI**.

### Creating a Pause container

Containerd is a CRI runtime designed for Kubernetes and has no separate network module, while Docker is designed with its own network functionalities. When Docker creates a pause container, it implements Docker-specific network setting. This setting causes the biggest difference between Docker and Containerd: If IPv6 is not to be used, Docker will set the kernel parameter `net.ipv6.conf.all.disable_ipv6` in the container's network namespace to `1` to disable the `ipv6` option in the container.

**For the same Pod, only IPv4 is enabled on the Docker node while both IPv4 and IPv6 are enabled on the Containerd node.**

If both IPv4 and IPv6 are enabled, DNS may send both IPv4 and IPv6 packets at the same time. In some cases, a business that requires frequent DNS resolution may trigger a bug of the DNS resolution library (depending on the Pod service implementation dependencies). On the Containerd node, you can disable IPv6 setting for a Pod by adding an init container to the Pod. The code is as follows: 

``` yaml
apiVersion: v1
kind: Pod
...
spec:
  initContainers:
  - image: busybox
    name: sysctl
    command: ["sysctl", "-w", "net.ipv6.conf.all.disable_ipv6=1"]
    securityContext:
      privileged: true
...
```

### Calling CNI 

There is no real difference between Containerd and Docker in calling CNI.

| Item | Docker | containerd |
| :------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Component responsible for calling CNI | docker-shim inside Kubelet                    | Containerd's built-in cri-plugin                                                                        |
| CNI configuration | Kubelet parameters <code>--cni-bin-dir</code> and <code>--cni-conf-dir</code> | containerd configuration file (toml): <br> <code>[plugins.cri.cni]</code><br>    <code>bin\_dir = "/opt/cni/bin"</code><br>    <code>conf\_dir = "/etc/cni/net.d"</code> |

## Container Log Differences

<table>
	<tr>
	<th style="width:10%;">Item</th>
	<th>Docker</th>
	<th>containerd</th>
	</tr>
	<tr>
		<td>Storage path</td>
		<td>
	If Docker serves as the K8s container runtime, it saves container logs to a directory such as <code>/var/lib/docker/containers/$CONTAINERID</code>. Kubelet will create a soft link under <code>/var/log/pods</code> and <code>/var/log/containers</code>, pointing to the container log files in the <code>/var/lib/docker/containers/$CONTAINERID</code> directory.
		</td>
		<td>
		If Containerd serves as the K8s container runtime, Kubelet saves container logs to the <code>/var/log/pods/$CONTAINER_NAME</code> directory, and creates a soft link under <code>/var/log/containers</code>, pointing to the log files.             
		</td>
	</tr>
  <tr>
    <td>Storage size</td>
    <td>For each container in a Pod, Docker retains 1 GB (100 MB x 10 = 1 GB) of logs by default.</td>
    <td>For each container in a Pod, Containerd retains 50 MB (10 MB x 5 = 50 MB) of logs by default.</td>
  </tr>
	<tr>
		<td>Configuration parameters</td>
		<td>
		Specify in the Docker configuration files:
		<br>    <code>"log-driver": "json-file",</code> 
		<br>    <code>"log-opts": {"max-size": "100m","max-file": "5"}</code>
		</td>
		<td>
		<ul>
		<li>
		Method 1: Specify in the Kubelet parameters: <br> <code>--container-log-max-files=5<br> --container-log-max-size="100Mi"</code> <br>
		</li>
		<li>Method 2: Specify in KubeletConfiguration: <br>    <code>"containerLogMaxSize": "100Mi",</code><br>    <code>"containerLogMaxFiles": 5, </code>
		</li>
		</ul>
		</td>
	</tr>
	<tr>
	<td>Save container logs to the data disk</td>
	<td>Mount the data disk to "data-root" (<code>/var/lib/docker</code> by default).</td>
	<td>Create a soft link <code>/var/log/pods</code> to point to a directory under the data disk mounting point. <br>Selecting "Store containers and images in the data disk" in TKE will automatically create the soft link <code>/var/log/pods</code>.
	</td>
	</tr>
</table>
