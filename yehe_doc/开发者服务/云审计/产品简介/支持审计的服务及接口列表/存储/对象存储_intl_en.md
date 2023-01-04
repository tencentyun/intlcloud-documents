Cloud Object Storage (COS) is a powerful Tencent Cloud distributed storage service that features low costs and high scalability, reliability, and security. It enables you to store a huge number of files. You can easily and quickly access it to upload, download, and manage files in various formats for storage and management of massive amounts of data via the console, API, SDK, or other tools.

Listed below are the COS operations supported by CloudAudit:

| Operation | Resource Type | Event Name |
|-------------------------|------|-------------------------|
| Deleting a bucket               | COS  | DeleteBucket            |
|  Deleting the CORS configuration of a bucket        | COS  | DeleteBucketCORS        |
| Deleting the custom domain name of a bucket              | COS  | DeleteBucketDomain      |
| Deleting the default encryption configuration of a bucket           | COS  | DeleteBucketEncryption  |
| Deleting the inventory jobs of a bucket            | COS  | DeleteBucketInventory   |
| Deleting the lifecycle configuration of a bucket       | COS  | DeleteBucketLifecycle   |
| BucketWrite\_All        | COS  | DeleteBucketOrigin      |
| Deleting the permission policy of a bucket          | COS  | DeleteBucketPolicy      |
| Deleting the replication configuration of a bucket | COS  | DeleteBucketReplication |
| Deleting bucket tags    | COS  | DeleteBucketTagging     |
| Deleting the static website configuration of a bucket      | COS  | DeleteBucketWebsite     |
| Deleting object tags     | COS  | DeleteObjectTagging     |
| Getting the configuration status of the global acceleration feature     | COS  | GetBucketAccelerate     |
| Getting the access control list of a bucket      | COS  | GetBucketACL            |
| Getting the CORS access control list of a bucket           | COS  | GetBucketCORS           |
| Getting the custom domain name of a bucket               | COS  | GetBucketDomain         |
| Querying the default encryption configuration of a bucket             | COS  | GetBucketEncryption     |
| Getting the user inventory job information of a bucket           | COS  | GetBucketInventory      |
| Getting the lifecycle configuration of a bucket      | COS  | GetBucketLifecycle      |
| Getting the log configuration of a bucket        | COS  | GetBucketLogging        |
| Getting the callback configuration of a bucket   | COS  | GetBucketNotification   |
| Getting the object versions | COS  | GetBucketObjectVersions |
| BucketRead\_All         | COS  | GetBucketOrigin         |
| Getting the read permission policy of a bucket         | COS  | GetBucketPolicy         |
| Getting the referer allowlist or blocklist of a bucket        | COS  | GetBucketReferer        |
| Getting the user’s bucket replication configuration    | COS  | GetBucketReplication    |
| Getting the existing tags of a bucket        | COS  | GetBucketTagging        |
| Getting the versioning information of a bucket     | COS  | GetBucketVersioning     |
| Getting the static website configuration of a bucket        | COS  | GetBucketWebsite        |
| Querying the access control list of an object             | COS  | GetObjectACL            |
| Getting the existing tags of an object        | COS  | GetObjectTagging        |
| Getting the list of all buckets under a specified account              | COS  | GetService              |
| Listing the files that failed to be uploaded    | COS  | ListMultipartUploads    |
| Restoring archived files                  | COS  | PostObjectRestore       |
| Creating a bucket under a specified account             | COS  | PutBucket               |
| Enabling or disabling the global acceleration feature of a bucket     | COS  | PutBucketAccelerate     |
| Setting the access control list of a bucket          | COS  | PutBucketACL            |
| Setting the CORS permission of a bucket           | COS  | PutBucketCORS           |
| Setting the custom domain name of a bucket                | COS  | PutBucketDomain         |
| Setting the default encryption configuration of a bucket             | COS  | PutBucketEncryption     |
| Setting the inventory jobs of a bucket            | COS  | PutBucketInventory      |
| Configuring lifecycle management for a bucket      | COS  | PutBucketLifecycle      |
| Enabling logging for a source bucket        | COS  | PutBucketLogging        |
| PutBucketNotification   | COS  | PutBucketNotification   |
| PutBucketOrigin         | COS  | PutBucketOrigin         |
| Configuring the permission policy for a bucket         | COS  | PutBucketPolicy         |
| Setting the referer allowlist or blocklist for a bucket        | COS  | PutBucketReferer        |
| Setting cross-region replication rules for a bucket    | COS  | PutBucketReplication    |
| Setting tags for an existing bucket        | COS  | PutBucketTagging        |
| Setting versioning for a bucket     | COS  | PutBucketVersioning     |
| Configuring the static website for a bucket        | COS  | PutBucketWebsite        |
| Setting tags for an existing object        | COS  | PutObjectTagging        |
