

The batch copy feature is used to copy objects in the inventory, i.e., allowing you to batch copy the specified objects from the source bucket to the destination bucket in the same region or in a different region. It supports customizing parameters for the `PUT Object-copy` operation, and parameter configuration affects the metadata and storage class of the target objects. For more information, see [PUT Object-copy](https://cloud.tencent.com/document/product/436/10881).

#### Restrictions

- All objects to be copied must be in the same bucket.
- Only one destination bucket can be configured for a batch copy job.
- You need to have permission to read objects from the source bucket and write objects into the destination bucket.
- The total size of the objects cannot exceed 5 GB.
- Verification through ETags and server-side encryption using custom keys are not supported.
- If the destination bucket does not have versioning enabled and contains an object with the same name as an object to be copied, COS will overwrite the object.
- If an object in the inventory has multiple versions, only one version can be copied. If the version ID is not specified, the latest version will be copied.

