## Overview
This document shows how to connect a local client to a TKE cluster by using kubectl, a Kubernetes command line tool.


>? To improve access security and stability of TKE clusters, TKE plans to officially discontinue the domain name “cls-xxx.ccs.tencent-cloud.com” from August 10, 2022 (UTC +8). 
TKE will upgrade the cluster access from July 20, 2022 (UTC +8). After the upgrade, a new architecture will be used when you enable public/private network access for a cluster. Please re-enable cluster access during July 20 to August 10 to migrate to the new architecture (the migration is required for existing clusters). For details, see [Enabling Cluster Access](#CreateClusterEndpoint) and [Obtaining Kubeconfig](#installKubectl).
1. Under the new architecture, you can pass in a custom domain name, for which a security signature will be provided. To ensure access security, you must configure the public network resolution on your own.
2. You can access TKE clusters directly with an IP. We will assign an IP with a security signature to you.

>! Differences between the old and new architectures are listed below. [Cluster access APIs](https://console.intl.cloud.tencent.com/api/explorer?Product=tke&Version=2018-05-25&Action=CreateClusterEndpoint&SignVersion=) are compatible with the new architecture. You can migrate to the new architecture by calling the APIs. Please make adaption before **July 20, 2022 (UTC +8)** if you plan to call the APIs.
1. The public network resolution feature is not available under the new architecture. You can pass in a domain name, for which a security signature will be provided. To ensure access security, you must configure the public network resolution on your own.
2. When enabling public network access under the new architecture, you must set a security group to configure access control polices.
3. When enabling public network access under the new architecture, a public CLB is created under your account. For pricing of public CLB, see [Billing for Bill-by-IP Accounts](https://intl.cloud.tencent.com/document/product/214/36998).


## Prerequisite

You have installed [curl](https://curl.se/).

 

## Directions

[](id:installKubectl)
### 1. Installing kubectl 

1. Install kubectl as instructed in [Installing and Setting up kubectl](https://kubernetes.io/docs/user-guide/prereqs/). You can select an appropriate way to obtain kubectl based on the OS type:
>! 
>- If you have already installed kubectl, skip this step.
>- Replace "v1.18.4" in the command line with the kubectl version required by your application based on actual needs. The version of kubectl on the client must be consistent with the latest version of Kubernetes on the service end. You can check the Kubernetes version on the **Cluster information** section of the **Basic information** page.
>
<dx-tabs>
::: For Mac OS X
Run the following command to obtain kubectl:
```shell
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.18.4/bin/darwin/amd64/kubectl
```
:::
::: For Linux
Run the following command to obtain kubectl:
```shell
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.18.4/bin/linux/amd64/kubectl
```
:::
::: For Windows
Run the following command to obtain kubectl:
```shell
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.18.4/bin/windows/amd64/kubectl.exe
```
:::
</dx-tabs>

2. Here we take Linux as an example. Run the following command to grant permissions to use kubectl.
```shell
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
```
3. Run the following command to verify whether the installation is successful.
```shell
kubectl version
```
If the output shows the version information, the installation is successful.
```shell
Client Version: version.Info{Major:"1", Minor:"5", GitVersion:"v1.5.2", GitCommit:"08e099554f3c31f6e6f07b448ab3ed78d0520507", GitTreeState:"clean", BuildDate:"2017-01-12T04:57:25Z", GoVersion:"go1.7.4", Compiler:"gc", Platform:"linux/amd64"}
```


[](id:CreateClusterEndpoint)
### 2. Enabling cluster access

1. Log in to the TKE console and select **[Cluster](https://console.cloud.tencent.com/tke2/cluster?rid=1)** in the left sidebar.
2. Select the region of the cluster on the “Cluster management” page.
3. Click the ID or name of the desired cluster to go to the details page of the cluster.
4. Click **Basic information** to see if the cluster access is enabled.
![](https://qcloudimg.tencent-cloud.cn/raw/7fe39f9c4f7acc6b42b91371e174ef75.png)
<dx-tabs>
::: Enabling public network access
You need to configure relevant parameters to enable the public network access.
![](https://qcloudimg.tencent-cloud.cn/raw/783f01739af7a4d01f6d37e2ac60a7a9.png)
- **Security group**: A public CLB is automatically assigned after the public network access is enabled. You can configure access control policies via a security group. We will bind the security group to the public CLB to control access.
- **ISP type**, **Network billing mode**, **Bandwidth cap**: Configure these parameters based on your actual needs. For more information, see [Creating CLB Instances](https://intl.cloud.tencent.com/document/product/214/6149).
- **Access type**: If “public domain name” is selected, you need to pass in a custom domain name, for which we will provide a security signature. You must configure the public network resolution on your own. If “public IP” is selected, we will assign a public IP and provide a security signature for it.
:::
::: Enabling private network access
You need to configure relevant parameters to enable private network access.
![](https://qcloudimg.tencent-cloud.cn/raw/25b9df7149740f630fda826a7902f0e1.png)
- **Subnet**: It is disabled by default. To enable the private network access, you need to configure a subnet. IP addresses are assigned from the configured subnet after the private network access is successfully enabled.
- **Access type**: If “private domain name” is selected, you need to pass in a custom domain name, for which we will provide a security signature. You must configure private network resolution on your own. If “private IP” is selected, we will assign a private IP and provide a security signature for it.
-. **Using the service IP address of Kubernetes**: On the cluster details page, select **Service and route > Service** in the left sidebar to obtain the service IP address of Kubernetes in the default namespace. Replace the clusters.cluster.server field in the Kubeconfig file with https://<`IP`>:443. **Note**: Kubernetes service is under the ClusterIP mode and is only applicable to access within the cluster.
:::
</dx-tabs>





### 3. Obtaining KubeConfig
TKE provides two types of KubeConfig for use in public network access and private network access, respectively. After the cluster access is enabled, you can follow the steps below to obtain the corresponding Kubeconfig:
1. Check “Cluster APIServer information” on the “Basic information” page of the cluster.
2. Copy or download **Kubeconfig** under the corresponding access type, or check the security group, access domain name (configured when the access is enabled) and access IP for the public network access.
![](https://qcloudimg.tencent-cloud.cn/raw/15c6ed35ab46937b7bde7b908cbef094.png)

### 4. Configure KubeConfig and access the Kubernetes cluster
1. Configure the cluster credential as needed.
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
2. After kubeconfig is completed, run the following commands in sequence to view the contexts and switch contexts to access the cluster.
```
kubectl config get-contexts
```
```
kubectl config use-context cls-3jju4zdc-context-default
```
3. Run the following command to check whether the cluster can be accessed.
```
kubectl get node
```
If you cannot connect to the cluster, check whether public network access or private network access is enabled, and ensure that the access client is in the specified network environment.

## Notes

### Introduction to the kubectl CLI

Kubectl is a CLI tool for performing operations on Kubernetes clusters. This document covers the `kubectl` syntax, common command operations, and examples. For more information on each command (including all main commands and sub-commands), see the [kubectl reference document](https://kubernetes.io/docs/reference/kubectl/) or run the `kubectl help` command to view help information.
