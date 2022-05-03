COS buckets are private by default. Identity verification is required for any access to COS, and object URLs used to access COS must carry signature information. However, if resources (buckets, objects, and folders) are configured with the Public Read permission, anonymous access is allowed, and users can use object URLs to download resources directly.

According to the permission application scope, COS allows users to set the Public Read permission at the bucket, object, or folder level.

## Setting the Permission of a Bucket to Public Read

If the permission of a bucket is set to Public Read/Private Write, all objects in the bucket can be accessed by anonymous users. For the setting method, see [Setting Access Permission](https://intl.cloud.tencent.com/document/product/436/13315).

## Setting the Permission of an Object to Public Read

If the permission of a specified object is set to Public Read/Private Write, the object can be accessed via the object URL. For the setting method, see [Setting Object Access Permission](https://intl.cloud.tencent.com/document/product/436/13327).

## Setting the Permission of a Folder to Public Read

If the permission of a folder is set to Public Read/Private Write, all files in the folder can be accessed by anonymous users. For the setting method, see [Setting Folder Permissions](https://intl.cloud.tencent.com/document/product/436/35261).

## Public Read Permission Evaluation Mechanism

For the COS permission evaluation mechanism, see [Access Policy Evaluation Process](https://intl.cloud.tencent.com/document/product/436/35240). If the Public Read permission settings for buckets, folders, and objects conflict, the priorities are as follows:

The ACL of an object has the highest priority. If the ACL of an object is inherited, the ACL of the corresponding folder applies. If the ACL of a folder is inherited, the ACL of the corresponding bucket applies.
