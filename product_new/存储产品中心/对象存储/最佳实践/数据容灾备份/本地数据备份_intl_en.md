## Overview

This document describes how to back up local data to the cloud. COS provides the following three methods to facilitate backup of local data to a COS bucket:

- Backup based on file sync through COSBrowser
- Backup based on online migration through COS Migration
- Backup based on offline migration through CDM

## Backup Based on File Sync

COSBrowser is a visual cloud file manager launched by COS that allows you to easily view, transfer, and manage COS resources through simple interactions. Currently, COSBrowser is available in Desktop Edition and Mobile Edition. For more information, please see [COSBrowser Overview](https://intl.cloud.tencent.com/document/product/436/11366).

COSBrowser Desktop Edition has a file sync feature that can be used to sync and upload local files to the cloud by associating local folders with buckets.

<img src="https://main.qcloudimg.com/raw/fc3160ec43b732936152ccf4f5f107c8.png" style="zoom:60%;" />

#### Usage

For more information, please see [COSBrowser Instructions](https://intl.cloud.tencent.com/document/product/436/32565#synchronization).

## Online Migration Scheme

COS Migration is an all-in-one tool integrating COS data migration features. You can migrate data to COS quickly after completing simple configurations.

#### Use cases

If you have a local IDC, COS Migration can help you migrate massive amounts of local data to COS.

#### Usage

For more information, please see [COS Migration](https://intl.cloud.tencent.com/document/product/436/32974#cos).

## Offline Migration Scheme

CDM uses a dedicated offline migration device provided by Tencent Cloud to help you migrate your local data to the cloud, solving the problems that arise from online migration from a local IDC to cloud, such as long time, high costs, and low security.

You can determine how to migrate data based on the data volume, IDC egress bandwidth, IDC idle server resources, acceptable completion time, and other factors. The estimated time needed for online migration is shown in the figure below. As can be seen, if data migration needs to take more than 10 days or the amount of data to be migrated exceeds 50 TB, you are recommended to use [CDM](https://intl.cloud.tencent.com/document/product/436/32974#cdm) for offline migration.

![](https://main.qcloudimg.com/raw/321d9e3f6a0a1f812da5f87792621093.png)

#### Usage

For more information, please see [CDM](https://intl.cloud.tencent.com/document/product/436/32974#cdm)

