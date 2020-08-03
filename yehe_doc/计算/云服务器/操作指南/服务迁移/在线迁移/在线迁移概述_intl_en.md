

Online migration is a service migration method that can migrate systems and applications on source servers from your IDCs or other cloud platforms to Tencent Cloud. It meets the business requirements for enterprise cloudification, cross-cloud migration, cross-account or cross-region migration, and hybrid cloud deployment.
> The source server can be a physical server, a virtual machine, or a cloud server on another cloud platform, such as AWS, Microsoft Azure, Google Cloud Platform, Alibaba Cloud, or Huawei Cloud.
>

## Scenarios

Online migration is applicable to the following scenarios:
- IT architecture cloudification
- Hybrid cloud architecture deployment
- Cross-cloud migration
- Cross-account or cross-region migration

## Differences from offline migration

In offline migration, you need to create images for system disks or data disks on source servers, and then migrate images to the Cloud Virtual Machine (CVM) or Cloud Block Storage (CBS). You do not need to create images for online migration. Instead, you can run the migration tool on source servers to migrate them to destination CVMs.

## Features

Currently, online migration supports the server migration feature.

## Preparations

- Register a Tencent Cloud account and prepare the destination CVM.
- Stop applications on the source server to prevent existing applications from being affected by the migration.
[Click here](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) to download the compressed migration tool package.

## FAQs

For more information, see [About Service Migration](https://intl.cloud.tencent.com/document/product/213/32395).
