## Overview

Cloud Native Datalake Storage helps you quickly deploy a COS-based data lake storage service on TKE. Then, you can deploy big data and AI service applications required by various businesses in a TKE or EKS cluster. In addition, you can also use GooseFS to connect to massive distributed storage services.


### Concepts and terms

The following lists some basic **concepts and terms** of Cloud Native Datalake Storage:
- **Environment**: It maintains the mappings between computing clusters and storage services. We recommend you uniformly manage computing clusters and storage services in an environment.
>! If you need to delete a computing cluster in the TKE console, we recommend you clear the data lake environment first.
>
- **Computing cluster**: It is a container cluster for running various computing businesses. You can create a TKE or EKS cluster.
- **Storage service**: It refers to COS, which stores different types of data for computing.
- **Application market**: It houses the application components for diversified computing businesses, such as Flink and Spark. You can select an application as needed when creating an environment.
>! When a container cluster is terminated, applications deployed in it will also be terminated. Proceed with caution.
>
- **GooseFS**: It manages different underlying buckets and caches frequently accessed data in your computing cluster to accelerate computing.

You can get some basic information in the following documents:
- COS: [Getting Started with the Console](https://intl.cloud.tencent.com/document/product/436/32955) describes how to create a bucket and upload/download files to/from it.
- TKE: [Quickly Creating a Standard Cluster](https://intl.cloud.tencent.com/document/product/457/40029) describes how to create a TKE or EKS cluster.
- Application market: [Application Market](https://intl.cloud.tencent.com/document/product/457/37706) describes how to create and deploy an application in a TKE cluster.
- GooseFS: [GooseFS on TKE Cloud Native Practices](https://www.tencentcloud.com/document/product/436/42228) describes how to manage GooseFS in a cluster.


## Prerequisites

- Currently, Cloud Native Datalake Storage is provided through an allowlist. To use it, [contact us](https://intl.cloud.tencent.com/contact-sales) for application.
- Cloud Native Datalake Storage relies on TKE and COS and requires **permissions to manipulate computing and storage services**. If you log in with a sub-account, make sure that the sub-account has at least the following permissions:
 - Permissions to manipulate COS buckets and files.
    - Permission to manipulate buckets: If you need to manage bucket configurations, get the corresponding permission from the root account. Generally, this permission doesn't affect data read/write and doesn't require extra configurations. It is sufficient to grant the read permission, such as the [QcloudCOSBucketConfigRead](https://console.cloud.tencent.com/cam/policy/detail/5295084&QcloudCOSBucketConfigRead&2) policy.
    - Permission to manipulate files: Generally, computing jobs require reading/writing files from/to buckets. You can get full access from the root account, such as the [QcloudCOSDataFullControl](https://console.cloud.tencent.com/cam/policy/detail/5294998&QcloudCOSDataFullControl&2) policy. Alternatively, the root account can grant the permission based on the [principle of least privilege](https://intl.cloud.tencent.com/document/product/436/32972).
 - Permissions to manage container clusters:
    - Permission to manipulate clusters: Generally, you need to grant permissions to create and manipulate clusters. For detailed directions, see [Using TKE Preset Policy Authorization](https://intl.cloud.tencent.com/document/product/457/37363).
    - Permission to manage clusters: TKE provides an authorization mode to connect to Kubernetes RBAC, so that sub-account access can be controlled in a refined manner. Sub-account operations are also subject to the [TKE Kubernetes object-level permission control](https://www.tencentcloud.com/document/product/457/37365).
    - Permission to manipulate the application market: The application market relies on the operations of the TCR service. For detailed directions on how to authorize a sub-account, see [TKE Image Registry Resource-level Permission Settings](https://intl.cloud.tencent.com/document/product/457/11527).


## Directions

The following details the steps, including **environment creation > cluster association > computing application deployment > storage service association > environment management**.

1. Log in to the [COS console](https://console.cloud.tencent.com/cos).
2. On the left sidebar, click **Cloud Native Datalake Storage**.
3. On the Cloud Native Datalake Storage page, you can see the deployment guide and environment list.

 - The deployment guide is displayed by default, and you can click **Collapse Guide** in the top-right corner to disable it.
 - The environment list page allows for search. You can manipulate an existing environment as follows:
     - Click **Environment Name** to enter the environment details page and manage the environment.
     - Click **Associated Cluster** to enter the cluster details page in the TKE console.
     - Click **Associated Bucket** to enter the bucket page and view the file information.
4. Click **Create Environment**.

Before creating an environment, select the target container computing cluster and configure the following parameters:
 - **Environment Name**: It can contain up to 63 characters and must be globally unique.
 - **Region**: Select the region of the container cluster.
 - **Cluster Type**: It can be TKE or EKS. If there are no clusters in the current region, you can click **Create Container Cluster** to create one in the TKE console.
 - **Cluster**: It is the name of the cluster for deploying computing applications and running computing jobs based on the **specified region** and **specified cluster type** conditions.
 - **Add-On**: It indicates the application service required for running a computing job. Currently, Flink, k8s-big-data-suite, colocation, Airflow, PyTorch, and spark-operator applications are supported by default. You can select one or multiple add-ons as needed. If you need to deploy a custom application, you can go to the TKE console for deployment on your own.
5. Click **Next** to enter the **Bucket Configuration** page.

You can configure different buckets for the computing cluster on this page. By default, GooseFS is available for managing buckets and caching data in the local nodes of the computing cluster for computing acceleration. You need to configure the following parameters:
 - Region: It is the region of the computing cluster by default and cannot be edited. If there are no available buckets for computing jobs in the region, you can click **Create Bucket** to create one.
 - Bucket: You can select multiple buckets in the specified region. You can also mount only a specified file directory of a bucket.
>! If you mount the entire bucket, you can ignore the second input box; if you need to specify a directory, enter the directory name in the format of `prefix/*`.
>
 - Enable GooseFS: GooseFS accelerates computing jobs. It is enabled by default and cannot be modified. No extra fees will be incurred.
6. Click **Next** to enter the **GooseFS Application Configuration** page.
In a data lake environment, all computing jobs need to access COS through GooseFS; therefore, you should grant GooseFS the permission to access the `secretId` and `secretKey` of the specified buckets.

7. Click **Next** and confirm the information.
8. Click **Create Environment**. If you need to modify the configuration items, click **Modify** to go back to the corresponding step.

After the creation, **go back to the environment list and refresh it**, then you can see the newly created environment.
To **delete an environment**, click **Delete** in the environment list and confirm the deletion in the pop-up window. After deletion, refresh the list, and you can see that the environment has been deleted.

9. Click the environment name in the list to enter the **Basic Information** page.

Three views are available to describe the environment, computing cluster, and bucket information.
 - Environment information: It displays the environment's name, region, associated computing cluster, storage service, and creation time.
 - Computing cluster information: It displays the computing cluster's name, number of nodes, and usage of CPU, memory, and GPU. You can click **View details** to enter the TKE console and view computing cluster details.
 - Bucket information: It displays the name, file URL, and GooseFS status of the bucket associated with the computing cluster. You can click **View details** to view the details of the storage service.

At this point, you have created a data lake environment.


