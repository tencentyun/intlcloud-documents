## TKE Cluster Configuration
This step describes how to enable the cluster access entry and obtain the cluster access address, token, and cluster CA certificate information for configuring Jenkins.
<span id="proof"></span>
### Obtaining the cluster credential
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Clusters** in the left sidebar to go to the cluster management page.
2. Choose **More** > **View Cluster Credentials** on the right of the row where the target cluster is located to go to the basic information page of the cluster.
3. In "Cluster APIServer Information", perform the following operations.

   1. View and record the **access address** of the cluster and the **token** in Kubeconfig.
   2. To enable private network access, you need to set the subnet as the VPC subnet shared by Jenkins Master and TKE nodes.

<span id="getCA"></span>
### Obtaining the cluster CA certificate
1. Log in to the node of the cluster as instructed in [Logging In to Linux Instances by Using the Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436).
2. Run the following command to view the cluster CA certificate.
```
cat /etc/kubernetes/cluster-ca.crt
```
3. Record and save the returned certificate information, as shown in the following figure:
![](https://main.qcloudimg.com/raw/9431bdeb070e4e2e382bf6ea628b1842.png)

### Authorizing docker.sock 

Each node of the TKE cluster has a `docker.sock` file. The slave pod connects to this file when running `docker build`. Before that, you need to log in to each node and run the following commands to authorize `docker build`:
```
chmod 666 /var/run/docker.sock
```
```
ls -l /var/run/docker.sock
```


## Configuring Jenkins

### Adding a TKE private network access address

1. Log in to the Jenkins Master node as instructed in [Logging in to Linux Instances by Using the Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436).
2. Run the following command to configure the access domain name.
```
sudo sed -i '$a 10.x.x.x cls-ixxxelli.ccs.tencent-cloud.com' /etc/hosts
```
> This command can be obtained from "Cluster APIServer" on the basic information page of the cluster after private network access is enabled in the cluster. For more information, see [Obtaining the cluster credential](#proof). 
> 
3. Run the following command to query whether the configuration is successful.
```
cat /etc/hosts
```
If the result shown in the following figure appears, the configuration was successful.
![](https://main.qcloudimg.com/raw/2e1bd6f1df51f150e9064d68f01e1754.png)
               
### Required plug-ins for Jenkins installation
1. Log in to the Jenkins backend and click **System Management** in the left sidebar.
2. On the "Manage Jenkins" panel, click **Plug-in Management**.
3. Select **Optional Plug-ins** on the plug-in management page, and check Locale, Kubernetes, Git Parameter, and Extended Choice Parameter.
 - **Locale**: indicates the Chinese localization plug-in. This plug-in sets the Jenkins interface to the Chinese version by default.
 - **Kubernetes**: indicates the Kubernetes plug-in.
 - **Git Parameter** and **Extended Choice Parameter**: are used to pass parameters during package building.
   Take the Kubernetes plug-in as an example, as shown in the following figure:
![](https://main.qcloudimg.com/raw/6849c1c9cbd54db29e3cb5fb91e3c994.png)
4. After checking the preceding plug-ins, click **Install Directly** and restart Jenkins.

### Enabling the jnlp port
1. Log in to the Jenkins backend and click **System Management** in the left sidebar.
2. On the "Manage Jenkins" panel, click **Global Security Configuration**.
3. On the "Global Security Configuration" page, set the TCP port of the inbound proxy to the "specified port 50000".
4. Keep other configuration items as their defaults and click **Save** at the bottom of the page.
<span id="addToken"></span>
### Adding a TKE cluster token
1. Log in to the Jenkins backend and choose **Credentials** > **System** in the left sidebar.
2. On the "System" panel, select **Global Credentials (Unrestricted)**.
3. On the "Global Credentials (Unrestricted)" page, click **Add Credentials** in the left sidebar.
- **Type**: select **Secret text**.
  - **Scope**: is **Global (Jenkins, nodes, items, all child items, and others)** by default.
  - **Secret**: enter the **cluster token** obtained in the [Obtaining the cluster credential](#proof) step.
  - **ID**: is left empty by default.
  - **Description**: complete the information about the credential, which is displayed as the credential name and descriptive information. This document uses `tke-token` as an example.
4. Click **OK** to add the credential, which is displayed in the credential list after being successfully added.
<span id="addGitlab"></span>
### Adding GitLab authentication
1. On the "Global Credentials (Unrestricted)" page, click **Add Credentials** in the left sidebar, and set the basic credential information as instructed in the following figure:
 - **Type**: select **Username with password**.
 - **Scope**: is **Global (Jenkins, nodes, items, all child items, and others)** by default.
 - **Username**: indicates the GitLab username.
 - **Password**: indicates the GitLab login password.
 - **ID**: is left empty by default.
 - **Description**: complete the information about the credential, which is displayed as the credential name and descriptive information. This document uses `gitlab-password` as an example.
2. Click **OK** to finish the addition.
<span id="PodTemplates"></span>
### Configuring the slave pod template
1. Log in to the Jenkins backend and click **System Management** in the left sidebar.
2. On the "Manage Jenkins" panel, click **System Configuration**.
3. At the bottom of the "System Configuration" panel, choose **Add a Cloud** > **Kubernetes** in the "Cloud" area.
4. Click **Kubernetes Cloud details...** to configure the following basic information for Kubernetes.
The following describes the main parameters. For other parameters, simply keep them as their defaults:
  - **Name**: enter a custom name. This document uses `kubernetes` as an example.
    - **Kubernetes address**: to obtain the TKE cluster access address, see [Obtaining the cluster credential](#proof).
    - **Kubernetes service certificate key**: to obtain the cluster CA certificate, see [Obtaining the cluster CA certificate](#getCA).
    - **Credential**: select the `tke-token` credential created in the [Adding a TKE cluster token](#addToken) step, and then click **Test Connection**. If the connection succeeds, the "Connection test successful" prompt appears.
    - **Jenkins address**: enter a Jenkins private network address, such as `http://10.x.x.x:8080`.
5. Choose **Pod Templates** > **Add Pod Template** > **Pod Template details...** and configure the basic information of the pod template.
The following describes the main parameters. For other parameters, simply keep them as their defaults:
 - **Name**: enter a custom name. This document uses `jnlp-agent` as an example.
 - **Tag list**: define the tag name. You can select a pod for building based on the tag. This document uses `jnlp-agent` as an example.
  - **Usage**: select **Use this node whenever possible**.
<span id="ContainerTemplate"></span>
6. In "Container List", choose **Add Container** > **Container Template** and configure the following information about the container.
  - **Name**: enter a custom container name. This document uses `jnlp-agent` as an example.
    - **Docker image**: enter the image address `jenkins/jnlp-slave:alpine`.
    - **Working directory**: keep it as its default. Record the working directory, which will be used for building and packaging shell scripts.
    - Leave other options as their defaults.
7. In "Volume", complete the following steps to add a volume and configure the docker command for the slave pod.
   1. Choose **Add Volume** > **Host Path Volume**. Enter `/usr/bin/docker` for both the host and mounting paths.
   2. Choose **Add Volume** > **Host Path Volume**. Enter `/var/run/docker.sock` for both the host and mounting paths.
8. Click **Save** at the bottom of the page to finish configuring the slave pod template.

## Subsequent Operations
Go to [Step 2: Slave pod building configuration](https://intl.cloud.tencent.com/document/product/457/34868) to create a task and configure task parameters.
