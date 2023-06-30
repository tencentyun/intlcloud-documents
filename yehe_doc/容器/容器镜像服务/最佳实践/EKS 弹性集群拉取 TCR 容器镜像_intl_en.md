## Overview

This document describes how to pull container images in the TCR Enterprise Edition instance in [Elastic Kubernetes Service (EKS )](https://intl.cloud.tencent.com/document/product/457/41709) and to create workloads.


## Prerequisites


Before using a private image hosted in TCR Enterprise Edition to deploy applications in TKE, complete the following operations:

- [Purchasing Instances](https://intl.cloud.tencent.com/document/product/1051/39088).
- [Connecting to a Cluster](https://intl.cloud.tencent.com/document/product/457/34048).
- If you are using a sub-account, you must have granted the sub-account required permissions for the instance. For more information, see [Example of Authorization Solution of the Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/37248).



## Directions

### Preparing a container image


#### Step 1: Creating a namespace

A new TCR Enterprise Edition instance does not have a default namespace, and a namespace cannot be automatically created through the pushed image. Therefore, create a namespace as required. For more information, see [Managing namespaces](https://intl.cloud.tencent.com/document/product/1051/35487).

We recommend that the namespace be named based on the project or team name. In this document, `docker` is used as an example. The following page appears after the namespace is created.
![](https://main.qcloudimg.com/raw/a28fba305ce10d5b5171bd8784858b1d.png)        



#### Step 2: (Optional) Creating an image repository

Container images are hosted in specific image repositories. Create an image repository as required. For more information, see [Creating an image repository](https://intl.cloud.tencent.com/document/product/1051/35488). Set the image repository name to the name of the container image to be deployed. In this document, `getting-started` is used as an example. The following page appears after the image repository is created.
![](https://main.qcloudimg.com/raw/dcdb8203395941831ca08c415c5b5544.png)       

>? Use `docker cli` or another image tool, such as jenkins, to push the image to the TCR Enterprise Edition instance. If no image repository exists, an image repository will be automatically created. You do not need to create one in advance.



#### Step 3: Pushing container images



1. You can use `docker cli` or another image building tool, such as jenkins, to push an image to a specific image repository. Here, the `docker cli` is used to push images. In this step, you need to use a CVM or CPM with Docker installed and ensure that the target client is in the public or private network access allowlist defined in [Network Access Control Overview](https://intl.cloud.tencent.com/document/product/1051/35490).
2. Obtain an access credential for the TCR Enterprise Edition instance and run the Docker Login command to log in to the instance. For more information on how to obtain an instance access credential, see [Obtaining an Instance Access Credential](https://intl.cloud.tencent.com/document/product/1051/37253).
3. After successful login, create a container image on the local server or obtain a public image from Docker Hub for testing.
This document uses the latest Nginx image on the official Docker Hub website as an example. In the command-line tool, run the following commands sequentially to push this image. Note to replace `demo-tcr`, `docker`, and `getting-started` with the actual instance, namespace, and image repository names that you created.
<dx-codeblock>
:::  sh
docker tag getting-started:latest demo-tcr.tencentcloudcr.com/docker/getting-started:latest
:::
</dx-codeblock>
<dx-codeblock>
:::  sh
docker push demo-tcr.tencentcloudcr.com/docker/getting-started:latest
:::
</dx-codeblock>
4. After the image is pushed, you can go to the [Image Repository](https://console.cloud.tencent.com/tcr/repository) page in the TCR console and click the name of a repository to view its details.






### Configuring an EKS cluster to access a TCR Enterprise Edition instance



For your data security, TCR and EKS initially deny all public and private accesses by default. Please configure the network access policies before deploying the images of TCR to EKS.



TCR Enterprise Edition instances support network access control. You can select public network or private network access for an EKS cluster to access a specific instance and pull the container image based on the network configuration of the EKS cluster. If the EKS cluster and TCR instance are deployed in the same region, we recommend that the EKS cluster pull the container image through the private network to accelerate pulling and reduce public network traffic costs.

This document will describe how to access through private network. If you need to access through public network, please see [Accessing Internet through NAT Gateway](https://intl.cloud.tencent.com/document/product/457/38369) for more information.






#### Step 1: Associating the VPC where the cluster is located to the TCR instance



For the data security, the new TCR instance denies all external access by default. To allow the specified EKS cluster to access the TCR instance to pull the image, you need to associate the VPC where the cluster is located to the TCR instance, and configure the corresponding private network domain resolutions.



1. [Create a private network access linkage](https://intl.cloud.tencent.com/document/product/1051/35492).
2. [Configure domain name private network resolution](https://intl.cloud.tencent.com/document/product/1051/35492).





#### Step 2: Obtaining TCR instance access credential[](id:step2)



Before pulling container images from TCR instances, you need log in to the instance with credential information. For more information, see [Obtaining an Instance Access Credential](https://intl.cloud.tencent.com/document/product/1051/37253). Keep the long-term access credential of this instance for later configuration and deployment of TCR images.





### Using the container image in the TCR instance to create a workload



1. Log in to the TKE console and click **[Elastic Container - Elastic Cluster](https://console.cloud.tencent.com/tke2/ecluster?rid=19)** in the left sidebar.
2. Select the cluster ID that you want to create the workload to go to the cluster details page.
3. On the cluster details page, choose **Workload** > **Deployment** in the left sidebar.
4. On the "Deployment" page, click **Create**.
5. On the “Create Workload” page, create a workload. The main parameters are as follows:
	- **Namespace**: select a namespace in the cluster as needed.
	- **Containers in the Pod**:
		- **Image**: click **Select Image**, select **Tencent Container Registry - Enterprise** in the pop-up, and select region, instance and image repository based on your needs. See the figure below:
	![](https://main.qcloudimg.com/raw/ca9b67d0d180e42fb08b17202cbb685b.png)    
	- **Image Tag**: after you select an image, click **Select Image Tag**, and select a tag for the image repository based on your needs in the pop-up. If you do not select, the `latest` will be used by default.
	- **Image Access Credential**: click **Add Image Access Credential**, and select **Use New Access Credential** in the drop-down list. See the figure below:
	![](https://main.qcloudimg.com/raw/ea875f129af582942cc01bacd9c17376.png)      
	Click **Configure Access Credential Information**, enter the repository domain name, username and password for the image in the pop-up.
	- **Repository Domain Name**: Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Image Repository** in the left sidebar to get the repository address of the desired image.
	- **Username**: go to [Account Info](https://console.cloud.tencent.com/developer) to get account ID. The account ID is your username.
	- **Password**: the access credential obtained in the above [Step 2](#step2) “Obtaining TCR instance access credential” is the password.
	- **Access Settings (Service)**: users can deploy all kinds of containers in Kubernetes. Some of them provide layer-7 network service through HTTP and HTTPS protocols, and others provide layer-4 network service through TCP and UDP protocols. The Service resources defined by Kubernetes can be used to manage the service access for layer-4 network in the cluster. Refer to the following main parameters to complete access setting.
		- **Service**: select **Enable**.
		- **Service Access**: select **Via VPC**.
6. After configuring other parameters, click **Create Workload** and view the workload deployment progress.
After the workload is deployed, "Number of Running/Desired Pods" for the workload becomes "1/1" on the "Deployment" page.   
