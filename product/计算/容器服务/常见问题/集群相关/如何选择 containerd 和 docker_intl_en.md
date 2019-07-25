## Runtime Component Description
As one of the most important components of Kubernetes (K8s), a container runtime is responsible for managing the lifecycle of images and containers. Kubelet interacts with the container runtime through the `Container Runtime Interface (CRI)` to manage images and containers.

TKE supports containerd and Docker as a runtime component:
- (Recommended) Containerd has a shorter call chain and fewer components and features higher stability and lower node resource consumption.
- Docker should be used as the runtime component if you need to use the following:
 - Docker in docker;
 - Commands such as docker build/push/save/load;
 - Docker API;
 - Docker compose or docker swarm.

## Common Commands in containerd and Docker
containerd does not support the docker API or docker CLI, however you can get this feature by cri-tool commands.

| Image-related Features | Docker | containerd |
| :--------------- | :------------- | :-------------- |
| Display the local image list | docker images | crictl ps |
| Download an image | docker pull | crictl pull |
| Upload an image | docker push | None |
| Delete a local image | docker rmi | crictl rmi |
| View image details | docker inspect | crictl inspecti |



| Container-related Functions | Docker | containerd |
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


| Pod-related Functions | Docker | containerd |
| :------------ | :----- | :-------------- |
| Display the pod list | None | crictl pods |
| View pod Details | None | crictl inspectp |
| Run a pod | None | crictl runp |
| Stop a pod | None | crictl stopp |

## Call Chain Description
- If Docker is selected as the K8s container runtime, the call relationship is as follows:
`kubelet --> docker shim (in the kubelet process) --> dockerd --> containerd`
- If containerd is selected as the K8s container runtime, the call relationship is as follows:
`kubelet --> cri plugin (in the containerd process) --> containerd`

Although dockerd adds functions such as swarm cluster, docker build, and docker API, it may also introduce some bugs and has one more layer of call than containerd.


## Stream Service
>Commands such as kubectl exec and kubectl logs require the establishment of a stream forwarding tunnel between the apiserver and the container runtime.
>

### Using and Configuring the Stream Service of containerd
The docker API itself provides a stream service, and the docker-shim inside the Kubelet forwards the stream through the docker API.
The stream service of containerd has to be configured separately:
```
[plugins.cri]
  stream_server_address = "127.0.0.1"
  stream_server_port = "0"
  enable_tls_streaming = false
```

### Configuration Differences
The stream service of containerd has different configurations for different versions of K8s.
- Before K8s v1.11:
Kubelet performs redirection but not stream proxying. That is, Kubelet sends the stream server address opened by containerd to apiserver and lets apiserver directly access the stream service of containerd. At this point, authentication should be implemented for the stream service forwarder for security protection.
- K8s v1.11 and later: 
 K8s v1.11 introduced [kubelet stream proxy](https://github.com/kubernetes/kubernetes/pull/64006), so that the stream service of containerd only needs to listen to the local address.

## Other Differences
### Container Log and Related Parameters

<table>
	<tr>
	<th style="width:10%;">Item</th>
	<th>Docker</th>
	<th>containerd</th>
	</tr>
	<tr>
		<td>Storage path</td>
		<td>
	If Docker is selected as the K8s container runtime, the container logs will be stored by Docker in a directory like <code>/var/lib/docker/containers/$CONTAINERID</code>. Kubelet will create a soft link under <code>/var/log/pods</code> and <code>/var/log/containers</code> pointing to the container log files in the <code>/var/lib/docker/containers/$CONTAINERID</code> directory.
		</td>
		<td>
		If containerd is selected as the K8s container runtime, the container logs will be stored by Kubelet in the <code>/var/log/pods/$CONTAINER_NAME</code> directory, which will create a soft link under <code>/var/log/containers</code> pointing to the log files.            
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
	<td>Create a soft link <code>/var/log/pods</code> to point to a directory under the data disk mount point. <br>Selecting "Store containers and images in the data disk" in TKE will automatically create the soft link <code>/var/log/pods</code>.
	</td>
	</tr>
</table>


### CNI Network
| Item | Docker | containerd |
| :------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Component responsible for calling CNI | docker-shim inside Kubelet | containerd's built-in cri-plugin (in containerd v1.1 or later) |
| How to configure CNI | Kubelet parameters <code>--cni-bin-dir</code> and <code>--cni-conf-dir</code> | containerd configuration file (toml): <br> <code>[plugins.cri.cni]</code><br>    <code>bin\_dir = "/opt/cni/bin"</code><br>    <code>conf\_dir = "/etc/cni/net.d"</code> |