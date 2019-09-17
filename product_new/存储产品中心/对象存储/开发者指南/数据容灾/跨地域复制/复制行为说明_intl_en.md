This document describes the content that will and will not be copied after you enable cross-region replication for a bucket.

## Content That Will Be Copied

In a source bucket with cross-region replication enabled, COS will copy the following:

- Any new objects uploaded to the source bucket after the cross-region replication rule is added.
- Object attribute information such as object metadata and version ID.
- Information on object operations such as adding an object of the same name (equivalent to adding a new object) and deleting an object.

>- If you specify to delete an object version from the source bucket (i.e., specifying the version ID), this operation will not be copied.
> - If you add a bucket-level configuration such as a lifecycle rule to the source bucket, object operations caused by such configurations will not be copied to the destination bucket.

#### Deletions with Cross-region Replication Enabled

If an object is deleted from a source bucket with cross-region replication enabled, the following will happen:

- When a DELETE request is executed with no object version ID specified, COS will add a delete marker to the source bucket, and cross-region replication will copy the marker to the destination bucket. For more information on versioning and delete marker, see [Versioning Configuration](/document/product/436/19884).
- When a DELETE request is executed with an object version ID specified, COS will delete the specified object version from the source bucket but will not copy the deletion operation to the destination bucket, which means that COS will not delete the specified object version from the destination bucket. This can prevent malicious deletion of data.

## Contents That Will Not Be Copied

In a source bucket with cross-region replication enabled, COS will not copy the following:

- Objects that have already been in the bucket when cross-region replication is enabled, i.e., the legacy data.
- Encrypted objects. COS does not copy encrypted data by default, but you can enable encrypted data replication by modifying the configuration information.
- New object data added to the source bucket that is copied from another bucket.
- Configuration updates at the bucket level.
- Results from the execution of the lifecycle configuration.

>- The cross-region replication of object data between buckets is not transitive. If you set two cross-region replication rules, one of which sets bucket A as the source bucket and bucket B as the destination bucket, and the other sets bucket B as the source bucket and bucket C as the destination bucket, then the object data added to bucket A will only be copied to bucket B but not to bucket C.
>- For example, if you update the lifecycle configuration of the source bucket, COS will not apply this configuration to the destination bucket synchronously.
>- If you only configure a lifecycle rule for the source bucket, COS will add delete markers to expired objects there, but the markers will not be copied to the destination bucket. If you want the destination bucket to delete the expired objects, you need to configure the same lifecycle rule for the destination bucket separately.
