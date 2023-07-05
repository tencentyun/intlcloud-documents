## Overview
Currently, TCR provides the Personal Edition and Enterprise Edition services at the same time. The Personal Edition service is for individual developers and only provides basic features for container image storage and distribution. While the Enterprise Edition service is for enterprise users and can provide a secure, dedicated, and high-performance cloud native artifacts hosting and distribution service. For the differences between the two editions, please see [TCR Specifications](https://intl.cloud.tencent.com/document/product/1051/35483).

This document describes how enterprise customers can migrate container image data and business configuration from the Personal Edition to the Enterprise Edition to achieve smooth business migration.

## Prerequisites

To migrate from the Personal Edition service to the Enterprise Edition, you need to confirm and complete the following preparations:
- You have activated the Personal Edition service and your account has the permission to pull all the images in the image repository of the Personal Edition. For how to grant full read/write permissions of the Personal Edition to the sub-account, please see [Example of Authorization Solution of the Personal Edition](https://intl.cloud.tencent.com/document/product/1051/37250).
- You have purchased the [Enterprise Edition Instance](https://intl.cloud.tencent.com/document/product/1051/39088), and your account has the permission to push image to this instance. For how to grant the sub-account the permission for pushing the container image and Helm Chart of the corresponding instance, please see [Example of Authorization Solution of the Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/37248). It is recommended to grant the full read/write permissions of TCR to the sub-account that configures synchronization.
- You have configured the running environment of the migration tool. It is recommended to perform the migration task in a VPC to increase the migration speed and avoid the cost of public network traffic.
  - Run the migration tool in the VPC: add the VPC where the server of the migration tool is running in the private network access of the target Enterprise Edition instance. For more information, please see [Private Network Access Control](https://intl.cloud.tencent.com/document/product/1051/35492).
  - Run the migration tool in the public network: enable the public network access entry of the target Enterprise Edition instance and allow the access sources. For more information, please see [Public Network Access Control](https://intl.cloud.tencent.com/document/product/1051/35491).

## Data Migration

### Preparing the basic running environment

1. Purchase an Enterprise Edition instance in the region where the container business is deployed.
2. In the same region, prepare a CVM for image migration, and try to choose a model with high CPU/memory and high private network bandwidth. After the CVM is started up, install the latest Docker client, or select an operating system with Docker installed.
3. Connect the VPC where the CVM is located to the Enterprise Edition instance, and enable automatic private network resolution. For more information, see [Private Network Access Control](https://intl.cloud.tencent.com/document/product/1051/35492).
4. Obtain the access credentials of the instance, run `Docker Login` on the CVM for migration, and ensure that you can use the CVM to access the instance successfully via the private network.

### Preparing migration configuration

1. Obtain the access credential of the image repository.
   - Access credential of Personal Edition image repository: the username is the UIN of the Tencent Cloud account to which the image to be migrated belongs, and the password is the one set during Personal Edition initialization. If you forgot the password, go to the **[TCR console](https://console.cloud.tencent.com/tcr/instance?rid=1)** > **Instance List**, select your Personal Edition instance, and click **More** > **Reset Login Password** to reset the password.
   - Access credential of Enterprise Edition image repository: you can go to the **[TCR console](https://console.cloud.tencent.com/tcr/instance?rid=1)** and select **Access Credential** on the left sidebar. Then, select an existing Enterprise Edition instance and click **Create** to generate a long-term access credential dedicated for migration, including the username and password. Note that the user who generates this access credential needs to have full read and write permissions for the instance.
2. Obtain the API calling credential.
   You need to call TencentCloud API to automatically create the namespace and image repository in the Enterprise Edition instance during the image migration. You can go to the **[CAM console](https://console.cloud.tencent.com/cam/capi)**, select **Access Key** > **Manage API Key** to create a key or view the existing keys. Please keep the key information carefully.

### Downloading and running the migration tool

Run the following command to download the dedicated container image for migration:

```bash
docker pull ccr.ccs.tencentyun.com/tcrimages/image-transfer:ccr2tcr
```

Run the following command to view the instructions of the tool:

```bash
docker run --network=host --rm ccr.ccs.tencentyun.com/tcrimages/image-transfer:ccr2tcr /run --help
```

Run the following command to modify the configuration and execute the migration task:

```bash
docker run --network=host --rm ccr.ccs.tencentyun.com/tcrimages/image-transfer:ccr2tcr /run --tcrName image-transfer --ccrRegionName ap-guangzhou --tcrRegionName ap-shanghai --ccrAuth username:password --tcrAuth username:password --ccrSecretId sid- example --ccrSecretKey skey-example --tcrSecretId sid-example --tcrSecretKey skey-example --tagNum 50
```

#### Parameter description
| Parameter | Description |
|---------|---------|
| tcrName | The name of the Enterprise Edition instance to migrate |
| ccrRegionName, tcrRegionName | The region of the instance. In Chinese mainland, ccr defaults to ap-guangzhou, and tcr is set to the actual region such as ap-shanghai. |
| ccrAuth, tcrAuth | The access credential of the image repository in the format of username:password. |
| ccrSecretId, ccrSecretKey, tcrSecretId, tcrSecretKey | Tencent Cloud API calling key. If the migration is under the same account, the calling keys of ccr and tcr are the same. |
| tagNum | Specifies that only the latest N tags of images in the image repository will be migrated. |

### Viewing and confirming the running result

Because the Personal Edition is fully migrated to the Enterprise Edition by default, the migration time is directly related to the number and size of the image repositories in the current Personal Edition. Please wait patiently for the migration.
If the following code is displayed, it means that the full migration is successful. Otherwise, re-run the migration tool to try again or [submit a ticket](https://console.intl.cloud.tencent.com/workorder) for assistance.

```bash
################# Finished, 0 transfer jobs failed, 0 normal urlPair generate failed, 0 jobs generate failed #################
```

## Business Migration

### Switching the configuration of cluster image repository

#### Switching the access address

Enter the details page of a cluster or EKS cluster, select **Workload** in the left sidebar, and select to create or update a workload. In **Containers in the Pod**, enter or select an image address, or directly modify the **image** parameter in YAML, as shown below:
![](https://main.qcloudimg.com/raw/fd8819e71f12df475c33b7e8c4e27f17.png)
- Image address of Personal Edition instance: defaults to `ccr.ccs.tencentyun.com/namespace/repo:tag`. The default regions cover the AZs in Chinese mainland except Hong Kong, such as Beijing, Shanghai, and Guangzhou. The prefix domain name of Hong Kong is hkccr. Multi-level paths are not supported.
- Image address of Enterprise Edition instance: you can customize the instance name `user-define`, such as `user-define.tencentcloudcr.com/namespace/repo:tag`. You can also customize the domain name, such as `xxx-company.com/namespace/repo:tag`. Multi-level path is supported, and the image address can be `xxx-company.com/ns/sub01/sub02/repo:tag`.

#### Switching the access credential
Enter the details page of a cluster or EKS cluster, select **Workload** in the left sidebar, and select to create or update a workload. Switch the access credential in **Image Access Credential**, or directly modify the **imagePullSecret** parameter in YAML, as shown below:
![](https://main.qcloudimg.com/raw/db218539e9674c9090d548abc6f1986a.png)
- Access credential of the Personal Edition instance: when you create a namespace, a Personal Edition access credential **qCloudregistryKey** will be delivered by default.
- Access credential of Enterprise Edition instance:
  - Recommended scheme: use the special plug-in for TCR Enterprise Edition to automatically deliver and configure access credential to achieve secret-free pulling. You do not need to configure the image access credential. Please leave this parameter empty. (This is only available for TKE)
  - Manual configuration: you can configure a long-term access credential in the TCR Enterprise Edition instance, and deliver it to the namespace, or create the image access credential when creating the workload.

#### Switching the network environment

TCR Personal Edition instance does not support the network ACL. By default, all servers in Chinese mainland regions can access the Personal Edition instance via private network. While TCR Enterprise Edition instance supports the network ACL. You need to connect the VPC of the cluster to the instance and allow the access via the private network.

- Network configuration of the Personal Edition instance: no configuration is required. By default, you can access the instance and upload/download images via all network environments.
- Network configuration of the Enterprise Edition instance:
  - Access via private network (recommended): connect the VPC of the cluster or EKS cluster to the target instance, and enable the automatic resolution in the VPC or manually manage the DNS resolution. For more information, see [Private Network Access Control](https://intl.cloud.tencent.com/document/product/1051/35492).
  - Public network access: we recommend that you enable the public network access only when testing or distributing images for the external teams, and the access allowlist must be configured.

### Best practices for Enterprise Edition instance

This document provides some best practices for migration from the Personal Edition to the Enterprise Edition.

#### Multi-instance planning

Based on the actual business needs, you can create one or more instances in multiple regions, configure synchronous replication policies, and use the custom domain names to uniformly manage instance access addresses. For more information, see [Configuring Instance Synchronization](https://intl.cloud.tencent.com/document/product/1051/35494), [Configuring Instance Replication](https://intl.cloud.tencent.com/document/product/1051/39845), and [Synchronizing Images to TCR Enterprise Edition from External Harbor](https://intl.cloud.tencent.com/document/product/1051/37255).

#### Security and Compliance

- Operation compliance
   - We recommend that you grant the minimum permissions to sub-accounts using the Enterprise Edition. You can configure the repository-level permissions, that is, you can specify that a sub-account can only pull or manage the specified image repository, or you can configure more fine-grained API calling permissions. For more information, see [Example of Authorization Solution of the Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/37248).
   - You can create dedicated long-term access credentials for different usage scenarios. All long-term access credentials created by an account are only used for accessing the instance.
   - We recommend that you use the temporary login token (valid for 1 hour) for temporary instance access. For more information, see [Obtaining a temporary login token](https://intl.cloud.tencent.com/document/product/1051/37253).

- Network security
   - Please do not enable the public network access entry to prevent the external unauthorized objects from accessing the instance, or avoid incurring public network access fees for downloading the images of your business via the public network.
   - You can bind a custom domain name to the instance, and manage the public network and VPC resolution of the domain name.

#### Image management

- Repository planning
   - We recommend that you use the namespace to isolate the services, teams, etc., to facilitate permission management and synchronization rule configuration.
   - Multi-level paths are supported. You can create multi-level repositories as needed to avoid creating too many namespaces.
   - You can push images to automatically create the repositories, and configure the default attributes such as public/private at the namespace level.
   - **Note**: the namespaces and image repositories are path markers. The backend data storage is not isolated.

- Tag naming
   - Please do not use latest to update the image tag in a production environment, which may affect service updates and rollbacks.
   - We recommend that you use the CI tool for the automatic naming of images to facilitate subsequent tag management and image synchronization.
   - **Note**: if you delete an image of a specified tag, the same digest image will be deleted as well.

#### CI/CD

- The CI/CD service comes with the Enterprise Edition.
   - CI/CD capabilities of the Enterprise Edition are completely based on CODING DevOps, so you need to activate it and complete basic configuration first.
   - Image building is supported. The optional code sources include GitHub, GitLab, TGit, Gitee, and CODING.
   - Delivery pipeline is supported, which enables you to automatically deploy images in clusters, elastic clusters, and edge clusters.

- External services can be connected.
   - You can use the webhook feature to connect to an existing CI/CD system, so image push will automatically trigger a webhook notification whose message body contains the basic image information. For more information, see [Managing Triggers](https://intl.cloud.tencent.com/document/product/1051/37254).
   - You can directly use the complete service of CODING DevOps, which has built-in TCR templates.
