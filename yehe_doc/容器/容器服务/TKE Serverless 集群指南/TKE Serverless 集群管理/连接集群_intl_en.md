This document describes how to connect a local Client to an TKE Serverless cluster through kubectl, which is the Kubernetes command-line tool.


## Prerequisites
- Install cURL software program.
- Select an appropriate way to obtain kubectl based on the OS type:
<dx-alert infotype="notice" title="">
Replace "v1.18.4" in the command line with the kubectl version required by your business based on actual needs. Generally, the version of kubectl on the Client should be consistent with the latest version of Kubernetes on service end. You can view the K8s version on the **Basic Information** section of the **Basic Information** page.
</dx-alert>
<dx-tabs>
::: Mac OS
Run the following command to obtain kubectl:
```shell
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.18.4/bin/darwin/amd64/kubectl
```
:::
::: Linux
Run the following command to obtain kubectl:
```shell
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.18.4/bin/linux/amd64/kubectl
```
:::
::: Windows
Run the following command to obtain kubectl:
```shell
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.18.4/bin/windows/amd64/kubectl.exe
```
:::
</dx-tabs>




## Directions
[](id:installKubectl)
### Installing kubectl

1. Install kubectl as instructed in [Installing and Setting up kubectl](https://kubernetes.io/docs/user-guide/prereqs/).
<dx-alert infotype="explain" title="">
- If you have already installed kubectl, skip this step.
- This step uses the Linux OS as an example.
</dx-alert>
2. Run the following command to grant permissions to use kubectl.
```shell
chmod +x ./kubectl
```
 ```shell
sudo mv ./kubectl /usr/local/bin/kubectl
 ```
3. Run the following command to verify the whether the installation is successful.
```shell
kubectl version
```
 If the output is similar to the following version information, the installation was successful.
```shell
Client Version: version.Info{Major:"1", Minor:"5", GitVersion:"v1.5.2", GitCommit:"08e099554f3c31f6e6f07b448ab3ed78d0520507", GitTreeState:"clean", BuildDate:"2017-01-12T04:57:25Z", GoVersion:"go1.7.4", Compiler:"gc", Platform:"linux/amd64"}
```


### Configuring kubeconfig


1. Log in to the TKE console and select **[Cluster](https://console.cloud.tencent.com/tke2/ecluster)** in the left sidebar.
2. On the **Cluster** list page, click the ID of the target cluster that you want to connect to go to the management page of the Serverless cluster.
3. Click **Basic Information** in the left sidebar to go to the **Basic Information** page, as shown in the following figure.
4. In **Cluster APIServer information** section, enable the **Internet Access** or **Private Network Access**, and view information such as the access address, and kubeconfig access credential of the cluster. 
 - Access entry: configure the access entry as needed.
    - **Internet Access**: this option is disabled by default. Note that enabling public network access will expose the APIServer of the cluster to the public network. In addition, you need to configure source authorization. By default, access from all sources is rejected. You can allow access from a single IP address or CIDR block. It is strongly recommended that you not open the cluster to all sources by configuring 0.0.0.0/0.
    - **Private Network Access**: this option is disabled by default. To enable it, you need to specify the subnet of the APIServer for private network access. IP addresses are assigned from the configured subnet after private network access is successfully enabled.
 - **Accessed URL**: APIServer address of the cluster. Note that this address cannot be copied and pasted to a browser for access.
 - **Kubeconfig**: access credential of the cluster, which can be copied and downloaded.
5. Configure the cluster credential as needed. For more information, see **Connecting to Kubernetes cluster through Kubectl** in the console.


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
kubectl get pod
```
If you cannot connect to the cluster, check whether public network access or private network access is enabled, and ensure that the access client is in the specified network environment.

## Notes

### Introduction to the kubectl CLI

Kubectl is a CLI tool for performing operations on Kubernetes clusters. This document covers the `kubectl` syntax, common command operations, and examples. For more information on each command (including all main commands and subcommands), see the [kubectl reference document](https://kubernetes.io/docs/reference/generated/kubectl/kubectl/) or run the `kubectl help` command to view help information. For more information on kubectl installation, see [Installing kubectl](#installKubectl).

