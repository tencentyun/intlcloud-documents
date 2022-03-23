## Overview
This document shows how to connect a local client to a TKE cluster by using kubectl, a Kubernetes command line tool.

## Prerequisites
The cURL software has been installed.
You have obtained kubectl. Choose an appropriate way to obtain kubectl based on the OS type.
>? Replace "v1.18.4" in the command line with the kubectl version required by your business based on actual needs. Generally, the version of kubectl on the Client should be consistent with the latest version of Kubernetes on service end. You can view the Kubernetes version on the **Cluster Information** section of the **Basic Information** page.

- **macOS X**
Run the following command to obtain kubectl:
```shell
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.18.4/bin/darwin/amd64/kubectl
```
- **Linux**
Run the following command to obtain kubectl:
```shell
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.18.4/bin/linux/amd64/kubectl
```
- **Windows**
Run the following command to obtain kubectl:
```shell
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.18.4/bin/windows/amd64/kubectl.exe
```

## Directions

### Installing Kubectl[](id:installKubectl)

1. Install kubectl as instructed in [Installing and Setting up kubectl](https://kubernetes.io/docs/user-guide/prereqs/).
>? 
>- If you have already installed kubectl, skip this step.
>- This step uses the Linux OS as an example.

2. Run the following commands to grant permissions to use kubectl.
```shell
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
```
3. Run the following command to verify the whether the installation is successful.
```shell
kubectl version
```
If the output shows the version information, the installation is successful.
```shell
Client Version: version.Info{Major:"1", Minor:"5", GitVersion:"v1.5.2", GitCommit:"08e099554f3c31f6e6f07b448ab3ed78d0520507", GitTreeState:"clean", BuildDate:"2017-01-12T04:57:25Z", GoVersion:"go1.7.4", Compiler:"gc", Platform:"linux/amd64"}
```

### Configuring kubeconfig

1. Log in to the TKE console and click **[Cluster](https://console.cloud.tencent.com/tke2/cluster?rid=4)** in the left sidebar to go to the cluster management page.
2. Click the ID or name of the cluster to connect to go to the details page of the cluster.
3. Click **Basic Information** in the left sidebar. You can view information such as the access address, public network/private network access status, and kubeconfig access credential of the cluster in the **Cluster APIServer Information** section of the **Basic Information** page. See the figure below.
![](https://main.qcloudimg.com/raw/9cf12f9b9be373e521f16713669d3629.png)
 - **Accessed URL**: APIServer address of the cluster. Note that this address cannot be copied and pasted to a browser for access.
 - **Access entry**: Configure the address entry as needed.
	- **Public Network Access**: This option is disabled by default. Note that enabling public network access **exposes the APIServer of the cluster to the public network**. In addition, you need to configure source authorization. By default, accesses from all sources are rejected. You can allow accesses from a single IP address or CIDR. It is strongly recommended not to open the cluster to all sources by configuring `0.0.0.0/0`.
	- **Private Network Access**: this option is disabled by default. To enable it, you need to configure a subnet. IP addresses are assigned from the configured subnet after private network access is successfully enabled.
	-. **Using the service IP address of Kubernetes**: On the cluster details page, choose **Services and Routes** > **Service** in the left sidebar to obtain the service IP address of Kubernetes in the default namespace. Replace the clusters.cluster.server field in the Kubeconfig file with https://\<`IP`\>:443. **Note**: Kubernetes service is under the ClusterIP mode and is only applicable to access within the cluster.
 - **Kubeconfig**: Access credential of the cluster, which can be copied and downloaded.
4. Configure the cluster credential as needed.
   Before configuration, check whether the access credential for any cluster has been configured on the current client.
	- **If no**, the `~/.kube/config` file is empty, and you can copy the obtained kubeconfig access credential to the file. If the `~/.kube/config` file does not exist on the client, you can create one.
	- **If yes**, you can download the obtained kubeconfig to a specified location and run the following commands in sequence to merge the config files of multiple clusters.
```
KUBECONFIG=~/.kube/config:~/Downloads/cls-3jju4zdc-config kubectl config view --merge --flatten > ~/.kube/config
```
```
export KUBECONFIG=~/.kube/config
```
	where, `~/Downloads/cls-3jju4zdc-config` is the kubeconfig file path of the current cluster. Replace it with the actual local path of the file.


### Accessing the Kubernetes cluster
1. After kubeconfig is completed, run the following commands in sequence to view the contexts and switch contexts to access the cluster.
```
kubectl config get-contexts
```
```
kubectl config use-context cls-3jju4zdc-context-default
```
2. Run the following command to check whether the cluster can be accessed.
```
kubectl get node
```
If you cannot connect to the cluster, check whether public network access or private network access is enabled, and ensure that the access client is in the specified network environment.

## Notes

### Introduction to the kubectl CLI

Kubectl is a CLI tool for performing operations on Kubernetes clusters. This document covers the `kubectl` syntax, common command operations, and examples. For more information on each command (including all main commands and subcommands), see the [kubectl reference document](https://kubernetes.io/docs/reference/generated/kubectl/kubectl/) or run the `kubectl help` command to view help information. For more information on kubectl installation, see [Installing kubectl](#installKubectl).

