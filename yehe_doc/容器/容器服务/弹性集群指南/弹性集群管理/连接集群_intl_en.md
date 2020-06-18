## Introduction
This document describes how to connect a local client to an elastic cluster through kubectl, which is the Kubernetes command-line tool.


## Prerequisites
- Install cURL software program
- Select an appropriate way to obtain kubectl based on the OS type:
>Replace `v1.14.5` in the following commands with the actual version of your kubectl.
>
 - **MacOS**
 Run the following command to obtain kubectl:
```shell
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.14.5/bin/darwin/amd64/kubectl
```
 - **Linux**
Run the following command to obtain kubectl:
```shell
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.14.5/bin/linux/amd64/kubectl
```
 - **Windows**
Run the following command to obtain kubectl:
```shell
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.14.5/bin/windows/amd64/kubectl.exe
```

## Directions

### Installing kubectl

1. Install kubectl as instructed in [Install and Set Up kubectl](https://kubernetes.io/docs/user-guide/prereqs/).
>
>- If you have already installed kubectl, skip this step.
>- This step uses the Linux OS as an example.
2. Run the following command to grant permissions to use kubectl.
```shell
chmod +x ./kubectl
```
```
sudo mv ./kubectl /usr/local/bin/kubectl
```
3. Run the following command to verify the whether the installation is successful.
```shell
kubectl version
```
If the output is similar to the following version information, the installation was successful.
```shell
Client Version: version.Info{Major:"1", Minor:"14", GitVersion:"v1.14.5", GitCommit:"0e9fcb426b100a2aea5ed5c25b3d8cfbb01a8acf", GitTreeState:"clean", BuildDate:"2019-08-05T09:21:30Z", GoVersion:"go1.12.5", Compiler:"gc", Platform:"windows/amd64"}
```

### Obtaining the account, password, and certificate information of the cluster
1. Log in to the TKE console and click **[Elastic Cluster](https://console.cloud.tencent.com/tke2/ecluster)** in the left sidebar.
2. On the **Elastic Cluster** page that appears, click the ID of the cluster that you want to connect to open the management page.
3. Click **Basic Information** in the left sidebar to go to the **Basic Information** page.
4. On the **Basic Information** page, click **Show Credential** for the **Cluster Credential** field.
5. <span id="info"></span>In the **Cluster Credential** window that appears, do as follows depending on the actual situation:
  - Obtain the account, password, and certificate information and then click **Copy** or **Download** to save the CA certificate locally.
  - Enable **Internet Access** or **private network Access** and then connect to the cluster through the IP address.
    - **Intra-cluster access**: leave the values of **Public IP Access Address** and **Private Network Access Address** as their defaults, which indicate that public and private IP addresses are disabled. In this case, you can directly run kubectl commands on a server in the cluster without any configuration.
     - **Internet-based access**: set **Public IP Access Address** to **Enabled**. After that, you can gain access to the cluster through a public IP address. For more information, see [Operating the cluster based on certificate information through kubectl](#TheCluster).
    - **VPC-based access**: set **Private Network Access Address** to **Enabled**. You must specify the subnet of the VPC for the API server. In addition, ensure that the selected subset has an available IP address. After that, you can access the cluster through the private IP address. For more information, see [Operating the cluster based on certificate information through kubectl](#TheCluster).

<span id="TheCluster"></span>

### Operating the cluster based on certificate information through kubectl

#### Sending a single kubectl operation request with certificate information
>This method can be used to perform a single operation on a cluster. This way, you do not have to save the certificate information of the TKE cluster to the server for a long period of time.
>
**Request:**
Parameters in the kubectl command are described as follows:
```
-s "Domain information" --username=Username --password=Password --certificate-authority=Certificate path
```
 - **Domain information**: indicates the obtained public or private IP address.
 - **Username**: defaults to `admin`.
 - **Password**: it is the same as that of `token` in the **Cluster Credential** window. You can obtain the token from [Step 5](#info).
 - **Certificate path**: it is the same as that of `Cluster CA Certificate` in the **Cluster Credential** window. You can obtain the path from [Step 5](#info).

**Examples**
Run the following command to obtain the node information of a cluster:
```shell
kubectl get node -s "https://xxx.xx.xx.xxx:443/" --username=admin --password=6666o9oIB2gHD88882quIfLMy6666 --certificate-authority=/etc/kubernetes/cluster-ca.crt
```

#### Modifying the kubectl configuration file for long-term validity
>This method can be used to perform long-term operations on a cluster through kubectl. You only need to configure the configuration file once, and the configuration file remains effective until it is modified.
>
1. Run the following example command to modify the password and certificate information in the kubectl configuration file.
```shell
kubectl config set-credentials default-admin --username=admin --password=6666o9oIB2gHD88882quIfLMy6666
kubectl config set-cluster default-cluster --server=https://xxx.xx.xx.xxx:443/ --certificate-authority=/etc/kubernetes/cluster-ca.crt
kubectl config set-context default-system --cluster=default-cluster --user=default-admin
kubectl config use-context default-system
```
2. After the configuration is completed, run the following example command to obtain the node information.
```shell
kubectl get namespaces
```
A message similar to the following is returned, indicating that the configuration was successful.
```
NAME         STATUS    AGE
default      Active    11d
kube-system  Active    11d
```

<span id="setKubectlAutomaticComplete"></span>
### Enabling auto-complete for commands in kubectl
You can run the following command to enable auto-complete for all commands that you enter in kubectl, so as to improve the usability of kubectl.
```shell
source <(kubectl completion bash)
```

