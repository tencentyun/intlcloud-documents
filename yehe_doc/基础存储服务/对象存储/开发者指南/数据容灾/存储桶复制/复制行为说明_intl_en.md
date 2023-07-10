This document describes what COS will and will not replicate after you enable cross-bucket replication for a bucket.

## What is replicated

In a source bucket with cross-bucket replication enabled, COS will replicate the following:

- Any new objects uploaded to the source bucket after the cross-bucket replication rule is added.
- Object attributes such as object metadata and version ID.
- Information on object operations such as adding an object of the same name (equivalent to adding a new object) and deleting an object.

>?
>
>- If you specify an object version to delete in the source bucket by specifying a version ID, COS will not replicate this delete operation.
>- If you add a bucket-level configuration such as a lifecycle rule to the source bucket, COS will not replicate any resulting object operations.

#### Delete operations in cross-bucket replication

If an object is deleted from a source bucket with cross-bucket replication enabled, the following will happen:

- If you try to delete an object from the source bucket without specifying a version ID, COS will add a delete marker to the object. Then, if you select the option **Sync Delete Marker**, cross-bucket replication will replicate this delete marker to the destination bucket. Regardless of whether the delete marker is replicated, the object will not be deleted from the destination bucket. You can always access a noncurrent version of the object by specifying its version ID. For more information, please see [Versioning Overview](https://intl.cloud.tencent.com/document/product/436/19883).
- If you specify a version ID to delete an object, COS will delete the specified object version from the source bucket, but will not replicate the delete operation to the destination bucket. That is, COS will not delete this object version from the destination bucket. This prevents malicious data deletion.

## What isn't replicated

In a source bucket with cross-bucket replication enabled, COS will not replicate the following:

- Objects that existed before cross-bucket replication is enabled.
- An object’s encryption information, which will be lost once the encrypted object is replicated.
- Object data in the source bucket that has been copied from another bucket.
- Updates to bucket-level configuration.
- Actions performed by lifecycle configuration.

>?
>
>- The cross-bucket replication of object data between buckets is not transitive. If you set two cross-bucket replication rules, one of which sets bucket A as the source bucket and bucket B as the destination bucket, and the other sets bucket B as the source bucket and bucket C as the destination bucket, then the object data added to bucket A will be replicated only to bucket B but not to bucket C.
>- For example, if you update the lifecycle configuration of the source bucket, COS will not apply this configuration to the destination bucket synchronously.
>- If you configure a lifecycle rule only for the source bucket, COS will add delete markers to expired objects there, but the markers will not be replicated to the destination bucket. For the destination bucket to delete these expired objects as well, you need to configure the same lifecycle rule for the destination bucket.
