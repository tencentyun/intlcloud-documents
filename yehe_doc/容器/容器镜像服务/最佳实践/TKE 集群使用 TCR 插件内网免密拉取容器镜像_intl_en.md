## Overview
This document describes how to use the TCR plug-in in [Tencent Kubernetes Engine (TKE)](https://intl.cloud.tencent.com/document/product/457/6759) to enable secret-free pulling of container images in an Enterprise Edition instance through the private network and to create workloads.

## Prerequisites
Before using a private image hosted in TCR Enterprise Edition to deploy applications in TKE, complete the following operations:
- [Create an Enterprise Edition instance](https://intl.cloud.tencent.com/document/product/1051/39088).
- [Create a TKE cluster.](https://intl.cloud.tencent.com/document/product/457/30637).
- If you are using a sub-account, you must have granted the sub-account required permissions for the instance. For more information, see [Example of Authorization Solution of the Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/37248).
- If you are using an existing TKE cluster, ensure that the sub-account has required permissions for the cluster. For more information, see [TKE Cluster Permission Management](https://intl.cloud.tencent.com/document/product/457/11542).


## Directions

### Preparing a container image
#### Step 1: Creating a namespace
A new TCR Enterprise Edition instance does not have a default namespace, and a namespace cannot be automatically created through the pushed image. Therefore, create a namespace as required. For more information, see [Manage namespaces](https://intl.cloud.tencent.com/document/product/1051/35487).
We recommend that the namespace be named based on the project or team name. In this document, `docker` is used as an example. The following page appears after the namespace is created.
![](https://main.qcloudimg.com/raw/a28fba305ce10d5b5171bd8784858b1d.png)

#### Step 2: (Optional) Creating an image repository
Container images are hosted in specific image repositories. Create an image repository as required. For more information, see [Managing Image Registry](https://intl.cloud.tencent.com/document/product/1051/35488). Set the image repository name to the name of the container image to be deployed. In this document, `getting-started` is used as an example. The following page appears after the image repository is created.
>?Use Docker CLI or another image tool, such as jenkins, to push the image to the TCR Enterprise Edition instance. If no image repository exists, an image repository will be automatically created. You do not need to create one in advance.
>
![](https://main.qcloudimg.com/raw/dcdb8203395941831ca08c415c5b5544.png)

#### Step 3: Pushing container images
You can use Docker CLI or another image building tool, such as jenkins, to push an image to a specific image repository. Here, the Docker CLI is used to push images. In this step, you need to use a CVM or CPM with Docker installed and ensure that the target client is in the public or private network access allowlist defined in [Network Access Control Overview](https://intl.cloud.tencent.com/document/product/1051/35490).
1. Obtain an access credential for the TCR Enterprise Edition instance and run the Docker login command to log in to the instance. For more information on how to obtain an instance access credential, see [Obtaining an Instance Access Credential](https://intl.cloud.tencent.com/document/product/1051/37253).
2. After successful login, create a container image on the local server or obtain a public image from Docker Hub for testing.
This document uses the latest Nginx image on the official Docker Hub website as an example. In the command-line tool, run the following commands sequentially to push this image. Note to replace `demo-tcr`, `docker`, and `getting-started` with the actual instance, namespace, and image repository names that you created.
```
docker tag getting-started:latest demo-tcr.tencentcloudcr.com/docker/getting-started:latest
```
```
docker push demo-tcr.tencentcloudcr.com/docker/getting-started:latest
```
After the image is pushed, you can go to the [Image Repository](https://console.cloud.tencent.com/tcr/repository) page in the TCR console and click the name of a repository to view its details.

### Configure TKE cluster access TCR instance[](id:deployTKE)
TCR Enterprise Edition instances support network access control and deny all external access by default. You can select public network or private network access for a TKE cluster to access a specific instance and pull the container image based on the network configuration of the TKE cluster. If the TKE cluster and TCR instance are deployed in the same region, we recommend that the TKE cluster pull the container image through the private network to accelerate pulling and reduce public network traffic costs.
#### Step 1: Associating the VPC where the cluster is located to the TCR instance
For the data security, the new TCR instance denies all external access by default. To allow the specified TKE cluster to access the TCR instance to pull the image, you need to associate the VPC where the cluster is located to the TCR instance, and configure the corresponding private network domain resolutions.
1. [Create a private network access linkage](https://intl.cloud.tencent.com/document/product/1051/35492).
2. [Configure domain name private network resolution](https://intl.cloud.tencent.com/document/product/1051/35492).




#### Step 2: Installing the TCR add-on in the TKE cluster
If you are using TKE, refer to [TCR](https://intl.cloud.tencent.com/document/product/457/38710) to install the TCR add-on in the TKE cluster and select **Enable Private Network Parsing** in the **TCR Add-on Parameter Settings** window. For nodes in the cluster, this plug-in can automatically configure private network resolution for the associated TCR instance. This enables secret-free pulling of images in the instance through the private network.
After the add-on is installed, the cluster can pull images from the associated instance without needing a password through a private network.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/xsAp075_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230209155921.png)

<dx-alert infotype="explain" title="">
Currently, the TCR add-on only supports clusters in Kubernetes1.12, 1.14, 1.16, 1.18 and 1.20. If you are using another cluster version, manually configure the access method.
</dx-alert>



### Using the container image in the TCR instance to create a workload
1. Log in to the TKE console and select **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Select the cluster ID that you want to create the workload to go to the cluster details page.
3. On the cluster details page, choose **Workload** > **Deployment** in the left sidebar.
4. On the "Deployment" page, click **Create**.
5. On the “Create Workload” page, create a workload. The main parameters are as follows:
 - **Namespace**: select as needed. Make sure that when you install the TCR add-on, the namespace configured to support secret-free pulling already contains the namespace required at this time.
 - **Containers in the Pod**:
    - **Image**: click **Select Image**, and select **Tencent Container Registry - Enterprise** in the pop-up. Select region, instance and image repository as needed. See the figure below:
    ![](https://main.qcloudimg.com/raw/ca9b67d0d180e42fb08b17202cbb685b.png)
    - **Image Tag**: after you select an image, click **Select Image Tag**, and select a tag for the image repository based on your needs in the pop-up. If you do not select, the `latest` will be used by default.
 - **Image Access Credential**: if the TCR add-on has been installed in the cluster, explicit configuration is not required. **Please do not select other access credentials, otherwise, this workload cannot load the secret-free pulling configuration of TCR add-on.**
6. After configuring other parameters, click **Create Workload** and view the workload deployment progress.
After the workload is deployed, "Number of Running/Desired Pods" for the workload becomes "1/1" on the "Deployment" page.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/aYMx653_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230209160209.png)
