### How do I select a runtime component?
As one of the most important components of Kubernetes (K8s), a container runtime manages the lifecycle of images and containers. Kubelet interacts with the container runtime through the `Container Runtime Interface (CRI)` to manage images and containers.

You can choose Containerd and Docker as container runtime components:
- (Recommended) Containerd has a shorter calling chain and fewer components, and features higher stability and lower node resource consumption.
- Docker should be used as the runtime component in the following situations:
 - You need to use docker in docker;
 - You need to use commands such as docker build/push/save/load in the TKE node;
 - You need to call the docker API;
 - You need the docker compose or docker swarm.


### How do I modify a runtime component?
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2/cluster/startUp) and click **Cluster** in the left sidebar.
2. On the **Cluster management** page, click the target cluster ID to enter the cluster basic information page.
3. Modify the runtime component in the **Basic information** section.
>? Modifications on the runtime component and version only take effect for added nodes that are not assigned to any node pool. The existing nodes are not affected.
>



### What are the commands commonly used in Containerd and Docker?
Containerd does not support docker API or docker CLI. However, you can get similar features with the `cri-tool` command.

| Image Feature | Docker | Containerd |
|:-------- |:-------------- |:--------------- |
| Display the local image list | docker images | crictl images |
| Download an image | docker pull | crictl pull |
| Upload an image | docker push | None |
| Delete a local image | docker rmi | crictl rmi |
| View image details | docker inspect IMAGE-ID | crictl inspect IMAGE-ID |



| Container Feature | Docker | Containerd |
|:------ |:-------------- |:-------------- |
| Display the container list | docker ps | crictl ps |
| Create a container | docker create | crictl create |
| Start a container | docker start | crictl start |
| Stop a container | docker stop | crictl stop |
| Delete a container | docker rm | crictl rm |
| View container details | docker inspect | crictl inspect |
| attach | docker attach  | crictl attach  |
| exec   | docker exec    | crictl exec    |
| logs   | docker logs    | crictl logs    |
| stats  | docker stats   | crictl stats   |


| Pod Feature | Docker | Containerd |
|:------- |:------ |:--------------- |
| Display the Pod list | None | crictl pods |
| View Pod details | None | crictl inspectp |
| Run a Pod | None | crictl runp |
| Stop a Pod | None | crictl stopp |

### What are the differences between the calling chains?
- When Docker is used as the K8s container runtime, the calling chain is as follows:
`kubelet --> docker shim (in the kubelet process) --> dockerd --> containerd`
- When Containerd is used as the K8s container runtime, the calling chain is as follows:
`kubelet --> cri plugin (in the containerd process) --> containerd`

Although Docker offers more features such as swarm cluster, docker build, and docker API, it may also introduce some bugs and requires one more calling step than containerd.


## Stream Service
>?Commands such as `kubectl exec` and `kubectl logs` require the establishment of a stream forwarding tunnel between the apiserver and the container runtime.
>

### How do I use and configure stream services in Containerd?
The docker API itself provides a stream service, and the docker-shim inside the Kubelet forwards streams through the docker API.
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

## Other Differences
### Container logs and parameters

<table>
	<tr>
	<th style="width:10%;">Item</th>
	<th>Docker</th>
	<th>Containerd</th>
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
		<td>Configuration parameters</td>
		<td>
		Specify in the Docker configuration files:
		<br>    <code>"log-driver": "json-file",</code> 
		<br>    <code>"log-opts": {"max-size": "100m","max-file": "5"}</code>
		</td>
		<td>
		<ul>
		<li>
		Method 1: Specify in the Kubelet parameters:<br> <code>--container-log-max-files=5<br> --container-log-max-size="100Mi"</code> <br>
		</li>
		<li>Method 2: Specify in KubeletConfiguration: <br>    <code>"containerLogMaxSize": "100Mi",</code><br>    <code>"containerLogMaxFiles": 5, </code>
		</li>
		</ul>
		</td>
	</tr>
	<tr>
	<td>Save container logs to the data disk</td>
	<td>Mount the data disk to `data-root` (<code>/var/lib/docker</code> by default).</td>
	<td>Create a soft link <code>/var/log/pods</code> to point to a directory under the data disk mounting point. <br>Selecting "Store containers and images in the data disk" in TKE will automatically create the soft link <code>/var/log/pods</code>.
	</td>
	</tr>
</table>


### CNI network
| Item      | Docker            | Containerd                                                                                                       |
|:-------- |:---------------------------------------- |:---------------------------------------------------------------------------------------------------------------- |
| Component responsible for calling CNI | docker-shim inside Kubelet                    | Containerd's built-in cri-plugin (in containerd v1.1 or later)                                                                        |
| How to configure CNI  | Kubelet parameters <code>--cni-bin-dir</code> and <code>--cni-conf-dir</code> | Containerd configuration file (toml):<br> <code>[plugins.cri.cni]</code><br>    <code>bin\_dir = "/opt/cni/bin"</code><br>    <code>conf\_dir = "/etc/cni/net.d"</code> |



