## Overview
The Tencent Container Registry (TCR) Enterprise Edition provides enterprise-grade exclusive and secure image hosting services for enterprise-grade container customers who have strict data security and compliance requirements, businesses distributed across multiple regions, and large cluster scales. Compared with the TCR Personal Edition, the TCR Enterprise Edition supports container image secure scanning, cross-region automatic synchronization, Helm chart hosting, network access control, and other features. For more information, see [Tencent Container Registry](https://intl.cloud.tencent.com/document/product/1051).

This document describes how to use a private image hosted in TCR to deploy applications in Tencent Kubernetes Engine (TKE).

## Prerequisites
Before you use a private image hosted in TCR to deploy applications in TKE, ensure that you have completed the following operations:
- You have created a TCR enterprise edition instance in the [TCR console](https://console.cloud.tencent.com/tcr). If you have not created a TCR enterprise edition instance, create one. For more information, see [Create an enterprise instance](https://intl.cloud.tencent.com/document/product/1051/35486).
- If you are using a sub-account, you must have granted the sub-account operation permissions for the corresponding instance. For more information, see [Example of Authorization Solution of the Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/37248).


## Directions

### Preparing a container image
#### Creating a namespace
A new TCR Enterprise Edition instance does not have a default namespace, and a namespace cannot be automatically created through the pushed image. Therefore, create a namespace as required. For more information, see [Manage namespaces](https://intl.cloud.tencent.com/document/product/1051/35487).
We recommend that the namespace be named according to the project or team name. In this document, `docker` is used as an example. The following page appears after the namespace is created.
![](https://main.qcloudimg.com/raw/38d0f3739e45a94c39265b32fe0437aa.png)

#### Creating an image repository (optional)
Container images are hosted in specific image repositories. Create an image repository as required. For more information, see [Manage Image Registry](https://intl.cloud.tencent.com/document/product/1051/35488). Set the image repository name to the name of the container image to be deployed. In this document, `getting-started` is used as an example. The following page appears after the image repository is created.
>? Use Docker CLI or another image tool, such as jenkins, to push the image to the TCR Enterprise Edition instance. If no image repository exists, an image repository will be automatically created. You do not need to create one in advance.

![](https://main.qcloudimg.com/raw/c07fbfbc133bde822f13f7a5005ea6d8.png)

#### Pushing a container image
You can use Docker CLI or another image, such as jenkins to push an image to a specific image repository. Here, the Docker CLI is used to push images. To push a container image, you need to use a CVM or physical server with Docker installed and ensure that the client is allowed to access the instance. For more information, see [Network Access Control Overview](https://intl.cloud.tencent.com/document/product/1051/35490).
1. Obtain an access credential for the TCR enterprise edition instance and run the Docker Login command to log in to the instance. For more information on how to obtain an instance access credential, see [Obtaining an Instance Access Credential](https://intl.cloud.tencent.com/document/product/1051/37253).
2. After successful login, create a container image on the local server or obtain a public image from Docker Hub for testing.
This document uses the latest Nginx image on the official Docker Hub website as an example. In the command line tool, run the following commands sequentially to push this image. Replace `demo-tcr`, `docker`, and `getting-started` with the names of the actual instance, namespace, and image repository you have created.
```
docker tag getting-started:latest demo-tcr.tencentcloudcr.com/docker/getting-started:latest
```
```
docker push demo-tcr.tencentcloudcr.com/docker/getting-started:latest
```
After the image is pushed, you can go to the "[Image Repository](https://console.cloud.tencent.com/tcr/repository)" page in the TCR console and select a repository name to view details.
<span id="deployTKE"></span>

### Configuring a TKE cluster to access a TCR Enterprise Edition instance
TCR Enterprise Edition instances support network access control and deny all external access by default. You can select a public network or private network for a TKE cluster to access a specific instance and pull the container image based on the network configuration of the TKE cluster. If the TKE cluster and TCR instance are deployed in the same region, we recommend that the TKE cluster pull the container image through a private network to accelerate pulling and reduce public network traffic costs.
#### Using the TCR add-on for quick access configuration (recommended)
1. Log in to the TKE console and click **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. On the "Cluster Management" page, click the ID of the target cluster to go to the cluster details page. 
3. On the cluster details page, click **Component management** in the left sidebar to go to the "Component management" page and click **Create**.
4. On the "Create an add-on" page, select "TCR", as shown below.
    >? The TCR add-on only supports clusters in Kubernetes 1.14 or 1.16. If you use another cluster version, manually configure the access method.
	
   ![](https://main.qcloudimg.com/raw/217494ffd43b7d2e6d2621df67d5d80a.png)
  - Click **View Details** view the add-on features and configuration description.
  - Click **Parameter Configurations** to configure the add-ons.
5. On the "TCR add-on parameter settings" page, configure related parameters based on the add-on configuration method in **View Details**, as shown below:
![](https://main.qcloudimg.com/raw/729b3e3b4170de3c6d344adb1ccaf7cf.png)
    - **Associate with Instance**: select a TCR instance in the same region as the TKE cluster.
    - **Password-free Pulling**: retain the default setting.
    - **Private Network Access**: if "Normal link" is not displayed for "Private network access link", configure a private network link between the TCR instance and TKE cluster in the VPC where they reside. For more information, see [Private network Access control](https://intl.cloud.tencent.com/document/product/1051/35492).
6. Click **OK** to return to the add-on selection page.
7. On the add-on selection page, click **Done** to install the TCR add-on for the cluster.
8. After the add-on is installed, the cluster can pull images from the associated instance without needing a password through a private network, as shown below.
![](https://main.qcloudimg.com/raw/28820e0f8742656ea540f86e6336c156.png)

#### Manually configuring private network access and the access credential
#### 1. Configuring private network access
1. Configure a private network link between the TCR instance and TKE cluster in the VPC where they reside. For more information, see [Private network access control](https://intl.cloud.tencent.com/document/product/1051/35492).
2. Configure the domain name resolution of the TCR instance in the TKE cluster. Select either of the following solutions based on your actual requirements:
 - **Configuring the node host when creating the cluster**
 In the "CVM Configuration" step during the TKE cluster creation process, select **Advanced Settings** and enter the following content in "Node Launch Configuration":
```
echo '172.21.17.69 demo.tencentcloudcr.com' >> /etc/hosts
```
 - **Configuring the node host for an existing cluster**
Log in to the cluster nodes and run the following command:
```
echo '172.21.17.69 demo.tencentcloudcr.com' >> /etc/hosts
```
Replace `172.21.17.69` and `demo.tencentcloudcr.com` with the private network resolution IP address and TCR instance domain name that you use.

<span id="issued"></span>
#### 2. Configuring the access credential
When creating a namespace, follow the steps below to deliver an access credential:
1. Log in to the TKE console and click **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. On the "Cluster Management" page, click the ID of the target cluster to go to the cluster details page.
3. Click **Namespace** in the left sidebar to go to the "Namespace" page and click **Create**.
4. On the "CreateNamespace" page, select "Auto-issue TKE image repository access token" and select the TCR instance that the cluster needs to access, as shown below.
	![](https://main.qcloudimg.com/raw/46557c14ff5e9f833e911a9ad08e0d6d.png)
5. Click **Create Namespace**.
	After the namespace is created, the access credential of the instance is automatically delivered to the namespace. To view the access credential, for example, `1000090225xx-tcr-m3ut3qxx-dockercfg`, choose **Configuration Management** > **Secret**. `1000090225xx` indicates the UIN of the sub-account used to create the namespace, and `tcr-m3ut3qxx` indicates the ID of the selected instance.

Perform the following steps to deliver the access credential to an existing namespace:
<span id="loginInfo"></span>
1. Obtain the username and password used to log in to the instance. For more information, see [Obtaining an Instance Access Credential](https://intl.cloud.tencent.com/document/product/1051/37253).
2. On the cluster details page, choose **Configuration Management** > **Secret** in the left sidebar to go to the "Secret" page.
3. On the "Secret" page, click **Create** to go to the "CreateSecret" page, as shown below. Refer to the following information to deliver the access credential.
	![](https://main.qcloudimg.com/raw/73e3f94b14b0c37940c27f85f58e5e87.png)
	Main parameters are described as follows:
	 - **Secret Type**: select **Dockercfg**.
	 - **Effective Scope**: select the namespace to which the access credential is delivered.
	 - **Repository Domain Name**: enter the access domain name of the TCR instance.
	 - **Username and Password**: enter the username and password obtained in [Step 1](#loginInfo).
4. Click **Create Secret** to deliver the access credential.

### Using the container image in the TCR instance to create a workload
1. On the cluster details page, choose **Workload** > **Deployment** from the left sidebar.
2. On the "Deployment" page, click **Create**.
3. On the "CreateWorkload" page, set the following parameters to create a workload.
The main parameters are described as follows:
 - **Namespace**: select the namespace to which the access credential is delivered.
 - **Containers in the pod**:
    - **Image**: click **Select an image**. In the "Select an image" window, select a container image in the TCR instance, as shown below:
![](https://main.qcloudimg.com/raw/deb308676d70aa35a6f3fba1046281d9.png)
 - **Image Access Credential**:
	 - If the cluster has the TCR add-on installed, it does not need to be configured.
	 - If the cluster does not have the TCR add-on installed, click **Add Image Access Credential** and select the access credential delivered in [Configuring the access credential](#issued).
![](https://main.qcloudimg.com/raw/e8ef83350f71a79b014bfcfc2382fd46.png)
4. After other parameters are set, click **Create Workload** and view the workload deployment progress.
After the workload is deployed, the "Number of running/desired pods" for the workload is "1/1" on the "Deployment" page, as shown below.
![](https://main.qcloudimg.com/raw/b1d02a4df392d56e191daff8ae61db0f.png)
