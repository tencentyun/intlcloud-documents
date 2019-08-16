This document describes the contents that will and will not be copied after you configure cross-region replication for a bucket.

## Content That Will Be Copied

In a source bucket with cross-region replication enabled, COS will copy the following:

- Any new objects uploaded to the source bucket after the cross-region replication rule is added.
- Object attribute information such as object metadata and version ID.
- Information on object operations such as adding an object of the same name (equivalent to adding a new object) and deleting an object.

>- If you specify to delete an object version from the source bucket (i.e., specifying the version ID), this operation will not be copied.
> - If you add a bucket-level configuration such as a lifecycle rule to the source bucket, object operations caused by such configurations will not be copied to the destination bucket.

#### Deletions Under Cross-region Replication

If an object is deleted from the source bucket, the cross-region replication behaviors are as follows:

- When a DELETE request is executed with no object version ID specified, COS will add a deletion flag to the source bucket, and cross-region replication will copy the flag to the destination bucket. For more information on versioning and deletion flag, see [Versioning Configuration](https://intl.cloud.tencent.com/document/product/436/19884).
- When a DELETE request is executed with an object version ID specified, COS will delete the specified object version from the source bucket but will not copy the deletion operation to the destination bucket, i.e., COS will not delete the specified object version from the destination bucket. This behavior prevents malicious deletion of data.

## Contents That Will Not Be Copied

In a source bucket with cross-region replication enabled, COS will not copy the following:

- Objects that have already been stored before cross-region replication is enabled, i.e., the existing data.
- Encrypted objects. COS does not copy encrypted data by default, but you can implement encrypted data replication by modifying the configuration information.
- New object data added to the source bucket that is copied from another bucket.
- Configuration update behaviors at the bucket level.
- Results after the execution of the lifecycle configuration.

>- The cross-region replication of object data between buckets is not transitive. If you set two cross-region replication rules at the same time where bucket A is the source bucket and bucket B is the destination bucket in one rule and bucket B is the source bucket and bucket C is the destination bucket in the other rule, then the object data added to bucket A will only be copied to bucket B but not transitively copied to bucket C.
>- For example, if you update the lifecycle configuration of the source bucket, COS will not apply this configuration to the destination bucket synchronously.
>- If you only configure a lifecycle rule for the source bucket, COS will add deletion flags to expired objects there, which will not be copied to the destination bucket. If you want the destination bucket to be able to delete the expired objects too, you need to configure the same lifecycle rule for the destination bucket separately.
