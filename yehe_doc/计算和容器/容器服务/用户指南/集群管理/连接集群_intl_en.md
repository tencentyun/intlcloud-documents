## Scenario

You can connect to a TKE cluster from a local client by using kubectl, the Kubernetes command line tool. This document describes how to connect to a cluster.

## Prerequisites

The cURL software program has been installed.
You have obtained kubectl. Choose an appropriate way to obtain kubectl based on the operating system type.

>? Replace "v1.8.13" in the command line with the kubectl version required by your business as needed.

- **MacOS X**
  Run the following command to obtain kubectl:

```shell
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.8.13/bin/darwin/amd64/kubectl
```

- **Linux**
  Run the following command to obtain kubectl:

```shell
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.8.13/bin/linux/amd64/kubectl
```

- **Windows**
  Run the following command to obtain Kubectl:

```shell
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.8.13/bin/windows/amd64/kubectl.exe
```

## Directions

### Installing kubectl<span id="installKubectl"></span>

1. Install kubectl as described in [Installing and Setting Up kubectl](https://kubernetes.io/docs/user-guide/prereqs/).

>? 
>
>- Skip this step if you have already installed kubectl.
>- This step uses the Linux operating system as an example.

2. Run the following commands to grant permissions to use kubectl.

```shell
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
```

3. Run the following command to verify the installation result.

```shell
kubectl version
```

If the returned version information is similar to the following, the installation was successful.

```shell
Client Version: version.Info{Major:"1", Minor:"5", GitVersion:"v1.5.2", GitCommit:"08e099554f3c31f6e6f07b448ab3ed78d0520507", GitTreeState:"clean", BuildDate:"2017-01-12T04:57:25Z", GoVersion:"go1.7.4", Compiler:"gc", Platform:"linux/amd64"}
```

### Configuring kubeconfig

1. Log in to the TKE console and click **[Clusters](https://console.cloud.tencent.com/tke2/cluster?rid=4)** in the left sidebar to go to the cluster management page.
2. Click the ID or name of the target cluster to go to the details page of the cluster.
3. Click **Basic Info** in the left sidebar. You can view information such as the access address, public network/private network access status, and kubeconfig access credential of the cluster in the "Cluster APIServer Info" section of the "Basic Info" page, as shown in the following figure.
   ![](https://main.qcloudimg.com/raw/0505a359567a8e06c53d897e10a13b89.png)

 - **Accessed URL**: indicates the APIServer address of the cluster. Note that this address cannot be copied and pasted to a browser for access.
 - **Access Entry**: configure the address entry as needed.
   - **Public Network Access**: this option is disabled by default. Note that enabling public network access **will expose the APIServer of the cluster to the public network**. In addition, you need to configure source authorization. By default, access attempts from all sources are rejected. You can allow access from a single IP address or CIDR block. We strongly recommend that you not open the cluster to all sources by configuring `0.0.0.0/0`.
   - **Private Network Access**: this option is disabled by default. To enable it, you need to configure a subnet. IP addresses are assigned from the configured subnet after private network access is successfully enabled.
 - **Kubeconfig**: indicates the access credential of the cluster, which can be copied and downloaded.

4. Configure the cluster credential as needed.
   Before configuration, determine whether the access credential for any cluster has been configured on the current client.
   - **If no**, the `~/.kube/config` file is empty, and you can copy the obtained kubeconfig access credential into the file. If the `~/.kube/config` file does not exist on the client, create one.
   - **If yes**, you can download the obtained kubeconfig to a specified location and run the following commands in sequence to merge the config files of multiple clusters.

```
KUBECONFIG=~/.kube/config:~/Downloads/cls-3jju4zdc-config kubectl config view --merge --flatten > ~/.kube/config
```

```
export KUBECONFIG=~/.kube/config
```

	In the preceding commands, `~/Downloads/cls-3jju4zdc-config` indicates the kubeconfig file path of the current cluster. Replace this path with the actual local path of the downloaded file.
	


### Accessing the Kubernetes cluster

1. After configuring kubeconfig, run the following commands in sequence to view the contexts and switch contexts to access the cluster.

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

Kubectl is a CLI tool for performing operations on Kubernetes clusters. This document covers the `kubectl` syntax, common command operations, and some examples. For more information on each command (including all main commands and subcommands), see the [kubectl reference document](https://kubernetes.io/docs/reference/generated/kubectl/kubectl/) or run the `kubectl help` command to view help information. For more information on kubectl installation, see [Installing kubectl](#installKubectl).