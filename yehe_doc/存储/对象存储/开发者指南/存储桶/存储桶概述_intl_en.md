## Overview

Bucket is the carrier of objects, which can be understood as the "container" for storing objects, and this "container" has no upper limit of capacity. Objects are stored in buckets in a flat structure with no concept of folders and directories. You can choose to store objects in one or multiple buckets.

>?A bucket can contain any number of objects, but one root account can create only up to 200 buckets.


## Bucket Naming Conventions

A bucket name consists of BucketName and APPID connected by a hyphen (-). For example, in the bucket name `examplebucket-1250000000`, examplebucket is the user-defined string, and 1250000000 is the system-generated numeric string (APPID). In API and SDK samples, the naming format of a bucket is `<BucketName-APPID>`.


- BucketName: a custom string of characters in the following conventions:
 - Only lowercase letters (a-z), digits (0-9), and hyphens (-) are allowed.
 - The length of a user-defined string cannot exceed 50 characters.
 - A bucket name cannot start or end with "-".
- [APPID](https://intl.cloud.tencent.com/document/product/436/18507): the account you get after you successfully register in Tencent Cloud. It is automatically assigned by the system as a unique permanent ID, which can be viewed in [Account Information](https://console.cloud.tencent.com/developer). When creating a bucket in the console, you don't need to enter it; however, when using tools, APIs, and SDKs, you need to specify it.


The following are examples of valid bucket names:

- examplebucket-1-1250000000
- mybucket123-1250000000
- 1-newproject-1250000000


## Bucket Region
Region is where a COS IDC is located. COS allows you to create buckets in different regions. You can select the region closest to the location where your business is deployed for the buckets so as to reduce latency and cost and meet the compliance requirements.

For example, if your business is distributed in South China, creating buckets in the Guangzhou region can accelerate object uploads and downloads. For more information on regions, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224).

>!A region must be specified when a bucket is created and cannot be modified once specified. All objects in the bucket are stored in the IDC in the region. You cannot set regions for objects.




## Permission Types

A bucket provides two types of permissions by default: public and user.

### Public permissions
Public permissions include "Private Read/Write", "Public Read/Private Write", and "Public Read/Write". You can modify bucket access permissions in **Permission Management** of the bucket in the COS console. For more information, please see [Basic Concepts of Access Control](https://intl.cloud.tencent.com/document/product/436/30581).

- Private read/write
  Only the creator of the bucket and authorized accounts have Read/Write permission to the objects in the bucket. The default access permission of a bucket is Private Read/Write, which is recommended.
- Public Read/Private Write
  Anyone (including anonymous visitors) has Read permission to the objects in the bucket, but only the bucket creator and authorized accounts have Write permission to them.
- Public Read/Write
  Anyone (including anonymous visitors) has read/write permission to the objects in the bucket, which is not recommended.

### User permissions

The root account has all the permissions of the bucket by default (i.e., full access). In COS, sub-accounts can be added to read/write data, read/write permissions, and have the full access.


## Bucket Operations


You can manage buckets and configure attributes of buckets in various methods such as the Tencent Cloud console, tools, APIs, and SDKs. For example, you can set a bucket for hosting a static website or set access permission to a bucket. The following documents describe how to configure some features. For more information on bucket configuration, please see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). 
- [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309)
- [Setting up a Static Website](https://intl.cloud.tencent.com/document/product/436/14984)
- [Setting Access Permission](https://intl.cloud.tencent.com/document/product/436/13315)
- [Setting Hotlink Protection](https://intl.cloud.tencent.com/document/product/436/13319)



## Notes

- COS stores objects in a flat structure with no traditional folder concept. For more information, please see the Folder and Directory section in [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324).
- Each root account (i.e., the same APPID) can create up to 200 buckets in total in all regions. There is no limit on the number of objects in a bucket.
- In Tencent Cloud COS, the bucket name under one APPID must be unique.
- Once a bucket is created, it cannot be renamed. To rename a bucket, you need to delete it and create another one with the desired name.
- When creating a bucket, make sure to select the desired region, as the region cannot be changed once specified.