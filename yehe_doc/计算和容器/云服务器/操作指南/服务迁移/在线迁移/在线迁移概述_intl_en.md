Online migration refers to migrating or synchronizing systems and applications on the source server or virtual machine from your IDCs or other cloud platforms to Tencent Cloud with no system downtime.
After the go2tencentcloud migration tool provided by Tencent Cloud is executed on the source server to be migrated, all systems and service applications running on the source server can be migrated to the destination CVM of Tencent Cloud. This migration tool can directly migrate source data to the cloud without the tedious preparations, such as creating, uploading, and importing images. It can meet enterprises' business requirements for cloud deployment, cross-cloud platform migration, cross-account or cross-region migration, and hybrid cloud deployment.

<dx-alert infotype="explain" title="">
The source server can be a physical server, a virtual machine, or a cloud server on another cloud platform, such as AWS, Google Cloud Platform, VMware, Alibaba Cloud, or Huawei Cloud.
</dx-alert>



## Application Scenarios

Online migration is applicable to the following scenarios (including but not limited to):
- IT architecture cloudification
- Hybrid cloud architecture deployment
- Cross-cloud migration
- Cross-account or cross-region migration

## Differences from Offline Migration

In offline migration, you need to create images for system disks or data disks on source servers, and then migrate images to the Cloud Virtual Machine (CVM) or Cloud Block Storage (CBS). You do not need to create images for online migration. Instead, you can run the migration tool on source servers to migrate them to destination CVMs.

## Features

Currently, online migration supports the server migration feature.

## Starting Migration

<dx-alert infotype="explain" title="">
Currently, the online migration service in the console is in beta test. To try it out, [contact us](https://intl.cloud.tencent.com/document/product/213/34837) for application.
</dx-alert>

After registering the migration source server to Tencent Cloud using the go2tencentcloud tool provided by Tencent Cloud, manage the migration source and complete the migration task via the feature of online migration in the CVM console. For details, see [Migration in Console](https://intl.cloud.tencent.com/document/product/213/44338).

## FAQs

For more information, please see [Service Migration](https://intl.cloud.tencent.com/document/product/213/32395).
