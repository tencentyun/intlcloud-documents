## Operation Scenario

You can connect to a TKE cluster from a local client using kubectl, the Kubernetes command line tool. This document guides you through the process of connecting to a cluster.

## Preparing the Software

Please select an appropriate way to obtain kubectl based on the OS type:
> Replace "v1.8.13" in the command line with the kubectl version required by your business based on actual needs.

- **macOS X**
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

1. Install kubectl as instructed in [Installing and Setting up kubectl](https://kubernetes.io/docs/user-guide/prereqs/).
>If you have already installed kubectl, ignore this step.
2. Run the following command to add run permission.
```shell
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
```
3. Run the following command to check the installation result.
```shell
kubectl version
```
If the output is similar to the following version information, the installation is successful.
```shell
Client Version: version.Info{Major:"1", Minor:"5", GitVersion:"v1.5.2", GitCommit:"08e099554f3c31f6e6f07b448ab3ed78d0520507", GitTreeState:"clean", BuildDate:"2017-01-12T04:57:25Z", GoVersion:"go1.7.4", Compiler:"gc", Platform:"linux/amd64"}
```

### Getting Cluster Account, Password and Certificate Information

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster?rid=4)** to go to the cluster management page.
3. Click the **ID/name** of the cluster to be connected to to go to the management page of the cluster.
4. In the left sidebar, select "Basic information" to go to the "Basic information" page. See the figure below:
![Basic Information](https://main.qcloudimg.com/raw/8dc59b2eaab1c1e19a75974d573ec96d.png)
5. In "Basic information", click **Show credentials** in "Cluster credentials".
6. In the "Cluster credentials" window that pops up, view the username, password, and certificate information.
>You can save the cluster CA certificate locally by clicking **Copy** or **Download** based on actual needs.
7. In the "Cluster credentials" window that pops up, get the access entry.
 - Directly access in the cluster: Keep the default values for "Public network access address" and "Private network access address" and you can run kubectl commands directly on a server in the cluster without any configuration required.
 - Get public network access entry: Set the "Public network access address" to "On". Then, you can directly use the public network access address to access the public network as instructed in [Setting kubectl Command Autocomplete](#setKubectlAutomaticComplete).
 - Get VPC private network access entry: Set the "Private network access address" to "On" and specify the client server's **hosts** to support domain name resolution. You can do so by appending the **IP** and domain name returned by the private network to the end of the `/etc/hosts` file. You can set it manually or by referring to the code below.
```
sudo sed -i '$a **IP address** **domain name**' /etc/hosts
```
After the configuration is completed, you can use the private network access address and domain name to access the private network as instructed in [Setting kubectl Command Autocomplete](#setKubectlAutomaticComplete).
>If there are no nodes available in the cluster (including cases where nodes are exceptional or cordoned), private network access will take effect when there are nodes available in the cluster.
8. Click **Close**.

### Using kubectl to Manipulate a Cluster Through Certificate Information

#### Single kubectl Operation Request with Certificate Information

>This method is well suited for a single kubectl operation on a cluster, without saving the certificate information of the container cluster to the server.

**Request method**

The kubectl command format is as follows:
```
-s "domain name information" --username=username --password=password --certificate-authority=certificate path
```

**Sample**

```shell
kubectl get node -s "https://cls-66668888.ccs.tencent-cloud.com" --username=admin --password=6666o9oIB2gHD88882quIfLMy6666 --certificate-authority=/etc/kubernetes/cluster-ca.crt
```

#### Modifying the kubectl Configuration File for Long-term Validity

>This method is well suited for long-term operation on a cluster through kubectl. It only needs to be configured once and can be used for a long time without having to modifying the file.

1. Refer to the following command to modify the password and certificate information in the kubectl configuration file.
```shell
kubectl config set-credentials default-admin --username=admin --password=6666o9oIB2gHD88882quIfLMy6666
kubectl config set-cluster default-cluster --server=https://cls-66668888.ccs.tencent-cloud.com --certificate-authority=/etc/kubernetes/cluster-ca.crt
kubectl config set-context default-system --cluster=default-cluster --user=default-admin
kubectl config use-context default-system
```
2. After the configuration is completed, run the following command to get the node information.
```shell
kubectl get nodes
```
If a message similar to the one below is returned, the modification is successful.
```
NAME        STATUS    AGE
10.0.0.61   Ready     10h
```

<span id="setKubectlAutomaticComplete"></span>
### Setting kubectl Command Autocomplete

You can configure kubectl autocomplete to improve usability by running the following command.
```shell
source <(kubectl completion bash)
```
