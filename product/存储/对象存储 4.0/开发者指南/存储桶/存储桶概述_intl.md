## Definition

A bucket is a carrier of objects, which can be considered as a "container" for storing objects. You can manage buckets and configure attributes for buckets through various methods such as the Tencent Cloud Console, APIs, and SDKs. For example, you can set a bucket to be used for static website hosting or set access permission for a bucket.
For more information on bucket configuration, see the following topics: 

-  [Creating a Bucket](https://intl.cloud.tencent.com/document/product/436/13309)
-  [Setting up a Static Website](https://intl.cloud.tencent.com/document/product/436/14984)
-  [Setting Access Permission](https://intl.cloud.tencent.com/document/product/436/13315)
-  [Setting Hotlink Protection](https://intl.cloud.tencent.com/document/product/436/13319)

### Region
Region is where the COS IDC is located. COS allows users to create buckets in different regions. You can select the region closest to the location where you deploy your business for the buckets so as to reduce latency and cost, and meet the compliance requirements.

For example, if your business is distributed in South China, creating buckets in the Guangzhou region can accelerate object upload and download. For specific regions, see [Region and Access Domain Name](https://intl.cloud.tencent.com/document/product/436/6224).

>A region must be specified when a bucket is created, and cannot be modified once specified. All objects in the bucket are stored in the IDC in the region. You cannot set regions for objects.

## Naming Conventions

A bucket name consists of two parts: **user-defined string** and **system-generated numeric string (APPID)**, which are connected by a dash ("-"). For example, in the bucket name `examplebucket-1250000000`, examplebucket is a user-defined string, and 1250000000 is a system-generated numeric string (APPID). In the bucket name examples of API and SDK, the naming format of a bucket is: `<BucketName-APPID>`.

-  System-generated numeric string [APPID](https://intl.cloud.tencent.com/document/product/436/18507#appid): Automatically assigned by the system, and you do not need to specify it. It is unique in Tencent Cloud.
-  User-defined string: A string of characters entered manually by a user, as specified below.

Naming convention for user-defined strings:

-  You can only use lowercase letters [a-z], numbers [0-9], underscore "-" and the combination of them.
-  The length of a user-defined string cannot exceed 40 characters.
-  A bucket name cannot begin or end with "-".

The following are examples of valid bucket names:

- mybucket123-1250000000
- 1-newproject-1250000000

## Type of Access

Three types of bucket access permissions are available by default: "Private Read/Write", "Public Read/Private Write" and "Public Read/Write". You can modify bucket access permissions in **Permission Management** of the bucket in the COS Console. For more information, see [Basic Concepts of Access Control](https://intl.cloud.tencent.com/document/product/436/30581).

-  Private Read/Write
  Only the creator of the bucket and the authorized accounts has read and write permissions to the objects in the bucket. The default access permission of a bucket is Private Read/Write, which is recommended.
-  Public Read/Private Write
  Anyone (including anonymous visitors) has read permission to the objects in the bucket, but only the bucket creator and the authorized accounts have write permission to the objects in the bucket.
-  Public Read/Write
  Anyone (including anonymous visitors) has read and write permissions to the objects in the bucket. (Not recommended)

## Description

-  In COS that comes with no folders, objects are stored in a flat structure. For more information, see [Folder and Directory](https://intl.cloud.tencent.com/document/product/436/13324#.E6.96.87.E4.BB.B6.E5.A4.B9.E5.92.8C.E7.9B.AE.E5.BD.95).
-  A maximum of 200 buckets can be created under one user account (for all regions), but there is no limit on the number of objects in a bucket.
-  In Tencent Cloud COS, the bucket name under one APPID is unique.
-  Once a bucket is created, it cannot be renamed. To rename a bucket, you need to delete it and create another one with the desired name.
-  When creating a bucket, make sure to select the desired region, since the region cannot be changed once specified.


