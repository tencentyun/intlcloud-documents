This document describes how to install LogListener on a self-built Kubernetes cluster to collect logs to CLS.

During the installation process, perform the following operations:
1. Dependencies
 - Standard Kubernetes cluster. MicroK8s, K3s, or other non-standard Kubernetes clusters are not supported.
 - Helm 3.1 or later is required.

2. Helm installation
For detailed directions, see [Installing Helm](https://docs.helm.sh/docs/intro/install/).

3. LogListener installation
```
wget https://mirrors.tencent.com/install/cls/k8s/tencentcloud-cls-k8s-install.sh
```
```
bash +x tencentcloud-cls-k8s-install.sh
```
```
./tencentcloud-cls-k8s-install.sh --region ap-guangzhou --secretid xxx --secretkey xxx
```

4. Parameter description
<table>
	<tr>
		<th>Parameter</th>
		<th>Description</th>
	</tr>
		<tr>
			<td>secretid</td>
			<td>Tencent Cloud account access ID</td>
		</tr>
		<tr>
			<td>secretkey</td>
			<td>Tencent Cloud account access key</td>
		</tr>
		<tr>
			<td>region</td>
			<td>CLS region</td>
		</tr>
		<tr>
			<td>docker_root</td>
			<td>The root directory of the cluster Docker. The default value is `/var/lib/docker`. If the actual directory is different from the default one, specify the root directory of Docker.</td>
		</tr>
		<tr>
			<td>cluster_id</td>
			<td>Cluster ID. If it is not specified, a default ID will be generated during installation (we recommend that you specify a cluster ID, as the generated default ID is less readable).</td>
		</tr>
		<tr>
			<td>network</td>
			<td>Private network or public network (default).</td>
		</tr>
		<tr>
			<td>api_network</td>
			<td>Private network or internet (default) for TencentCloud API.</td>
		</tr>
		<tr>
			<td>api_region</td>
			<td>TencentCloud API region. For more information, see <a href="https://intl.cloud.tencent.com/document/product/614/18940"> Available Regions</a>.</td>
		</tr>
</table>

	Sample:
  Component deployment in Guangzhou
  ```
  ./tencentcloud-cls-k8s-install.sh --secretid xxx --secretkey xx --region ap-guangzhou  --network internet --api_region ap-guangzhou
  ```

5. Viewing 
  1. View the installed Helm package.
  After the successful installation, view the `tencent-cloud-cls-log` Helm package.
  ```
  helm list -n kube-system
  ```

  2. View the components.
  ```
  kubectl get pods -o wide -n kube-system | grep tke-log-agent
  ```
  ```
  kubectl get pods -o wide -n kube-system | grep cls-provisioner
  ```

  Run the above commands to check whether all components start properly. In normal cases, a `tke-log-agent` collection Pod and a `cls-provisioner` Pod will start on each host.

6. LogListener configuration

  1. Run the following kubectl command to modify the environment variables of `tke-log-agent`.

     ```
     kubectl edit ds tke-log-agent -n kube-system
     ```

  2. Edit the environment variables to define LogListener collection configuration. ![img](https://tapd.woa.com/tfl/captures/2023-01/tapd_20422236_base64_1673580199_31.png)

  3. Parameter description

     <table>
     	<tr>
     		<th>Variable</th>
     		<th>Description</th>
     	</tr>
     		<tr>
     			<td>MAX_CONNECTION</td>
     			<td>Maximum number of connections, which is `10` by default.</td>
     		</tr>
     		<tr>
     			<td>CHECKPOINT_WINDOW_SIZE</td>
     			<td>The checkpoint window size of a file, which is `1024` by default.</td>
     		</tr>
     		<tr>
     			<td>MAX_FILE_BREAKPOINTS</td>
     			<td>Breakpoint file size, which is `N*2k`. `N` defaults to `8k`.</td>
     		</tr>
     		<tr>
     			<td>MAX_SENDRATE</td>
     			<td>Maximum sending rate (bytes/s), which is not limited by default.</td>
     		</tr>
     		<tr>
     			<td>MAX_FILE</td>
     			<td>Maximum number of monitored files, which is `15000` by default.</td>
     		</tr>
     		<tr>
     			<td>MAX_DIR</td>
     			<td>Maximum number of monitored directories, which is `5000` by default.</td>
     		</tr>
     		<tr>
     			<td>MAX_HTTPS_CONNECTION</td>
     			<td>Maximum number of HTTPS connections, which is `100` by default.</td>
     		</tr>
     		<tr>
     			<td>CONCURRENCY_TASKS</td>
     			<td>LogListener task pool, which is `256` by default (supported by v3.x or later).</td>
     		</tr>
       	<tr>
     			<td>PROCESS_TASKS_EVERY_LOOP</td>
     			<td>Number of tasks processed every loop, which is `4` by default.</td>
     		</tr>
       	<tr>
     			<td>CPU_USAGE_THRES</td>
     			<td>LogListener memory usage threshold, which is not limited by default.</td>
     		</tr>
     </table>

7. Upgrade

  1. For Kubernetes 1.13 or later:
  ```
  wget http://mirrors.tencent.com/install/cls/k8s/upgrade/upgrade.sh
  ```

    ```
  chmod +x upgrade.sh
    ```

    ```
  ./upgrade.sh
  ```

  2. For Kubernetes versions earlier than 1.13:
  ```
  wget http://mirrors.tencent.com/install/cls/k8s/upgrade/upgrade-1.13.sh
  ```

    ```
  chmod +x upgrade-1.13.sh
  ```

    ```
  ./upgrade-1.13.sh
  ```

8. Uninstallation
  Run the following command to uninstall the installed `tencent-cloud-cls-log` Helm package.
  ```
  helm uninstall tencent-cloud-cls-log -n kube-system
  ```
>! To completely delete the `tencent-cloud-cls-log` package, regardless of whether you need to redeploy it after specifying the `–cluster_id` parameter incorrectly or you don't need to deploy it any more, you need to run the following command to delete the `secret` of `cls-k8s`, as it saves the `–cluster_id` parameter.
```
kubectl delete secret -n kube-system cls-k8s
```

8. Troubleshooting
For detailed directions, see [Self-Built Kubernetes Log Collection Troubleshooting Guide](https://cloud.tencent.com/document/product/614/84182).
