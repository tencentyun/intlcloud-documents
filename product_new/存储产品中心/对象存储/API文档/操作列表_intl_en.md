Below are APIs of Cloud Object Storage (COS) and their descriptions:

## Service APIs

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ---------------------------- |
| [GET Service](https://intl.cloud.tencent.com/document/product/436/8291) | Querying bucket list | Queries the list of all buckets under the specified account |

## Bucket APIs

#### Basic Operation APIs

| API | Operation | Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates a bucket under the specified account |
| [GET Bucket（List Object）](https://intl.cloud.tencent.com/document/product/436/7734) | Querying object list | Queries some or all objects in a bucket |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | Checking a bucket and its permission | Check whether a bucket exists and you have permission to access it |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket under the specified account |

#### Access Control List (acl) APIs

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------ |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | Setting bucket ACL | Sets the ACL for the specified bucket |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | Querying bucket ACL | Queries the ACL of a bucket |



#### Cross-Origin Resource Sharing (cors) APIs

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------- |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting cross-origin access configuration | Sets the cross-origin access permission to a bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying cross-origin access configuration | Queries the cross-origin access configuration information of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting cross-origin access configuration | Deletes the cross-origin access configuration information of a bucket |



#### Lifecycle (lifecycle) APIs

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------- |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting lifecycle | Sets the lifecycle management configuration of a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying lifecycle | Queries the lifecycle management configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting lifecycle | Deletes the lifecycle management configuration of a bucket |



#### Bucket Policy (policy) APIs

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------ |
| [PUT Bucket policy](https://intl.cloud.tencent.com/document/product/436/8282) | Setting a bucket policy | Sets a permission policy for the specified bucket |
| [GET Bucket policy](https://intl.cloud.tencent.com/document/product/436/8276) | Querying bucket policy | Queries the permission policy of the specified bucket |
| [DELETE Bucket policy](https://intl.cloud.tencent.com/document/product/436/8285) | Deleting a bucket policy | Deletes the permission policy of the specified bucket |





#### Hotlink Protection (referer) APIs

| API | Operation | Description |
| ------------------------------------------------------------ | ------------------ | ----------------------------------- |
| [PUT Bucket referer](https://intl.cloud.tencent.com/document/product/436/31423) | Setting bucket referer | Sets Referer-based whitelist or blacklist for a bucket |
| [GET Bucket referer](https://intl.cloud.tencent.com/document/product/436/30615) | Querying bucket referer | Queries Referer-based whitelist or blacklist for a bucket |



#### Tag (tagging) APIs

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8281) | Setting a bucket tag | Sets a tag for an existing bucket |
| [GET Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8277) | Querying bucket tags | Queries the existing tags of the specified bucket |
| [DELETE Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8286) | Deleting a bucket tag | Deletes the specified bucket tag |



#### Static Website (website) APIs

| API | Operation | Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [PUT Bucket website](https://intl.cloud.tencent.com/document/product/436/30617) | Setting bucket website | Configures a static website for a bucket |
| [GET Bucket website](https://intl.cloud.tencent.com/document/product/436/30616) | Querying bucket website | Queries the configuration information of the static website associated with a bucket |
| [DELETE Bucket website](<https://intl.cloud.tencent.com/document/product/436/30629>) | Deleting bucket website | Deletes the configuration information of the static website of the specified bucket |



## Object APIs

#### Basic Operation APIs

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ---------------------------------------- |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Simply uploading an object | Uploads an object to a bucket |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Setting object copy | Copies a file to the destination path |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | Uploading an Object Using a Form | Uploads an object using a form request |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes the specified object in a bucket |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes objects in a bucket in batches |
| [OPTIONS Object](https://intl.cloud.tencent.com/document/product/436/8288) | Pre-requesting cross-origin configuration | Uses a pre-request to confirm whether a real cross-origin request can be sent |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Retrieves an archived object for access |



#### Access Control APIs

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------------- |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting object ACL | Sets the ACL for the specified object in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying object ACL | Queries the ACL of an object |



#### Multipart Upload APIs

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload task |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads file parts |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of the entire file |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload operation and deletes the uploaded parts |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying a multipart upload | Queries the information of a multipart upload in progress |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries uploaded parts in the specified multipart upload operation |
