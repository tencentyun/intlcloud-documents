Online migration refers to migrating or synchronizing systems and applications on the source server or virtual machine from your IDCs or other cloud platforms to Tencent Cloud with no system downtime.
After the go2tencentcloud migration tool provided by Tencent Cloud is executed on the source server to be migrated, all systems and service applications running on the source server can be migrated to the destination CVM of Tencent Cloud. This migration tool can directly migrate source data to the cloud without the tedious preparations, such as creating, uploading, and importing images. It can meet enterprises' business requirements for cloud deployment, cross-cloud platform migration, cross-account or cross-region migration, and hybrid cloud deployment.

<dx-alert infotype="explain" title="">
The source server can be a physical server, a virtual machine, or a cloud server on another cloud platform, such as AWS, Google Cloud Platform, VMware, Alibaba Cloud, or Huawei Cloud.
</dx-alert>



## Scenarios

Online migration is applicable to the following scenarios (including but not limited to):
- IT architecture cloudification
- Hybrid cloud architecture deployment
- Cross-cloud migration
- Cross-account or cross-region migration

## Differences from Offline Migration

In offline migration, you need to create images for system disks or data disks on source servers, and then migrate images to Cloud Virtual Machine (CVM) or Cloud Block Storage (CBS) instances. You do not need to create images for online migration. Instead, you can run the migration tool on source servers to migrate them to the destination CVM instances.

## Starting Migration

- Importing the migration source on the client: Log in to the source server, run the go2tencentcloud tool provided by Tencent Cloud to import the migration source server to Tencent Cloud, and manage the migration source and complete the migration task by using the online migration feature in the CVM console. For more information, see [Operation Guide](https://www.tencentcloud.com/document/product/213/44338).
- Quick migration in the console: Create multiple migration tasks in the console and synchronize the operating system and programs of the source server to Tencent Cloud without logging in to the source server or downloading tools. For more information, see [Quick Migration Guide](https://intl.cloud.tencent.com/document/product/213/53265).


## FAQs

For more information, see [Service Migration](https://www.tencentcloud.com/document/product/213/32395).
