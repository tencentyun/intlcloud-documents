Users often have to perform complex customization tasks on TKE clusters in order to accommodate their businesses. When Pods do not function properly, it is hard to pinpoint the exact cause. This article aims to provide a starting point for troubleshooting these issues.

[Pod Exceptions](https://intl.cloud.tencent.com/document/product/457/35760#.E9.97.AE.E9.A2.98.E5.AE.9A.E4.BD.8D) is a great series of articles that describes how to troubleshoot and solve these issues.

## Common Commands

The following is a list of commands commonly used for troubleshooting Pod issues:

* Query Pod status
```
kubectl get pod <pod-name> -o wide
```
* Query Pod YAML configuration
```
kubectl get pod <pod-name> -o yaml
```
* Query Pod events
```
kubectl describe pod <pod-name>
```
* Query container logs
```
kubectl logs <pod-name> [-c <container-name>]
```

## Pod Statuses

The following table provides a list of Pod statuses:
<table>
	<tr>
	<th>Status</th> <th>Description</th>
	</tr>
	<tr>
	<td><code>Error</code></td><td>Error occurred during Pod launch.</td>
	</tr>
	<tr>
	<td><code>NodeLost</code></td><td>The node on which the Pod resides is unreachable.</td>
	</tr>
	<tr>
	<td><code>Unkown</code></td><td>Pod is unreachable or other unknown exception.</td>
	</tr>
	<tr>
	<td><code>Waiting</code></td><td>Pod is waiting to launch.</td>
	</tr>
	<tr>
	<td><code>Pending</code></td><td>Pod is waiting to be scheduled.</td>
	</tr>
	<tr>
	<td><code>ContainerCreating</code></td><td>Pod containers are being created.</td>
	</tr>
	<tr>
	<td><code>Terminating</code></td><td>Pod is being terminated.</td>
	</tr>
	<tr>
	<td><code>CrashLoopBackOff</code></td><td>Container exited. Kubelet is restarting it.</td>
	</tr>
	<tr>
	<td><code>InvalidImageName</code></td><td>Unable to resolve image name.</td>
	</tr>
	<tr>
	<td><code>ImageInspectError</code></td><td>Unable to verify image.</td>
	</tr>
	<tr>
	<td><code>ErrImageNeverPull</code></td><td>Policy prohibits image pull.</td>
	</tr>
	<tr>
	<td><code>ImagePullBackOff</code></td><td>Trying to pull the image again.</td>
	</tr>
	<tr>
	<td><code>RegistryUnavailable</code></td><td>Unable to connect to the image registry.</td>
	</tr>
	<tr>
	<td><code>ErrImagePull</code></td><td>General image pull error.</td>
	</tr>
	<tr>
	<td><code>CreateContainerConfigError</code></td><td>Unable to create the container configuration used by kubelet.</td>
	</tr>
	<tr>
	<td><code>CreateContainerError</code></td><td>Failed to create container.</td>
	</tr>
	<tr>
	<td><code>RunContainerError</code></td><td>Failed to launch container.</td>
	</tr>
	<tr>
	<td><code>PreStartHookError</code></td><td>preStart hook execution error.</td>
	</tr>
	<tr>
	<td><code>PostStartHookError</code></td><td>postStart hook execution error.</td>
	</tr>
	<tr>
	<td><code>ContainersNotInitialized</code></td><td>Container not initialized.</td>
	</tr>
	<tr>
	<td><code>ContainersNotReady</code></td><td>Container not ready.</td>
	</tr>
	<tr>
	<td><code>ContainerCreating</code></td><td>Container is being created.</td>
	</tr>
	<tr>
	<td><code>PodInitializing</code></td><td>Pod being initialized.</td>
	</tr>
	<tr>
	<td><code>DockerDaemonNotReady</code></td><td>Docker is not ready.</td>
	</tr>
	<tr>
	<td><code>NetworkPluginNotReady</code></td><td>Network plugin not ready.</td>
	</tr>
</table>


## Troubleshooting
Use one of the following articles to troubleshoot your Pod exceptions:
- [Pod remains in ContainerCreating or Waiting Status](https://intl.cloud.tencent.com/document/product/457/35761)
- [Pod Remains in ImagePullBackOff Status](https://intl.cloud.tencent.com/document/product/457/35762)
- [Pod Remains in Pending Status](https://intl.cloud.tencent.com/document/product/457/35763)
- [Pod Remains in Terminating Status](https://intl.cloud.tencent.com/document/product/457/35764)
- [Pod Health Check Fails](https://intl.cloud.tencent.com/document/product/457/35765)
- [Pod Remains in CrashLoopBackOff Status](https://intl.cloud.tencent.com/document/product/457/35766)
- [Container Exits](https://intl.cloud.tencent.com/document/product/457/35767)
