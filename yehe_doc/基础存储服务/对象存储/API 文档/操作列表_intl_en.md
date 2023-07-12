COS APIs are described as follows:

## Service APIs

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ---------------------------- |
| [GET Service (List Buckets)](https://intl.cloud.tencent.com/document/product/436/8291) | Querying the bucket list | Queries the list of all buckets under a specified account |

## Bucket APIs

#### Basic operation APIs

| API | Operation | Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------------------- |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates a bucket under a specified account |
| [GET Bucket (List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying an object list | Queries some or all objects in a bucket |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | Checking a bucket and its permission | Checks whether a bucket exists and whether you have permission to access it |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket under a specified account |
| [GET Bucket Object versions](https://intl.cloud.tencent.com/document/product/436/31551) | Querying object versions | Queries some or all objects in a bucket and their historical versions |


#### ACL APIs

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------ |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | Setting a bucket ACL | Sets an ACL for a bucket |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | Querying a bucket ACL | Queries the ACL of a bucket |



#### CORS APIs

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------- |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting CORS | Sets CORS permissions for a bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying CORS configuration | Queries the CORS configuration of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting CORS configuration | Deletes the CORS configuration of a bucket |


#### Lifecycle APIs

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------- |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting lifecycle | Sets lifecycle for a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying a lifecycle configuration | Queries the lifecycle configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting a lifecycle configuration | Deletes the lifecycle configuration of a bucket |



#### Bucket policy APIs

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------ |
| [PUT Bucket policy](https://intl.cloud.tencent.com/document/product/436/8282) | Setting a bucket policy | Sets a permission policy for a bucket |
| [GET Bucket policy](https://intl.cloud.tencent.com/document/product/436/8276) | Querying a bucket policy | Queries the permission policy of a bucket |
| [DELETE Bucket policy](https://intl.cloud.tencent.com/document/product/436/8285) | Deleting a bucket policy | Deletes the permission policy of a bucket |


#### Hotlink Protection (referer) APIs

| API | Operation |  Description |
| ------------------------------------------------------------ | ------------------ | ----------------------------------- |
| [PUT Bucket referer](https://intl.cloud.tencent.com/document/product/436/31423) | Setting a bucket referer | Sets a bucket referer allowlist or blocklist |
| [GET Bucket referer](https://intl.cloud.tencent.com/document/product/436/30615) | Querying a bucket referer | Queries a bucket referer allowlist or blocklist |



#### Bucket tagging APIs

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8281) | Setting bucket tags | Sets tags for an existing bucket |
| [GET Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8277) | Querying bucket tags | Queries the existing tags of a bucket |
| [DELETE Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8286) | Deleting bucket tags | Deletes the tags of a bucket |



#### Static website APIs

| API | Operation | Description |
| ------------------------------------------------------------ | ---------------- | ---------------------------------- |
| [PUT Bucket website](https://intl.cloud.tencent.com/document/product/436/30617) | Setting a static website | Sets a static website for a bucket |
| [GET Bucket website](https://intl.cloud.tencent.com/document/product/436/30616) | Querying static website configuration | Queries the static website configuration of a bucket |
| [DELETE Bucket website](<https://intl.cloud.tencent.com/document/product/436/30629>) | Deleting a static website configuration | Deletes the static website configuration of a bucket |


#### INTELLIGENT TIERING APIs

| API | Operation | Description |
| ------------------------------------------------------------ | ---------------- | ---------------------------- |
| [PUT Bucket IntelligentTiering](https://intl.cloud.tencent.com/document/product/436/38314) | Setting INTELLIGENT TIERING | Enables INTELLIGENT TIERING for a bucket |
| [GET Bucket IntelligentTiering](https://intl.cloud.tencent.com/document/product/436/38315) | Querying INTELLIGENT TIERING configuration | Queries the INTELLIGENT TIERING configuration of a bucket |




#### Inventory APIs

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------- |
| [PUT Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30625) | Creating an inventory job | Creates an inventory job in a bucket |
|  [POST Bucket inventory](https://intl.cloud.tencent.com/document/product/436/46869)       |    Creating a one-time inventory job             |  Creates a one-time inventory job for a bucket  |
| [GET Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30623) | Querying inventory jobs | Queries an inventory configuration of a bucket |
|  [List Bucket Inventory Configurations](https://intl.cloud.tencent.com/document/product/436/30627) | Querying the list of inventory configurations | Queries the list of inventory configurations for a bucket |
| [DELETE Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30626) | Deleting an inventory job | Deletes an inventory job from a bucket |

#### Versioning APIs

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | -------------------------------- |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Enables/Suspends versioning for a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning information of a bucket |

#### Cross-bucket replication APIs

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------------ |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting cross-bucket replication | Sets a cross-bucket replication rule for a versioning-enabled bucket |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying cross-bucket replication | Queries the cross-bucket replication rule of a bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting a cross-bucket replication rule | Deletes a cross-bucket replication rule of a bucket |

#### Logging APIs

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | -------------------------- |
| [PUT Bucket logging](https://intl.cloud.tencent.com/document/product/436/17054) | Setting logging | Enables logging for a source bucket |
| [GET Bucket logging](https://intl.cloud.tencent.com/document/product/436/17053) | Querying logging configuration | Queries the logging configuration of a source bucket |

#### Global acceleration (accelerate) APIs

| API | Operation | Description |
| ---------------------- | ------------ | -------------------------- |
| [PUT Bucket Accelerate](https://intl.cloud.tencent.com/document/product/436/33411)| Setting global acceleration | Enables/Suspends global acceleration for a bucket |
| [GET Bucket Accelerate](https://intl.cloud.tencent.com/document/product/436/33412)| Querying global acceleration | Queries the global acceleration configuration of a bucket |



#### Bucket encryption APIs

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------ |
| [PUT Bucket encryption](https://intl.cloud.tencent.com/document/product/436/33459) | Setting bucket encryption | Sets the default encryption configuration for a bucket |
| [GET Bucket encryption](https://intl.cloud.tencent.com/document/product/436/33460) | Querying bucket encryption configuration | Queries the default encryption configuration of a bucket |
| [DELETE Bucket encryption](https://intl.cloud.tencent.com/document/product/436/33461) | Deleting bucket encryption configuration | Deletes the default encryption configuration of a bucket |



#### Object lock (ObjectLock) APIs


| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------ |
| [PUT Bucket ObjectLockConfiguration](https://intl.cloud.tencent.com/document/product/436/40133)|     Configuring object lock    |     Configures object lock for existing buckets   |
| [GET Bucket ObjectLockConfiguration](https://intl.cloud.tencent.com/document/product/436/40134)|     Querying object lock    |    Queries the object lock configuration that has taken effect    |
|[GET Object retention](https://www.tencentcloud.com/document/product/436/40135) | Querying the expiration date of object lock   |    Queries the expiration date of object lock     |


## Object APIs

#### Basic operation APIs

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ---------------------------------------- |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object in whole | Uploads an object to a bucket. |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object | Copies a file to the destination path. |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | Uploading an object using an HTML form | Uploads an object using an HTML form. |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object. |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting an object | Deletes an object from a bucket. |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from a bucket. |
| [OPTIONS Object](https://intl.cloud.tencent.com/document/product/436/8288) | Checking cross-origin resource sharing (CORS) configuration | Sends a preflight request to determine whether an actual CORS request can be sent. |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access |
| [SELECT Object Content](https://intl.cloud.tencent.com/document/product/436/32360) | Extracting object content | Extracts the content of an object |

#### ACL APIs

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------------- |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting an object ACL | Sets an ACL for an object in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying an object ACL | Queries the ACL of an object |

#### Object tagging APIs

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------- |
| [PUT   Object tagging](https://intl.cloud.tencent.com/document/product/436/35709) | Setting object tags | Sets tags for an uploaded object |
| [GET   Object tagging](https://intl.cloud.tencent.com/document/product/436/35710) | Querying object tags | Queries all tags of an object |
| [DELETE   Object tagging](https://intl.cloud.tencent.com/document/product/436/35711) | Deleting object tags | Deletes all tags of an object |

#### Multipart upload APIs

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload. |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads a file in parts. |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part. |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of a file. |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload and deletes the uploaded parts. |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries in-progress multipart uploads. |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries the uploaded parts of a multipart upload. |


## Batch Operation APIs

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------------------ |
| [CreateJob](https://intl.cloud.tencent.com/document/product/436/33781) | Creating a job | Creates a batch operation job in a bucket |
| [DescribeJob](https://intl.cloud.tencent.com/document/product/436/33782) | Describing a job | Gets the parameters and job execution status of a created batch operation job |
| [ListJobs](https://intl.cloud.tencent.com/document/product/436/33783) | Querying jobs | Lists created batch operation jobs |
| [UpdateJobPriority](https://intl.cloud.tencent.com/document/product/436/33784) | Updating job priority | Updates the priority of a created job |
| [UpdateJobStatus](https://intl.cloud.tencent.com/document/product/436/33785) | Updating job status | Updates the status of a created job |
|   [CommonElements](https://intl.cloud.tencent.com/document/product/436/33786)|—|   Common elements of the batch operation feature|
|  [ErrorResponse](https://intl.cloud.tencent.com/document/product/436/33787)|—|  Error responses of the batch operation feature|




## Data Processing APIs         


#### Data processing APIs

Data processing APIs include image processing, AI-based content recognition, media processing, and file processing APIs. For details, see [Data Processing APIs](https://www.tencentcloud.com/document/product/436/36364).



#### Content moderation APIs

Content moderation APIs includes image moderation, video moderation, audio moderation, text moderation, file moderation, webpage moderation, and live stream moderation APIs. For details, see [Content Moderation APIs](https://www.tencentcloud.com/document/product/436/48186).


#### Job and workflow APIs

Job and workflow APIs include workflow APIs, workflow instances, job APIs, template APIs, and batch job APIs. For details, see [Job and Workflow APIs](https://www.tencentcloud.com/document/product/436/46211).


#### Cloud virus detection APIs

| API | Description  |
| ---------------------------------------------- | -------------- |
|  [Submitting virus detection job](https://intl.cloud.tencent.com/document/product/436/50132) |  Detects viruses such as trojans and worms in COS files|
|  Querying virus detection job result | Queries the status or result of a virus detection job |







