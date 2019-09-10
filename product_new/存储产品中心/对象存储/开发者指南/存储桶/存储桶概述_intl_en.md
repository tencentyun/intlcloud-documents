## Definition

A bucket is a carrier of objects, which can be considered as a "container" for storing objects. You can manage buckets and configure attributes of buckets in various methods such as the Tencent Cloud Console, APIs, and SDKs. For example, you can set a bucket for hosting a static website or set access permission to a bucket. For more information on bucket configuration, see the topics below: 
- [Creating a Bucket](https://intl.cloud.tencent.com/document/product/436/13309)
- [Setting up a Static Website] (https://intl.cloud.tencent.com/document/product/436/14984)
- [Setting Access Permission](https://intl.cloud.tencent.com/document/product/436/13315)
- [Setting Hotlink Protection](https://intl.cloud.tencent.com/document/product/436/13319)

#### Region
Region is where a COS IDC is located. COS allows you to create buckets in different regions. You can select the region closest to the location where your business is deployed for the buckets so as to reduce latency and cost and meet the compliance requirements.

For example, if your business is distributed in South China, creating buckets in the Guangzhou region can accelerate object uploads and downloads. For more information on regions, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224).

> It is a must to specify a region when creating a bucket, and the specification is inalterable. All objects in the bucket are stored in the IDC in the region. You cannot set regions on the objects level.

## Naming Conventions

A bucket name consists of two parts: **user-defined string** and **system-generated numeric string (APPID)**, which are connected by a dash ("-"). For example, in the bucket name `examplebucket-1250000000`, examplebucket is the user-defined string, and 1250000000 is the system-generated numeric string (APPID).
In the bucket name examples for APIs and SDKs, the naming format of a bucket is `<BucketName-APPID>`.

- System-generated numeric string ([APPID](https://intl.cloud.tencent.com/document/product/436/18507#appid): automatically assigned by the system, which you do not need to specify and is unique in Tencent Cloud.
- User-defined string: a string of characters entered manually by you, as specified below.

Naming convention for user-defined strings:

- You can only use lowercase letters [a-z], numbers [0-9], dashes "-", or a combination of them.
- The length of a user-defined string cannot exceed 40 characters.
- A bucket name cannot begin or end with "-".

The following are examples of valid bucket names:

- mybucket123-1250000000
- 1-newproject-1250000000

## Type of Access

Three types of bucket access permissions are available by default, i.e., "Private Read/Write", "Public Read/private Write", and "Public Read/Write". You can modify bucket access permissions in **Permission Management** of the bucket in the COS Console. For more information, see [Basic Concepts of Access Control](https://intl.cloud.tencent.com/document/product/436/30581).
- Private Read/Write
  Only the creator of the bucket and authorized accounts have Read/Write permission to the objects in the bucket. The default access permission of a bucket is Private Read/Write, which is recommended.
- Public Read/Private Write
  Anyone (including anonymous visitors) has Read permission to the objects in the bucket, but only the bucket creator and authorized accounts have Write permission to them.
- Public Read/Write
  Anyone (including anonymous visitors) has Read/Write permission to the objects in the bucket, which is not recommended.

## Descriptions

- COS stores objects in a flat structure with no traditional folder concept. For more information, see the Folder and Directory section in [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324#.E6.96.87.E4.BB.B6.E5.A4.B9.E5.92.8C.E7.9B.AE.E5.BD.95).
- You can create up to 200 buckets in total in all regions with one account. There is no limit on the number of objects in a bucket.
- In Tencent Cloud COS, the bucket name under one APPID must be unique.
- Once a bucket is created, it cannot be renamed. To rename a bucket, you need to delete it and create another one with the desired name.
- When creating a bucket, make sure to select the desired region, as the region cannot be changed once specified.

