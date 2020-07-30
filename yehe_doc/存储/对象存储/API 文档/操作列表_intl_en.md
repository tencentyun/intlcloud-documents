COS APIs are as detailed below:

## Service APIs

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | ---------------------------- |
| [GET Service (List Buckets)](https://intl.cloud.tencent.com/document/product/436/8291) | Querying bucket list | Queries the list of all buckets under specified account |

## Bucket APIs

#### Basic operation APIs

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------------------- |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | Creating bucket | Creates bucket under specified account |
| [GET Bucket (List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying object list | Queries some or all objects in bucket |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | Checking bucket and its permission | Checks whether a bucket exists and you have permission to access it |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | Deleting bucket | Deletes empty bucket under specified account |
| [GET Bucket Object versions](https://intl.cloud.tencent.com/document/product/436/31551) | Querying object version | Queries some or all objects in bucket and their historical version information |


#### Access control (acl) APIs

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | ------------------------------ |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | Setting bucket ACL | Sets ACL for specified bucket |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | Querying bucket ACL | Queries the ACL of bucket |



#### Cross-domain resource sharing (cors) APIs

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | ---------------------------- |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting cross-origin access configuration | Sets the cross-origin access permission of bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying cross-origin access configuration | Queries the cross-origin access configuration information of bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting cross-origin access configuration | Deletes the cross-origin access configuration information of bucket |

#### Custom domain name (domain) APIs

| API | Operation | Description |
|---------|---------|---------|
| [PUT Bucket domain](https://intl.cloud.tencent.com/document/product/436/35868) | Setting custom domain name | Sets custom domain name information for bucket |	
| [GET Bucket domain](https://intl.cloud.tencent.com/document/product/436/35869)	| Querying custom domain name 	| Queries the custom domain name information of bucket |
| [DELETE Bucket domain](https://intl.cloud.tencent.com/document/product/436/35870) | Deleting custom domain name | Deletes the custom domain name information of bucket |


#### Lifecycle APIs

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | ---------------------------- |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting lifecycle | Sets the lifecycle management configuration of bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying lifecycle | Queries the lifecycle management configuration of bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting lifecycle | Deletes the lifecycle management configuration of bucket |



#### Bucket policy (policy) APIs

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | ------------------------ |
| [ PUT Bucket policy](https://intl.cloud.tencent.com/document/product/436/8282) | Setting bucket policy | Sets permission policy for specified bucket |
| [GET Bucket policy](https://intl.cloud.tencent.com/document/product/436/8276) | Querying bucket policy | Queries the permission policy of specified bucket |
| [DELETE Bucket policy](https://intl.cloud.tencent.com/document/product/436/8285) | Deleting bucket policy | Deletes the permission policy of specified bucket |


#### Hotlink protection (referer) APIs

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------------ | ----------------------------------- |
| [PUT Bucket referer](https://intl.cloud.tencent.com/document/product/436/31423) | Setting bucket referer | Sets bucket referer allowlist or blocklist |
| [GET Bucket referer](https://intl.cloud.tencent.com/document/product/436/30615) | Querying bucket referer | Queries bucket referer allowlist or blocklist |



#### Bucket tag (tagging) APIs

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8281) | Setting bucket tag | Sets tag for existing bucket |
| [GET Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8277) | Querying bucket tags | Queries the existing tags of specified bucket |
| [DELETE Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8286) | Deleting bucket tag | Deletes specified bucket tag |



#### Static website (website) APIs

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ---------------- | ---------------------------------- |
| [PUT Bucket website](https://intl.cloud.tencent.com/document/product/436/30617) | Setting static website | Configures static website for bucket |
| [GET Bucket website](https://intl.cloud.tencent.com/document/product/436/30616) | Querying static website configuration | Queries the configuration information of static website associated with bucket |
| [DELETE Bucket website](https://intl.cloud.tencent.com/document/product/436/30629) | Deleting static website configuration | Deletes the static website configuration information of specified bucket |


#### Inventory APIs

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | ---------------------------- |
| [PUT Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30625) | Setting inventory job | Creates inventory job in bucket |
| [GET Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30623) | Querying inventory jobs | Queries the configuration information of specified inventory for bucket |
|  [List Bucket Inventory Configurations](https://intl.cloud.tencent.com/document/product/436/30627)  | Querying all inventories | Queries all inventory jobs of bucket |
| [DELETE Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30626) | Deleting inventory job | Deletes the specified inventory job of bucket |

#### Versioning APIs

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | -------------------------------- |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Enables or suspends versioning for bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning information of bucket |

#### Cross-region replication (replication) APIs

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------------ |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting cross-region replication | Configures cross-region replication rule for bucket with versioning enabled |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying cross-region replication | Queries the cross-region replication configuration information of bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting cross-region replication | Deletes the cross-region replication configuration information of bucket |

#### Log management (logging) APIs

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | -------------------------- |
| [PUT Bucket logging](https://intl.cloud.tencent.com/document/product/436/17054) | Setting log management | Enables logging for source bucket |
| [GET Bucket logging](https://intl.cloud.tencent.com/document/product/436/17053) | Querying log management | Queries the logging configuration information of source bucket |

#### Global acceleration (Accelerate) APIs

| API | Operation Name | Operation Description |
| ---------------------- | ------------ | -------------------------- |
| [PUT Bucket Accelerate](https://intl.cloud.tencent.com/document/product/436/33411)|  Setting global acceleration  |  Enables or suspends global acceleration for specified bucket
| [GET Bucket Accelerate](https://intl.cloud.tencent.com/document/product/436/33412)|  Querying global acceleration   |  Queries the global acceleration configuration information of specified bucket  |


#### Bucket encryption (encryption) APIs

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | ------------------------------ |
| [PUT Bucket encryption](https://intl.cloud.tencent.com/document/product/436/33459) | Setting bucket encryption | Sets default encryption configuration for specified bucket |
| [GET Bucket encryption](https://intl.cloud.tencent.com/document/product/436/33460) | Querying bucket encryption | Queries the default encryption configuration of specified bucket |
| [DELETE Bucket encryption](https://intl.cloud.tencent.com/document/product/436/33461) | Deleting bucket encryption configuration | Deletes the default encryption configuration of specified bucket |



## Object APIs

#### Basic operation APIs

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | ---------------------------------------- |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Simply uploading object | Uploads object to bucket |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Setting object replication | Copies file to destination path |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | Uploading object by using form | Uploads object by using form request |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading object | Downloads object to local file system |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of object |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting one object | Deletes specified object in bucket |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from bucket in one single request |
| [OPTIONS Object](https://intl.cloud.tencent.com/document/product/436/8288) | Pre-requesting cross-origin configuration | Uses pre-request to confirm whether a real cross-origin request can be sent |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring archived object | Retrieves archived object for access |
| [SELECT Object Content](https://intl.cloud.tencent.com/document/product/436/32360) | Extracting object content | Extracts the content of specified object |

#### Access control APIs

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | ---------------------------------- |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting object ACL | Sets ACL for specified object in bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying object ACL | Queries the ACL of object |

#### Object tag APIs

| API | Operation Name | Operation Description |
| ----------- | ------------ | --------- |
| [PUT Object tagging](https://intl.cloud.tencent.com/document/product/436/35709) | Sets object tag | Sets tag for uploaded object       |
| [GET   Object tagging](https://intl.cloud.tencent.com/document/product/436/35710) | Queries object tag | Queries the existing tag of specified object |
| [DELETE   Object tagging](https://intl.cloud.tencent.com/document/product/436/35711) | Deletes object tag | Deletes the existing tag of specified object |

#### Multipart upload APIs

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing multipart upload | Initializes multipart upload job |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading part | Uploads file part |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying part | Copies object as part |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing multipart upload | Completes the multipart upload of entire file |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting multipart upload | Aborts multipart upload operation and deletes uploaded parts |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart upload | Queries the information of multipart upload in progress |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries uploaded parts in specified multipart upload operation |


## Batch Operation (batch) APIs

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------------------ |
| [CreateJob](https://intl.cloud.tencent.com/document/product/436/33781) | Creating job       | Creates batch operation job in bucket                 |
| [DescribeJob](https://intl.cloud.tencent.com/document/product/436/33782) | Describing job | Gets the parameters and job execution status of created batch operation job |
| [ListJobs](https://intl.cloud.tencent.com/document/product/436/33783) | Querying jobs | Lists created batch operation jobs |
| [UpdateJobPriority](https://intl.cloud.tencent.com/document/product/436/33784) | Updating job priority | Updates the priority of created job |
| [UpdateJobStatus](https://intl.cloud.tencent.com/document/product/436/33785) | Updating job status | Updates the status of created job |


## Data Processing APIs         

#### Basic image processing APIs


| API  | Description |
| ---- | -------- |
| [Scaling](https://intl.cloud.tencent.com/document/product/436/36366) | Scales image                                         |
| [Cropping](https://intl.cloud.tencent.com/document/product/436/36367) | Crops image, including regular cropping, scaling and cropping, inscribed circle cropping, rounded corner cropping, and smart cropping |
| [Rotation](https://intl.cloud.tencent.com/document/product/436/36368) | Rotates image, including common rotation and adaptive rotation                     |
| [Format conversion](https://intl.cloud.tencent.com/document/product/436/36369) | Performs format conversion, GIF format optimization, and progressive display for image                  |
| [Quality conversion](https://intl.cloud.tencent.com/document/product/436/36370) | Adjusts image quality                                           |
| [Gaussian blurring](https://intl.cloud.tencent.com/document/product/436/36371) | Blurs image                                           |
| [Sharpening](https://intl.cloud.tencent.com/document/product/436/36372) | Sharpens image                                               |
| [Image Watermark](https://intl.cloud.tencent.com/document/product/436/36373) | Watermarks image                                           |
| [Text watermark](https://intl.cloud.tencent.com/document/product/436/36374) | Watermarks image with real-time text                                   |
| [Getting basic image information](https://intl.cloud.tencent.com/document/product/436/36375) | Queries the basic information of image, such as format, length, and width                         |
| [Getting image EXIF](https://intl.cloud.tencent.com/document/product/436/36376) | Queries EXIF information                                               |
| [Getting image average hue](https://intl.cloud.tencent.com/document/product/436/36377) | Queries the average hue information of image                                           |
| [Removing metadata](https://intl.cloud.tencent.com/document/product/436/36378) | Removes image metadata, including EXIF information                               |
| [Quick thumbnail template](https://intl.cloud.tencent.com/document/product/436/36379) | Generates thumbnail through image processing template                           |
| [Pipeline operator](https://intl.cloud.tencent.com/document/product/436/36380) | Performs multiple operations in sequence on image                                  |

#### Content audit APIs

| API  | Description |
| ---- | -------- |
| [Content audit](https://intl.cloud.tencent.com/document/product/436/37399)  | Scans existing COS data for pornographic, politically sensitive, terrorism, and marketing images and videos                            |


