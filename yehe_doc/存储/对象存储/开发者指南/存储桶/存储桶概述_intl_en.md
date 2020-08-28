## Definition

A bucket is a carrier of objects, which can be considered as a "container" for storing objects. You can manage buckets and configure attributes of buckets in various methods such as the Tencent Cloud Console, APIs, and SDKs. For example, you can set a bucket for hosting a static website or set access permission to a bucket. For more information on bucket configuration, see the topics below: 
- [Creating a Bucket](https://intl.cloud.tencent.com/document/product/436/13309)
- [Setting up a Static Website](https://intl.cloud.tencent.com/document/product/436/14984)
- [Setting Access Permission](https://intl.cloud.tencent.com/document/product/436/13315)
- [Setting Hotlink Protection](https://intl.cloud.tencent.com/document/product/436/13319)

#### Region
Region is where the COS IDC is located. COS allows users to create buckets in different regions. You can select the region closest to the location where you deploy your business for the buckets so as to reduce latency and cost, and meet the compliance requirements.

For example, if your business is distributed in South China, creating buckets in the Guangzhou region can accelerate object uploads and downloads. For more information on regions, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224).

> It is a must to specify a region when creating a bucket, and the specification is inalterable. All objects in the bucket are stored in the IDC in the region. You cannot set regions on the objects level.

## Naming Conventions

A bucket name consists of two parts: **user-defined string** and **system-generated numeric string (APPID)**, which are connected by a dash ("-"). For example, in the bucket name `examplebucket-1250000000`, examplebucket is the user-defined string, and 1250000000 is the system-generated numeric string (APPID).
In the bucket name examples for APIs and SDKs, the naming format of a bucket is `<BucketName-APPID>`.

- System-generated numeric string ([APPID](https://intl.cloud.tencent.com/document/product/436/18507): automatically assigned by the system, which you do not need to specify and is unique in Tencent Cloud.
- User-defined string: a string of characters entered manually by you, as specified below.

Naming convention for user-defined strings:

- You can only use lowercase letters [a-z], numbers [0-9], dashes "-", or a combination of them.
- The length of a user-defined string cannot exceed 50 characters.
- A bucket name cannot begin or end with "-".

The following are examples of valid bucket names:

- mybucket123-1250000000
- 1-newproject-1250000000

## Types of Permission

A bucket provides two types of permissions by default: public and user.

### Public permissions
Public permissions include "Private Read/Write", "Public Read/Private Write", and "Public Read/Write". You can modify bucket access permissions in **Permission Management** of the bucket in the COS Console. For more information, see [Basic Concepts of Access Control](https://intl.cloud.tencent.com/document/product/436/30581).

- Private Read/Write
  Only the creator of the bucket and authorized accounts have Read/Write permission to the objects in the bucket. The default access permission of a bucket is Private Read/Write, which is recommended.
- Public Read/Private Write
  Anyone (including anonymous visitors) has Read permission to the objects in the bucket, but only the bucket creator and authorized accounts have Write permission to them.
- Public Read/Write
  Anyone (including anonymous visitors) has Read/Write permission to the objects in the bucket, which is not recommended.

### User permissions

A root account has all the permissions (full control) for buckets by default. In addition, you can add sub-accounts that are granted permissions to read/write data and Read/Write permissions, and even **full access** to buckets.


## Notes

- COS stores objects using a flat structure instead of folders. For more information, see “Folders and Directories” in [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324).
- Each root account (APPID) can create up to 200 buckets (not region-specific), and an unlimited number of objects. 
- In Tencent Cloud COS, the bucket name under one APPID must be unique.
- Once a bucket is created, it cannot be renamed. To rename a bucket, you need to delete it and create another one with the desired name.
- When creating a bucket, make sure to select the desired region, as the region cannot be changed once specified.

