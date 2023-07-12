## Overview

COS offers the Object Lock feature to help you lock your objects to prevent them from being overwritten or deleted during retention.

>? 
>- With this feature, COS can meet stringent requirements (including SEC Rule 17a-4 (f), FINRA 4511, and CFTC 1.31) on retaining electronic records.
>- SEC Rule 17a-4 is a regulation issued by the U.S. Securities and Exchange Commission under the US Securities Exchange Act of 1934. The rule outlines requirements for data retention, indexing, and accessibility for companies that deal in the trade or brokering of financial securities such as stocks, bonds, and futures. According to the rule, records of numerous types of transactions must be retained and cannot be rewritten or erased with immediate access for a period of two years and non-immediate access for at least six years.

Object Lock is a bucket-level feature, which means that each bucket can only have one time-based Object Lock rule. After this feature is enabled, a retention term is required, which can range from 1 day to 100 years. Permanent retention is not allowed.

During the retention period:
- The object cannot be deleted or modified.
- The storage class of the object cannot be modified.
- HTTP headers and user metadata (including `Content-Type`, `Content-Encoding`, `Content-Language`, `Content-Disposition`, `Cache-Control`, `Expires`, and `x-cos-meta-`) cannot be modified.
- The object tag cannot be modified.

A time-based Object Lock rule has only one status, that is, once the rule is submitted, it takes effect. The rule cannot be modified or deleted. You can only extend the retention period.


## How to Use

You can configure Object Lock by using the console or APIs.

#### Using COS console

For information on how to lock an object in the COS console, see [Setting Object Lock](https://intl.cloud.tencent.com/document/product/436/40136).

#### Using RESTful APIs

You can directly call the following APIs to manage Object Lock:

- [PUT Bucket ObjectLockConfiguration](https://intl.cloud.tencent.com/document/product/436/40133)
- [GET Bucket ObjectLockConfiguration](https://intl.cloud.tencent.com/document/product/436/40134)
- [GET Object Retention](https://www.tencentcloud.com/document/product/436/40135) 


## Restrictions

1. Object Lock is now only available to customers in the allowlist. To use this feature, [contact us](https://intl.cloud.tencent.com/contact-sales).
2. Once enabled, the Object Lock configuration will take effect on a bucket within five seconds.
3. Object Lock can be set for both existing buckets and objects, as shown below:
Assume that you created a bucket named `examplebucket` on July 1, 2012, and uploaded three objects (test1.txt, test2.txt, and test3.txt) at different time points (the upload dates are shown in the following table). Then, on September 1, 2013, you created an Object Lock rule for this bucket to retain objects for 5 years. In this case, the expiration dates of each object's lock rule are as follows:
<table>
	<tr><th>Object</th><th>Upload Date</th><th>Expiration Date of Object Lock Rule</th></tr>
	<tr><td>test1.txt</td><td>July 1, 2012</td><td>June 30, 2017</td></tr>
	<tr><td>test2.txt</td><td>September 1, 2013</td><td>August 31, 2018</td></tr>
	<tr><td>test3.txt</td><td>July 30, 2017</td><td>July 29, 2022</td></tr>
</table>

4. Versioning is not supported for Object Lock−enabled buckets. If the versioning feature is enabled or suspended in a bucket, Object Lock also cannot be enabled.
5. Cross-bucket replication is not supported for Object Lock−enabled buckets. This is because the cross-bucket replication rule requires that the source and destination bucket must have versioning enabled, which is not supported for Object Lock-enabled buckets.
6. INTELLIGENT TIERING is not supported for Object Lock-enabled buckets, and Object Lock cannot be enabled in a bucket that has INTELLIGENT TIERING enabled.
7. During the retention period, the storage class of LOCKED objects cannot be converted. In addition, Object Lock is incompatible with the lifecycle rule. The Object Lock-enabled buckets cannot be configured with lifecycle rules and vice versa.
8. If Object Lock is enabled, the incomplete multiple uploads are not subject to the object lock rule and can be purged for a bucket.
9. Object Lock cannot be disabled once enabled. After all files in the bucket are purged, you can delete the bucket to cancel the object lock rule.
10. If Object Lock is enabled, ACLs of the bucket and objects can still be modified.
