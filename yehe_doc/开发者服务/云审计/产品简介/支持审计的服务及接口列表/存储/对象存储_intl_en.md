Tencent Cloud Object Storage (COS) is a distributed storage service that can store a high number of files and features high scalability, cost effectiveness, reliability, and security. You can connect to it easily and quickly through a diversity of means such as the console, API, SDK, and tools to upload, download, and manage files in various formats for storage and management of massive amounts of data.

COS operations supported by CloudAudit are as shown below:

| Operation Name | Resource Type | Event Name |
|-------------------------|------|-------------------------|
| Deleting bucket               | cos  | DeleteBucket            |
| Deleting bucket CORS           | cos  | DeleteBucketCORS        |
| Deleting domain                | cos  | DeleteBucketDomain      |
| Deleting bucket encryption setting            | cos  | DeleteBucketEncryption  |
| Deleting inventory             | cos  | DeleteBucketInventory   |
| Deleting bucket lifecycle configuration       | cos  | DeleteBucketLifecycle   |
| BucketWrite\_All        | cos  | DeleteBucketOrigin      |
| Deleting bucket permission policy          | cos  | DeleteBucketPolicy      |
| DeleteBucketReplication | cos  | DeleteBucketReplication |
| DeleteBucketTagging     | cos  | DeleteBucketTagging     |
| DeleteBucketWebsite     | cos  | DeleteBucketWebsite     |
| DeleteObjectTagging     | cos  | DeleteObjectTagging     |
| GetBucketAccelerate     | cos  | GetBucketAccelerate     |
| Reading bucket ACP operation group          | cos  | GetBucketACL            |
| GetBucketCORS           | cos  | GetBucketCORS           |
| Getting domain                | cos  | GetBucketDomain         |
| Getting bucket encryption              | cos  | GetBucketEncryption     |
| Getting inventory             | cos  | GetBucketInventory      |
| GetBucketLifecycle      | cos  | GetBucketLifecycle      |
| GetBucketLogging        | cos  | GetBucketLogging        |
| GetBucketNotification   | cos  | GetBucketNotification   |
| GetBucketObjectVersions | cos  | GetBucketObjectVersions |
| BucketRead\_All         | cos  | GetBucketOrigin         |
| GetBucketPolicy         | cos  | GetBucketPolicy         |
| GetBucketReferer        | cos  | GetBucketReferer        |
| GetBucketReplication    | cos  | GetBucketReplication    |
| GetBucketTagging        | cos  | GetBucketTagging        |
| GetBucketVersioning     | cos  | GetBucketVersioning     |
| GetBucketWebsite        | cos  | GetBucketWebsite        |
| Reading object ACP operation group             | cos  | GetObjectACL            |
| GetObjectTagging        | cos  | GetObjectTagging        |
| GetService              | cos  | GetService              |
| ListMultipartUploads    | cos  | ListMultipartUploads    |
| Restoring archived file                  | cos  | PostObjectRestore       |
| PutBucket               | cos  | PutBucket               |
| PutBucketAccelerate     | cos  | PutBucketAccelerate     |
| Writing bucket ACL operation group          | cos  | PutBucketACL            |
| PutBucketCORS           | cos  | PutBucketCORS           |
| Setting domain                | cos  | PutBucketDomain         |
| Setting bucket encryption              | cos  | PutBucketEncryption     |
| Setting inventory             | cos  | PutBucketInventory      |
| PutBucketLifecycle      | cos  | PutBucketLifecycle      |
| PutBucketLogging        | cos  | PutBucketLogging        |
| PutBucketNotification   | cos  | PutBucketNotification   |
| PutBucketOrigin         | cos  | PutBucketOrigin         |
| PutBucketPolicy         | cos  | PutBucketPolicy         |
| PutBucketReferer        | cos  | PutBucketReferer        |
| PutBucketReplication    | cos  | PutBucketReplication    |
| PutBucketTagging        | cos  | PutBucketTagging        |
| PutBucketVersioning     | cos  | PutBucketVersioning     |
| PutBucketWebsite        | cos  | PutBucketWebsite        |
| PutObjectTagging        | cos  | PutObjectTagging        |
