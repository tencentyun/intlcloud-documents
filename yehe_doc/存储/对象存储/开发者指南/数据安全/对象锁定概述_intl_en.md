## Overview

COS introduces Object Lock to meet the requirements of Securities Exchange Commission (SEC) Rule 17a-4. Object Lock can help prevent objects from being overwritten or deleted for a fixed amount of time and objects can still be accessed immediately.

>? SEC Rule 17a-4 is a regulation issued by the U.S. Securities and Exchange Commission under the US Securities Exchange Act of 1934. The rule outlines requirements for data retention, indexing, and accessibility for companies that deal in the trade or brokering of financial securities such as stocks, bonds, and futures. According to the rule, records of numerous types of transactions must be retained and cannot be rewritten or erased with immediate accessibility for a period of at least six years.

Object Lock is a bucket-level feature, that is, only one time-based Object Lock rule can be configured for a bucket. A retention period is required, which can be set to 1 day to 100 years. Setting the retention period to permanent is not allowed.

During the retention period:

- The object cannot be deleted or modified.
- The object’s storage class cannot be modified.
- HTTP headers and user metadata (including `Content-Type`, `Content-Encoding`, `Content-Language`, `Content-Disposition`, `Cache-Control`, `Expires`, and `x-cos-meta-`) cannot be modified.

A time-based Object Lock rule has only one status, that is, once the rule is submitted, it takes effect. The rule cannot be modified or deleted. You can only extend the retention period.




## How to Use

You can configure Object Lock using the console or APIs.

#### Using the COS console

You can configure Object Lock in the COS console. For more information, please see [Setting Object Lock](https://intl.cloud.tencent.com/document/product/436/40136).

#### Using RESTful APIs

You can directly call the following APIs to manage Object Lock:

- [PUT Bucket ObjectLockConfiguration](https://intl.cloud.tencent.com/document/product/436/40133)
- [GET Bucket ObjectLockConfiguration](https://intl.cloud.tencent.com/document/product/436/40134)
- [GET Object Retention](https://intl.cloud.tencent.com/document/product/436/40135) 



## Restrictions

1. Object Lock is now only available to customers in the allowlist, and only the Virginia (US East) and Silicon Valley (US West) regions are supported. To use this feature, please [contact us](https://intl.cloud.tencent.com/support).

2. Object Lock can be set for existing buckets and objects. For more information, please see the example below:

Assume that you created a bucket named `examplebucket` on July 1, 2012, and uploaded three objects (test1.txt, test2.txt, and test3.txt) at different time points (the upload dates are shown in the following table). Then, on September 1, 2013, you created an Object Lock rule for this bucket to retain objects for 5 years. In this case, the expiration dates of each object’s lock rule are as follows: 

| Object | Upload Date | Expiration Date of the Object Lock Rule |
| --------- | ------------- | -------------------- |
| test1.txt | July 1, 2012   | June 30, 2017 |
| test2.txt | September 1, 2013 | August 31, 2018 |
| test3.txt | July 30, 2017 | July 29, 2022 |

3. Cross-bucket replication is not supported for Object Lock−enabled buckets. It can neither be the source bucket nor the destination bucket.
4. Once an object is locked, its storage class cannot be modified and Lifecycle is no longer supported. 
>? if an object is configured with both Object Lock and Lifecycle, the Lifecycle configuration will not take effect.
5. You can still clean up the incomplete multipart uploads.
6. An Object Lock rule cannot be deleted independently. Only when the bucket is empty and deleted can the rule be deleted along with the bucket.
7. If Object Lock is enabled, ACLs of the bucket and objects can still be modified. 
8. For Versioning-enabled buckets, deleting or modifying any object version is not supported.


































































