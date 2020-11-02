## Overview
This document describes how to use the TCR plug-in in [Tencent Kubernetes Engine (TKE)](https://intl.cloud.tencent.com/document/product/457/6759) to enable secret-free pulling of container images in an Enterprise Edition instance through the private network and to create workloads.

## Prerequisites
Before using a private image hosted in TCR Enterprise Edition to deploy applications in TKE, complete the following operations:
- [Create an Enterprise Edition instance](https://intl.cloud.tencent.com/document/product/1051/35486).
- [Create a TKE cluster](https://intl.cloud.tencent.com/document/product/457/30637).
- If you are using a sub-account, you must have granted the sub-account required permissions for the instance. For more information, see [Example of Authorization Solution of the Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/37248).
- If you are using an existing TKE cluster, ensure that the sub-account has required permissions for the cluster. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/457/11542).


## Directions

### Preparing a container image
#### Step 1: Creating a namespace
A new TCR Enterprise Edition instance does not have a default namespace, and a namespace cannot be automatically created through the pushed image. Therefore, create a namespace as required. For more information, see [Managing Namespaces](https://intl.cloud.tencent.com/document/product/1051/35487).
We recommend that the namespace be named based on the project or team name. In this document, `docker` is used as an example. The following page appears after the namespace is created.
![](https://main.qcloudimg.com/raw/305c330e772b5e9547625e0ae77e7882.png)

#### Step 2: (Optional) Creating an image repository
Container images are hosted in specific image repositories. Create an image repository as required. For more information, see [Managing Image Registry](https://intl.cloud.tencent.com/document/product/1051/35488). Set the image repository name to the name of the container image to be deployed. In this document, `getting-started` is used as an example. The following page appears after the image repository is created:
>? Use Docker CLI or another image tool, such as jenkins, to push the image to the TCR Enterprise Edition instance. If no image repository exists, an image repository will be automatically created. You do not need to create one in advance.

![](https://main.qcloudimg.com/raw/b556fb9a5f6fc39250a2a279084842c3.png)

#### Step 3: Pushing container images
You can use Docker CLI or another image building tool, such as jenkins, to push an image to a specific image repository. Here, the Docker CLI is used to push images. In this step, you need to use a CVM or CPM with Docker installed and ensure that the target client is in the Internet or private-network access allowlist defined in [Network Access Control Overview](https://intl.cloud.tencent.com/document/product/1051/35490).
1. Obtain an access credential for the TCR Enterprise Edition instance and run the Docker login command to log in to the instance. For more information on how to obtain an instance access credential, see [Obtaining an Instance Access Credential](https://intl.cloud.tencent.com/document/product/1051/37253).
2. After successful login, create a container image on the local server or obtain a public image from Docker Hub for testing.
This document uses the latest Nginx image on the official Docker Hub website as an example. In the command-line tool, run the following commands sequentially to push this image. Note to replace `demo-tcr`, `docker`, and `getting-started` with the actual instance, namespace, and image repository names that you created.
```
docker tag getting-started:latest demo-tcr.tencentcloudcr.com/docker/getting-started:latest
```
```
docker push demo-tcr.tencentcloudcr.com/docker/getting-started:latest
```
After the image is pushed, you can go to the [**Image Repository**](https://console.cloud.tencent.com/tcr/repository) page in the TCR console and click the name of a repository to view its details.
<span id="deployTKE"></span>
### Configuring a TKE cluster to access a TCR Enterprise Edition instance
TCR Enterprise Edition instances support network access control and deny all external access by default. You can select public-network or private-network access for a TKE cluster to access a specific instance and pull the container image based on the network configuration of the TKE cluster. If the TKE cluster and TCR instance are deployed in the same region, we recommend that the TKE cluster pull the container image through the private network to accelerate pulling and reduce public-network traffic costs.
1. Log in to the TKE console and click **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. On the "Cluster Management" page, click the ID of the target cluster to go to the cluster details page. 
3. On the cluster details page, click **Component management** in the left sidebar to go to the "Component management" page and click **Create**.
4. On the "Create an add-on" page, select "TCR", as shown in the figure below:
    >? Currently, the TCR add-on only supports clusters in Kubernetes 1.14, 1.16, and 1.18. If you are using another cluster version, manually configure the access method.
	
   ![](https://main.qcloudimg.com/raw/ef9736cdcfda973f61506c4d792139c2.png)
  - Click **View Details** to view the add-on features and configuration description.
  - Click **Parameter Configurations** to configure the add-on.
5. On the "TCR add-on parameter settings" page, configure parameters based on the add-on configuration method in **View Details**, as shown in the figure below:
![](https://main.qcloudimg.com/raw/a1b54692ef14b7ccb948cbe909c2cb3b.png)
    - **Associate with Instance**: select a TCR instance in the same region as the TKE cluster.
    - **Password-free Pulling**: retain the default setting.
    - **Private Network Access**: if "Normal link" is not displayed for "Private network access link", configure a private-network link between the TCR instance and the VPC where the TKE cluster is located. For more information, see [Private Network Access Control](https://intl.cloud.tencent.com/document/product/1051/35492).
6. Click **OK** to return to the add-on selection page.
7. On the add-on selection page, click **Done** to install the TCR add-on for the cluster.
8. After the add-on is installed, the cluster can pull images from the associated instance without needing a password through a private network, as shown in the figure below.
![](https://main.qcloudimg.com/raw/4c46b790b553021a32adce893d66a016.png)

### Using the container image in the TCR instance to create a workload
1. On the cluster details page, choose **Workload** > **Deployment** in the left sidebar.
2. On the "Deployment" page, click **Create**.
3. On the "CreateWorkload" page, configure the following parameters to create a workload.
The main parameters are described as follows:
 - **Namespace**: select the namespace to which the access credential is delivered.
 - **Containers in the pod**:
    - **Image**: click **Select an image**. In the "Select an image" window, select a container image in the TCR instance, as shown in the figure below:
![](https://main.qcloudimg.com/raw/01851d3ef4780c20dd7bd939ba02159d.png)
 - **Image Access Credential**: if the TCR add-on has been installed in the cluster, explicit configuration is not required.
4. After configuring other parameters, click **Create Workload** and view the workload deployment progress.
After the workload is deployed, "Number of running/desired pods" for the workload becomes "1/1" on the "Deployment" page, as shown in the figure below:
![](https://main.qcloudimg.com/raw/9e959fb5f82335374e9089fd68b2930b.png)

