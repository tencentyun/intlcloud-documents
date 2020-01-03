## Operation Scenario

You can connect to a TKE cluster from a local client using kubectl, the Kubernetes command line tool.

## Directions

### Install kubectl tool

Install kubectl as instructed in [Installing and Setting up kubectl](https://kubernetes.io/docs/user-guide/prereqs/). Ignore this step if kubectl tool is already installed. 

### Download kubectl tool
- macOS X
```shell
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.8.13/bin/darwin/amd64/kubectl
```
- Linux
```shell
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.8.13/bin/linux/amd64/kubectl
```
- Windows
```shell
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.8.13/bin/windows/amd64/kubectl.exe
```
>For Kubernetes versions 1.10 and above, use kubectl tool v1.10 and above. Otherwise, please use kubectl tool prior to v1.10. Replace “v1.8.13” in the above sample to the kubectl version needed. 

#### Add execution permission

Use the command below to add execution permissions:
```shell
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
```

#### Testing the installation result

Enter the following commands to test the installation. If the version information is returned, kubectl is successfully installed.
```shell
kubectl version
Client Version: version.Info{Major:"1", Minor:"5", GitVersion:"v1.5.2", GitCommit:"08e099554f3c31f6e6f07b448ab3ed78d0520507", GitTreeState:"clean", BuildDate:"2017-01-12T04:57:25Z", GoVersion:"go1.7.4", Compiler:"gc", Platform:"linux/amd64"}
```

### Getting Cluster Account, Password and Certificate Information
1. Log into [TKE console > Clusters](https://console.cloud.tencent.com/tke2/cluster?rid=1). Click the **Cluster ID/name** of the cluster.
2. In the cluster information page, click **Show Credential** to check user name, password and certificate information. 
3. Copy or download the certificate file to your local storage.
4. Get access entry.
 - Public network access entry: Enable public network access, get the access address and use it directly as instructed in [Using kubectl to Manipulate a Cluster Through Certificate Information](#step3) 
 - VPC private network access entry: Private network **DNS** resolution is not supported currently. You need to specify the **hosts** of the client host for domain name resolution by adding the **IP** and domain name returned from the private network to the `/etc/hosts` file. You can use the command below or set it manually. 
```
sudo sed -i '$a **IP address** **domain name**' /etc/hosts
```
After the configuration, access via the private network access domain name as instructed in [Using kubectl to Manipulate a Cluster Through Certificate Information](#step3).
>If there are no nodes available in the cluster (including cases where nodes are exceptional or cordoned), private network access will take effect when there are nodes available in the cluster.
 - Inter-cluster access: no additional configurations required. You can run the kubectl command directly on nodes in the cluster.

<a id="step3"></a>

### Using kubectl to Manipulate a Cluster Through Certificate Information

#### Single kubectl Operation Request with Certificate Information

This method is well suited for a single kubectl operation on a cluster, without saving the certificate information of the container cluster to the server.
Request method, kubectl command format:
```
-s "domain name information" --username=username --password=password --certificate-authority=certificate path
```
Sample:
```shell
kubectl get node -s "https://cls-66668888.ccs.tencent-cloud.com" --username=admin --password=6666o9oIB2gHD88882quIfLMy6666 --certificate-authority=/etc/kubernetes/cluster-ca.crt
```

#### Modifying the kubectl Configuration File for Long-term Validity

This method is well suited for long-term cluster operations through kubectl. It only needs to be configured once and can be used long term as long as the file is not modified.
Refer to the following command to modify the password and certificate information in the kubectl configuration file.
```shell
kubectl config set-credentials default-admin --username=admin --password=6666o9oIB2gHD88882quIfLMy6666
kubectl config set-cluster default-cluster --server=https://cls-66668888.ccs.tencent-cloud.com --certificate-authority=/etc/kubernetes/cluster-ca.crt
kubectl config set-context default-system --cluster=default-cluster --user=default-admin
kubectl config use-context default-system

```
After configuration, directly use the following kubectl command:
```shell
kubectl get nodes
NAME        STATUS    AGE
10.0.0.61   Ready     10h
```


## Setting kubectl Command Autocomplete
You can configure kubectl autocomplete to improve usability.
```shell
source <(kubectl completion bash)
```
