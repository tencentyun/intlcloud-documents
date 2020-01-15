

The batch replication feature is used to replicate objects in the inventory, i.e., allowing you to batch replicate the specified objects from the source bucket to the destination bucket in the same region or in different regions. It supports customizing parameters for the `PUT Object-copy` operation, and the copy metadata and storage type are subject to the configuration information. For more information, please see [PUT Object-copy](https://cloud.tencent.com/document/product/436/10881).

#### Use Limits

- All objects to be replicated must be in the same bucket.
- Only one destination bucket can be configured for a batch replication job.
- You need to have permission to read objects from the source bucket and write objects into the destination bucket.
- The total size of the objects cannot exceed 5 GB.
- Verification via ETags and server-side encryption using custom keys are not supported.
- If the destination bucket does not have versioning enabled and contains an object file with the same name as a file to be replicated, COS will overwrite the object file.
