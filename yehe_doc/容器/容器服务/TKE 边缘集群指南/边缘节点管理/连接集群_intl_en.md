## Scenario
This document describes how to connect a local client to an edge cluster through kubectl, which is the Kubernetes command-line tool.

## Prerequisites
- The cURL software program has been installed.
- Select the appropriate way to obtain kubectl based on the operating system:
>Replace `v1.8.13` in the command with the kubectl version required by your business.
>
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
	Run the following command to obtain kubectl:
```shell
	curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.8.13/bin/windows/amd64/kubectl.exe
```

## Directions

### Installing kubectl
1. Install kubectl as instructed in [Installing and Setting Up kubectl](https://kubernetes.io/docs/user-guide/prereqs/).
>
>- If you have already installed kubectl, skip this step.
>- This step uses the Linux operating system as an example.
2. Run the following commands to grant permissions to use kubectl.
```shell
chmod +x ./kubectl
```
```
sudo mv ./kubectl /usr/local/bin/kubectl
```
3. Run the following command to check the installation result.
```shell
kubectl version
```
If the output is similar to the following version information, the installation was successful.
```shell
Client Version: version.Info{Major:"1", Minor:"5", GitVersion:"v1.5.2", GitCommit:"08e099554f3c31f6e6f07b448ab3ed78d0520507", GitTreeState:"clean", BuildDate:"2017-01-12T04:57:25Z", GoVersion:"go1.7.4", Compiler:"gc", Platform:"linux/amd64"}
```

### Obtaining cluster certificate information

1. Log in to the [Tencent Cloud TKE console](https://console.cloud.tencent.com/tke2) and click **Edge Clusters** in the left sidebar.
2. On the **Edge Clusters** page, click **View the cluster credential** for the cluster to be connected.
3. In the **Cluster Credential** window that appears, you can view, copy, and download the credential.
>You can save the cluster access credential locally by clicking **Copy** or **Download** as needed.
>
4. In **Internet access**, click <img src="https://main.qcloudimg.com/raw/fd1ae3941057881ca71bcf8b2874b510.png" style="margin:-6px 0px"> to enable internet access for the cluster. You can also see [Configuring kubectl autocomplete](#setKubectlAutomaticComplete) for accessing with the cluster access credential.


### Using kubectl to manipulate a cluster through certificate information


#### Request method
The kubectl command format is as follows:
```
--kubeconfig=<Local cluster access credential>
```

#### Example
Run the following command to view existing namespaces under the cluster.
```shell
kubectl get namespace --kubeconfig=cls-8ipgf8u4.kubeconfig
```
The cluster credential used in this example is `cls-8ipgf8u4.kubeconfig`. In real-life cases, replace it with the actual credential.
If a message similar to the following is returned, the request was successful.
```
NAME         STATUS    AGE
default      Active    11d
kube-system  Active    11d
```

<span id="setKubectlAutomaticComplete"></span>
### Configuring kubectl autocomplete

You can configure kubectl autocomplete to improve usability by running the following command.
```shell
source <(kubectl completion bash)
```

