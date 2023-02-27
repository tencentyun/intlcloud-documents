## Overview

A bucket is the carrier of objects, which can be understood as the "container" for storing objects, and this "container" has no upper limit of capacity. Objects are stored in buckets in a flat structure with no concept of folders and directories. You can choose to store objects in one or multiple buckets.

>? A bucket can contain any number of objects, but one root account can create only up to 200 buckets.
>


## Bucket Naming Conventions

A bucket name consists of BucketName and APPID connected by a hyphen (-). For example, in the bucket name `examplebucket-1250000000`, examplebucket is the user-defined string, and 1250000000 is the system-generated numeric string (APPID). In API and SDK samples, the naming format of a bucket is `<BucketName-APPID>`.


- BucketName: a custom string of characters in the following conventions:
 - Only lowercase letters (a-z), digits (0-9), and hyphens (-) are allowed.
 - The number of characters a bucket name is allowed to contain is limited by the length of the **[region abbreviation](https://intl.cloud.tencent.com/document/product/436/6224)** and **APPID**. The combined domain name can be up to 60 characters. For example, the domain name `123456789012345678901-1250000000.cos.ap-beijing.myqcloud.com` contains 60 characters.
 - A bucket name cannot start or end with "-".
- [APPID](https://intl.cloud.tencent.com/document/product/436/18507): the account you get after you successfully register in Tencent Cloud. It is automatically assigned by the system as a unique permanent ID, which can be viewed in [Account Information](https://console.cloud.tencent.com/developer). When creating a bucket in the console, you don't need to enter it; however, when using tools, APIs, and SDKs, you need to specify it.


The following are examples of valid bucket names:

- examplebucket-1-1250000000
- mybucket123-1250000000
- 1-newproject-1250000000


## Bucket Region
Region is where the COS IDC is located. COS allows users to create buckets in different regions. You can select the region closest to the location where you deploy your business for the buckets so as to reduce latency and cost, and meet the compliance requirements.

For example, if your business is distributed in South China, creating buckets in the Guangzhou region can accelerate object uploads and downloads. For more information on regions, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224).

>! A region must be specified when a bucket is created and cannot be modified once specified. All objects in the bucket are stored in the IDC in the region. You cannot set regions for objects.
>


## Types of Permission

A bucket provides two types of permissions by default: public and user.

>?
>- If the bucket permission is private read/write or a specified account is granted the permission, an object request needs to carry a signature for identity verification. For more information on signature, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
>- If the bucket permission is public read/private write or public read/write, an object request doesn't need to carry a signature, and anonymous users can directly access the object at the URL. However, your data may be leaked. Therefore, proceed with caution.



### Public permissions
Public permissions include "Private Read/Write", "Public Read/Private Write", and "Public Read/Write". You can modify bucket access permissions in **Permission Management** of the bucket in the COS console. For more information, see [Basic Concepts of Access Control](https://intl.cloud.tencent.com/document/product/436/30581).

- Private Read/Write
  Only the creator of the bucket and authorized accounts have Read/Write permission on the objects in the bucket. The default access permission of a bucket is Private Read/Write, which is recommended.
- Public Read/Private Write
  Anyone (including anonymous visitors) has Read permission on the objects in the bucket, but only the bucket creator and authorized accounts have Write permission on them.
- Public Read/Write
  Anyone (including anonymous visitors) has Read/Write permission on the objects in the bucket, which is not recommended.

### User permissions

A root account has all the permissions (full access) for buckets by default. In addition, you can add sub-accounts that are granted permissions to read/write data and permissions, and even full access.




## Bucket Operations


You can manage buckets and configure attributes of buckets in various methods such as the Tencent Cloud console, tools, APIs, and SDKs. For example, you can set a bucket for hosting a static website or set access permission on a bucket. The following documents describe how to configure some features. For more information on bucket configuration, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). 
- [Creating a Bucket](https://intl.cloud.tencent.com/document/product/436/13309)
- [Setting Up a Static Website](https://intl.cloud.tencent.com/document/product/436/14984)
- [Setting Access Permission](https://intl.cloud.tencent.com/document/product/436/13315)
- [Setting Hotlink Protection](https://intl.cloud.tencent.com/document/product/436/13319)



## Notes

- COS stores objects using a flat structure instead of folders. For more information, see “Folders and Directories” in [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324).
- Each root account (i.e., the same APPID) can create up to 200 buckets in total in all regions. There is no limit on the number of objects in a bucket.
- In Tencent Cloud COS, the bucket name under one APPID must be unique.
- Once a bucket is created, it cannot be renamed. To rename a bucket, you need to delete it and create another one with the desired name.
- When creating a bucket, make sure to select the desired region, as the region cannot be changed once specified.

