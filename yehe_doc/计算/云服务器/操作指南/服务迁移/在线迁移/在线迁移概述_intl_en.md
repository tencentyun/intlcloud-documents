

Online migration is a service migration method that can migrate systems and applications on source servers from your own IDC or cloud platform to Tencent Cloud. It meets service requirements for enterprise cloudification, migration across cloud platforms, migration across accounts or regions, and hybrid cloud deployment.
> Here, the source server can be a physical server, a virtual machine, or even a cloud server on another cloud platform, such as AWS, Microsoft Azure, Google Cloud Platform, Alibaba Cloud, or Huawei Cloud.
>

## Scenarios

Online migration is applicable to the following scenarios:
- IT architecture cloudification
- Hybrid cloud architecture deployment
- Cross-cloud migration
- Cross-account or cross-region migration

## Differences from Offline Migration

In offline migration, system disks or data disks on the source server are made into an image, and then the image is migrated to your designated Cloud Virtual Machine (CVM) or Cloud Block Storage (CBS). In contrast, the preparation of images is not required for online migration. Instead, you only need to run the migration tool on the source server to migrate the source server to your designated CVM.

## Features

Currently, online migration supports the server migration feature.

## Preparations

- Register a Tencent Cloud account and prepare the destination CVM.
- Stop applications on the source server to avoid potential impact from migration on existing applications.
[Click here](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) to download the compressed migration tool package.

## FAQs

For more information, see [About Service Migration](https://intl.cloud.tencent.com/document/product/213/32395).
