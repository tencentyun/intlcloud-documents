COS APIs are as detailed below:

## Service APIs

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ---------------------------- |
| [GET Service (List Buckets)](https://intl.cloud.tencent.com/document/product/436/8291) | Querying a bucket list | Queries the list of all buckets under a specified account |

## Bucket APIs

#### Basic operation APIs

| API                                                          | Operation                   | Description                                       |
| ------------------------------------------------------------ | ------------------ | ---------------------------------------------- |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates a bucket under a specified account |
| [GET Bucket (List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying an object list | Queries some or all objects in a bucket |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | Extracting a bucket and its permission | Checks whether a bucket exists and you have permission to access it |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket under a specified account |
| [GET Bucket Object versions](https://intl.cloud.tencent.com/document/product/436/31551) | Querying object versions | Queries some or all objects in a bucket and their version history |


#### Access Control List (acl) APIs

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------ |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | Setting bucket ACL | Sets the ACL for a specified bucket |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | Querying bucket ACL | Queries the ACL of a bucket |



#### Cross-Origin Resource Sharing (cors) APIs

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------- |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting cross-origin access configuration | Sets cross-origin access permissions for a bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying cross-origin access configuration | Queries the cross-origin access configuration of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting cross-origin access configuration | Deletes the cross-origin access configuration of a bucket |

#### Custom domain APIs

| API | Operation | Description |
|---------|---------|---------|
| [PUT Bucket domain](https://intl.cloud.tencent.com/document/product/436/35868) | Setting a custom domain name | Sets a custom domain name for a bucket |	
| [GET Bucket domain](https://intl.cloud.tencent.com/document/product/436/35869) | Querying a custom domain name | Queries the custom domain name of a bucket |
| [DELETE Bucket domain](https://intl.cloud.tencent.com/document/product/436/35870) | Deleting a custom domain name | Deletes a custom domain name from a bucket|


#### Lifecycle APIs

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------- |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting lifecycle | Sets the lifecycle management configuration of a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying lifecycle | Queries the lifecycle management configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting lifecycle | Deletes the lifecycle management configuration of a bucket |



#### Bucket policy APIs

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------ |
| [PUT Bucket policy](https://intl.cloud.tencent.com/document/product/436/8282) | Setting a bucket policy | Sets a permission policy for a specified bucket |
| [GET Bucket policy](https://intl.cloud.tencent.com/document/product/436/8276) | Querying a bucket policy | Queries the permission policy of a specified bucket |
| [DELETE Bucket policy](https://intl.cloud.tencent.com/document/product/436/8285) | Deleting a bucket policy | Deletes the permission policy of a specified bucket |


#### Hotlink protection (referer) APIs

| API | Operation | Description |
| ------------------------------------------------------------ | ------------------ | ----------------------------------- |
| [PUT Bucket referer](https://intl.cloud.tencent.com/document/product/436/31423) | Setting a bucket referer | Sets a bucket referer allowlist or blocklist |
| [GET Bucket referer](https://intl.cloud.tencent.com/document/product/436/30615) | Querying a bucket referer | Queries a bucket referer allowlist or blocklist |



#### Bucket tagging APIs

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8281) | Setting bucket tags | Sets tags for an existing bucket |
| [GET Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8277) | Querying bucket tags | Queries the existing tags of a specified bucket |
| [DELETE Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8286) | Deleting bucket tags | Deletes the tags of a specified bucket |



#### Static website APIs

| API                                                          | Operation                   | Description                                       |
| ------------------------------------------------------------ | ---------------- | ---------------------------------- |
| [PUT Bucket website](https://intl.cloud.tencent.com/document/product/436/30617) | Setting a static website| Sets a bucket as a static website|
| [GET Bucket website](https://intl.cloud.tencent.com/document/product/436/30616) | Querying a static website configuration | Queries the static website configuration of a bucket |
| [DELETE Bucket website](https://intl.cloud.tencent.com/document/product/436/30629) | Deleting a static website configuration | Deletes the static website configuration from a bucket |


#### Inventory APIs

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------- |
| [PUT Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30625) | Setting an inventory job | Creates an inventory job in a bucket |
| [GET Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30623) | Querying inventory jobs | Queries the specified inventory configuration of a bucket |
|  [List Bucket Inventory Configurations](https://intl.cloud.tencent.com/document/product/436/30627)  | Querying all inventory jobs | Queries all inventory jobs of a bucket |
| [DELETE Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30626) | Deleting an inventory job | Deletes an inventory job from a bucket   |

#### Versioning APIs

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | -------------------------------- |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Enables or suspends versioning for a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning configuration of a bucket |

#### Cross-region replication APIs

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------------ |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting cross-region replication | Sets a cross-region replication rule for a versioning-enabled bucket |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying cross-region replication | Queries the cross-region replication configuration of a bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting cross-region replication | Deletes the cross-region replication configuration from a bucket |

#### Logging APIs

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | -------------------------- |
| [PUT Bucket logging](https://intl.cloud.tencent.com/document/product/436/17054) | Setting logging | Enables logging for a source bucket |
| [GET Bucket logging](https://intl.cloud.tencent.com/document/product/436/17053) | Querying logging configuration | Queries the logging configuration of a source bucket |

#### Bucket encryption APIs

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------ |
| [PUT Bucket encryption](https://intl.cloud.tencent.com/document/product/436/33459) | Setting bucket encryption | Sets a default encryption configuration for a bucket |
| [GET Bucket encryption](https://intl.cloud.tencent.com/document/product/436/33460) | Querying bucket encryption | Querying the default encryption configuration of a bucket |
| [DELETE Bucket encryption](https://intl.cloud.tencent.com/document/product/436/33461) | Deleting bucket configuration | Deletes the default encryption configuration from a bucket |



## Object APIs

#### Basic operation APIs

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ---------------------------------------- |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading on object using simple upload | Uploads an object to a bucket |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object | Copies a file to a destination path |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | Uploading an object using a form | Uploads an object using a form request |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes a specified object from a bucket |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from a bucket in a single request |
| [OPTIONS Object](https://intl.cloud.tencent.com/document/product/436/8288) | Configuring pre-flight requests for cross-origin access | Sends a pre-flight request to check whether a real cross-origin access request can be sent |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access |
| [SELECT Object Content](https://intl.cloud.tencent.com/document/product/436/32360) | Extracting object content | Extracts the content of a specified object |

#### Access control APIs

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------------- |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting object ACL | Sets the ACL for a specified object in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying object ACL | Queries the ACL of an object |



#### Multipart upload APIs

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploads parts | Uploads a file in multiple parts |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copies a part | Copies an existing object to a part of a new object |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completes multipart upload | Completes the multipart upload of the entire file |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload operation and deletes the uploaded parts |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Queries multipart uploads | Queries in-progress multipart uploads |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Queries uploaded parts | Queries the uploaded parts in the specific multipart upload operation |


## Batch Operation APIs

| API                                                          | Operation                   | Description                                       |
| ------------------------------------------------------------ | -------------- | ------------------------------------------------ |
| [CreateJob](https://intl.cloud.tencent.com/document/product/436/33781) | Creating a job       | Creates a batch job for a bucket                   |
| [DescribeJob](https://intl.cloud.tencent.com/document/product/436/33782) | Describing a job | Gets the parameters and status of an existing batch operation job |
| [ListJobs](https://intl.cloud.tencent.com/document/product/436/33783) | Querying jobs | Lists existing batch operation jobs |
| [UpdateJobPriority](https://intl.cloud.tencent.com/document/product/436/33784) | Updating job priority | Updates the priority of an existing job |
| [UpdateJobStatus](https://intl.cloud.tencent.com/document/product/436/33785) | Updating job status | Updates the status of an existing job |


## Data Processing APIs         

#### Basic image processing APIs


| API  | Description |
| ---- | -------- |
| [Scaling](https://intl.cloud.tencent.com/document/product/436/36366) | Scales up or down an image                                         |
| [Cropping](https://intl.cloud.tencent.com/document/product/436/36367) | Crops an image, including regular cropping, scaling and cropping, inscribed circle cropping, rounded corner cropping, and smart cropping |
| [Rotation](https://intl.cloud.tencent.com/document/product/436/36368) | Rotates an image, including common rotation and adaptive rotation                     |
| [Format Conversion](https://intl.cloud.tencent.com/document/product/436/36369) | Provides format conversion, GIF optimization, and progressive display                  |
| [Quality Conversion](https://intl.cloud.tencent.com/document/product/436/36370) | Changes quality of an image                                           |
| [Gaussian Blur](https://intl.cloud.tencent.com/document/product/436/36371) | Blurs an image                                           |
| [Sharpening](https://intl.cloud.tencent.com/document/product/436/36372) | Sharpens an image                                               |
| [Image Watermarks](https://intl.cloud.tencent.com/document/product/436/36373) | Adds a watermark to an image                                          |
| [Text Watermarks](https://intl.cloud.tencent.com/document/product/436/36374) | Adds a real-time text watermark to an image                                   |
| [Obtaining Basic Image Information](https://intl.cloud.tencent.com/document/product/436/36375) | Queries the basic information about an image, including format, height and width                         |
| [Obtaining Image EXIF Data](https://intl.cloud.tencent.com/document/product/436/36376) | Queries EXIF data                                              |
| [Obtaining the Image Average Hue](https://intl.cloud.tencent.com/document/product/436/36377) | Queries the average hue of an image|
| [Removing Metadata](https://intl.cloud.tencent.com/document/product/436/36378) | Removes image metadata, including EXIF data                               |
| [Quick Thumbnail Template](https://intl.cloud.tencent.com/document/product/436/36379) | Generates a thumbnail using an image processing template                           |
| [Pipeline Operator](https://intl.cloud.tencent.com/document/product/436/36380) | Performs multiple processing styles on an image in a sequence.                                  |
