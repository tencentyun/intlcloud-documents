## Overview

During development and OPS, you may need to use multiple container image registries across tenants, regions, borders, and platforms. You can manually push and distribute tasks between instances, but problems such as high OPS costs, slow sync, and difficult management may exist.

For such scenarios, TCR currently provides synchronization and replication features and an open-source image migration tool.
- The instance synchronization feature allows you to **sync** instance images **as needed** based on the configured rules. For more information, see [Configuring Instance Synchronization](https://intl.cloud.tencent.com/document/product/1051/35494).
- The instance replication feature allows you to **replicate the full** image data from the primary instance to a replica instance. For more information, see [Configuring Instance Replication](https://intl.cloud.tencent.com/document/product/1051/39845).
- The image migration tool supports migration of Docker image data between **multiple image registry services**. For more information, see [Image Migration Tool: image-transfer](https://github.com/tkestack/image-transfer).
- In addition, when you migrate your data from another image registry service to TCR, you can also configure a custom domain name for your TCR instance or use the original domain name to maintain the service continuity. For more information, see [Configuring Custom Domain Name](https://www.tencentcloud.com/document/product/1051/43983).

This document describes how to sync and replicate image data between different image registries in a hybrid cloud.

## Prerequisites

Before creating and managing the replica instance of a TCR Enterprise Edition instance, complete the following preparations:

- You have [purchased a TCR Enterprise Edition instance](https://intl.cloud.tencent.com/document/product/1051/39088) with standard specification (for the instance synchronization feature) or premium specification (for the instance synchronization or replication feature).
- If you are using a sub-account, you must have granted the sub-account operation permissions for the corresponding instance. For more information, see [Example of Authorization Solution of the Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/37248).


## Directions

### Scenario 1: cross-region TCR instance replication

#### Cross-region instance replication

If you have a cross-region business, you can use the [instance replication](https://intl.cloud.tencent.com/document/product/1051/39845) feature to implement single-region upload, multi-region high-speed real-time synchronization, and nearby pull over private network. Compared with the instance synchronization feature, it can unify the release configuration in clusters in multiple regions and improve the cross-region synchronization speed of cloud native artifacts.

![](https://main.qcloudimg.com/raw/96e4f98d287af0d7b8c6ae54c631e33b.png)

#### Cross-border cross-region instance synchronization and replication

If your cross-region business is also cross-border, you also need to use the [instance synchronization](https://intl.cloud.tencent.com/document/product/1051/35494) feature. For security compliance considerations, cross-border instance replication is not supported currently.
1. Purchase a domestic and an overseas premium TCR instance and [create a synchronization rule](https://intl.cloud.tencent.com/document/product/1051/35494#.E5.88.9B.E5.BB.BA.E5.90.8C.E6.AD.A5.E8.A7.84.E5.88.99) to sync data across borders as needed.
2. [Create and manage replica instances](https://intl.cloud.tencent.com/document/product/1051/39845#.E5.88.9B.E5.BB.BA.E5.B9.B6.E7.AE.A1.E7.90.86.E5.A4.8D.E5.88.B6.E5.AE.9E.E4.BE.8B) in both instances to implement single-region upload, multi-region real-time replication, and nearby pull over private network domestically and overseas.
![](https://qcloudimg.tencent-cloud.cn/raw/892c4b757db9af5b0e7b62b632710018.png)
> !To implement nearby pull over private network, you need to manually connect the VPC in the replication region to the instance. Refer to [Private Network Access Control](https://intl.cloud.tencent.com/document/product/1051/35492) and select the VPC in the replication region.


### Scenario 2: cross-platform image migration or synchronization

If you use both a public cloud image registry and a self-built image registry at the same time or use multiple public cloud image registry, you often need to migrate or sync images across platforms. In this case, you can use TCR's custom domain name feature to implement unified access to multiple platforms through the same configuration, so as to ensure service continuity. For more information, see [Configuring Custom Domain Name](https://www.tencentcloud.com/document/product/1051/43983).

#### Cross-platform image migration

image-transfer is an open-source tool provided by Tencent Cloud for image migration and supports batch image migration between multiple image registry services as long as they are based on Docker Registry V2, such as TCR Personal Edition and Enterprise Edition, Docker Hub, Quay, Alibaba Cloud Container Registry (ACR), and Harbor. It has two use modes: general mode and quick migration mode exclusive to Tencent Cloud as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/c66431f1bd3fd2369ccac7bb29d5a9bb.png)

<dx-tabs>
::: General\smode
You can use the general mode of image-transfer to migrate images between multiple image registries. To do so, you only need to configure the authentication file and migration rule file. For more information on how to download, install, and use this tool, see [image-transfer](https://github.com/tkestack/image-transfer/blob/main/README.md).
:::
::: Quick\smigration\smode
You can use the quick migration mode of image-transfer to migrate from TCR Personal Edition to Enterprise Edition. For more information, see [Migration from TCR Personal Edition to TCR Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/39844), which describes how to use [image-transfer](https://github.com/tkestack/image-transfer) for quick full data migration and how to smoothly migrate a business in the TCR console.
Currently, TCR provides the Personal Edition and Enterprise Edition services at the same time. The Personal Edition service is for individual developers and only provides basic features for container image storage and distribution. While the Enterprise Edition service is for enterprise users and can provide a secure, dedicated, and high-performance cloud native artifacts hosting and distribution service. For the differences between the two editions, please see [TCR Specifications](https://intl.cloud.tencent.com/document/product/1051/35483).
:::
</dx-tabs>





#### Cross-platform image synchronization

In cross-platform scenarios, in addition to batch data migration, you often also need to sync images across platforms in real time.

You can sync an image from external Harbor to TCR Enterprise Edition as instructed in [Synchronizing Images to TCR Enterprise Edition from External Harbor](https://intl.cloud.tencent.com/document/product/1051/37255). To do so, you need to configure the synchronization rules in Harbor. On one hand, migration from an external container image service to TCR reduces the OPS and management costs of building and maintaining the service, and TCR offers professional and stable cloud hosting services and technical support; on the other hand, such migration enables linkage with TKE, so that you can enjoy a consistent user experience of cloud-based containers and pull images over the private network of the container cluster, which reduces the public network bandwidth costs. In addition, you can also configure rules in Harbor to sync images to other third-party registry service platforms. Harbor supports the following image registry services:

- Docker Hub
- Docker Registry
- AWS Elastic Container Registry
- Azure Container Registry
- Alibaba Cloud Container Registry
- Google Container Registry
- Huawei SWR
- Artifact Hub
- GitLab
- Quay
- Jfrog Artifactory
- Tencent Container Registry

You can also use the external Harbor registry as a relay to sync images between third-party registry service platforms.

The following image takes **real-time image synchronization from ACR to TCR** as an example:
1. Configure a pull-based replication policy in Harbor to pull an image from ACR to Harbor in real time and use Harbor as a relay registry.
2. Configure a push-based replication policy in Harbor to push the image from ACR in Harbor to TCR in real time.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/IxbV124_6474945ca85e11ed9e14525400088f3a.png)
In this way, the image can be synced from ACR to TCR. You can also configure image synchronization between other platforms in the same way.


### Scenario 3: DevOps image flow

During development and OPS, an application usually needs to undergo multiple steps from development and testing to pre-production and eventual release into the production environment. The corresponding image also needs to flow through multiple steps.

You can use TCR's instance synchronization feature to build a DevOps pipeline for the aforementioned scenario to flow the image. If different root account are used in different environments, enable "Support cross-root account instance synchronization" when configuring an instance synchronization rule.

You can also use the delivery pipeline feature to push code to automatically trigger image building and application deployment or locally push images to automatically trigger deployment.


![](https://qcloudimg.tencent-cloud.cn/raw/17550d36f7b536ca7e91133e2808fe64.png)

> ! Currently, TCR's delivery pipeline feature only supports preconfigured fixed pipelines. If you need more complicated DevOps pipelines, you can use [CODING DevOps](https://console.cloud.tencent.com/coding), which is Tencent Cloud's one-stop DevOps tool. TCR's delivery pipeline feature depends on the continuous integration and deployment features of CODING DevOps.

