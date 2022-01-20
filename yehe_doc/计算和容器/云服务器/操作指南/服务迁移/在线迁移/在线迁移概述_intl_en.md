Online migration refers to migrating or synchronizing systems and applications on the source server or virtual machine from your IDCs or other cloud platforms to Tencent Cloud with no system downtime.
After the go2tencentcloud migration tool provided by Tencent Cloud is executed on the source server to be migrated, all systems and service applications running on the source server can be migrated to the destination CVM. This tool can directly migrate source data to the cloud without the tedious preparation procedure of creating, uploading, and importing images. It can meet enterprises' business requirements for cloud deployment, cross-cloud platform migration, cross-account or cross-region migration, and hybrid cloud deployment.

<dx-alert infotype="explain" title="">
The source server can be a physical server, a virtual machine, or a cloud server on another cloud platform, such as AWS, Microsoft Azure, Google Cloud Platform, VMware, Alibaba Cloud, or Huawei Cloud.
</dx-alert>



## Use Cases

Online migration is applicable to the following scenarios:
-	IT architecture cloudification
-	Hybrid cloud architecture deployment
-	Cross-cloud migration
-	Cross-account or cross-region migration

## Differences from Offline Migration

In offline migration, you need to create images for system disks or data disks on source servers, and then migrate images to the Cloud Virtual Machine (CVM) or Cloud Block Storage (CBS). You do not need to create images for online migration. Instead, you can run the migration tool on source servers to migrate them to destination CVMs.

## Features

Currently, online migration supports the server migration feature.

## Starting Migration

<dx-alert infotype="explain" title="">
Currently, the online migration service in the console is in beta test. To try it out, [contact us](https://intl.cloud.tencent.com/document/product/213/34837) for application.
</dx-alert>


Online migration provides two migration methods: **migration in console** and **migration via tool**.
- Migration in console: you can easily and quickly view and manage migration sources and migration tasks in the online migration console. For more information, see [Migration in Console](https://intl.cloud.tencent.com/document/product/213/44338).
- Migration via tool: you can use the go2tencentcloud tool provided by Tencent Cloud for migration. For more information, see [Migration via Tool](https://intl.cloud.tencent.com/document/product/213/35640).

## FAQs

For more information, see [Service Migration](https://intl.cloud.tencent.com/document/product/213/32395).
