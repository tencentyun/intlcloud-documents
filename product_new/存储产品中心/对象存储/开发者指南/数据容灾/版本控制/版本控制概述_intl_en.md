## Overview
By enabling versioning, you can store multiple versions of an object in the same bucket. For example, you can store multiple objects with the same object key picture.jpg in one bucket, which have different version IDs such as 100000, 100101, and 120002. You can query, delete, or restore the objects by version ID. Versioning enables you to recover data that was lost due to accidental deletion or application failure. Versioning is ideal for the following scenarios:

- If you need to delete objects (not permanently) in a versioning-enabled bucket, COS will insert a deletion flag for the deleted objects, and the flag will serve as the current object version. You can restore the objects to a previous version by the **deletion flag**.
- If you need to replace objects, COS will insert a new version ID for the added objects, and you can still restore the replaced objects by the version ID.

## Versioning Status
There are three versioning states for a bucket: not enabled, enabled, or suspended.
- **Versioning not enabled:** Bucket versioning is not enabled default.
- **Versioning enabled:** When bucket versioning is enabled, it will be applied to **all objects** in the bucket. After versioning is enabled for the first time, the newly added objects in the bucket will be assigned a unique version ID.
- **Versioning suspended:** When versioning status is changed from enabled to suspended (versioning cannot be disabled once enabled), the newly added objects will not be subject to versioning.

>1. Once versioning is enabled for the bucket, it cannot be disabled. However, you can suspend versioning to stop object versioning.
>2. Before enabling versioning, the version ID of all the objects stored in the bucket is "null".
>3. Enabling or suspending versioning will change the request method of COS when processing the objects but not the objects themselves.
>4. Only the root account and authorized sub-accounts can suspend versioning for a bucket.

## Managing Versioned Objects

You can add, query, and delete the objects in a bucket in different versioning states. Except when versioning is not enabled, version ID can be specified or not specified when you query or delete objects in the bucket.

- If versioning is not enabled, you can add, query, and delete objects in the same way as in an ordinary bucket. For more information, see the [Object Management](https://intl.cloud.tencent.com/document/product/436/13321).
- If versioning is enabled or suspended, the methods for adding, querying, and deleting objects are different from before as version ID can be used. There is also a "deletion flag" concept during object deletion.


### Managing Unversioned Objects
Before versioning is enabled, the version ID of objects in a bucket is null. Enabling versioning will change the way how COS deals with the objects (such as the request method) but not the objects themselves. In this case, newly added objects with the same name will be stored in the same bucket on different versions. You can manage objects in a versioning-enabled bucket as described below:

> You can add objects to a bucket in the same way no matter whether versioning is enabled, but the version IDs are different. If versioning is enabled, COS will assign a specific version ID to an object added to the bucket; if versioning is not enabled, the version ID remains null.

#### Adding Objects

If versioning is enabled for a bucket, when you perform PUT, POST, and COPY operations, COS will automatically assign a unique version ID to the objects added to the bucket.
As shown below, when objects are added to a versioning-enabled bucket, COS will assign a unique version ID to them:

![](https://main.qcloudimg.com/raw/960e513c5cc95caf81c29ea7c8ebb5b8.png)

#### Listing Versioned Objects

This section provides an example of listing object versions in a versioning-enabled bucket. COS stores object version information in the versions parameter associated with the bucket and returns object versions in the order of storage time from newest to oldest.

#### Querying All Versions of a Specific Object

You can query all versions of a particular object using the versions parameter together with the prefix request parameter. For more information on prefix, see [GET Bucket Object Versions](https://intl.cloud.tencent.com/document/product/436/31551).
Below is a sample request for querying all versions of a specific object:

```
GET /?versions&prefix=OjectKey HTTP/1.1
```

#### Querying Data Version

If version ID is not specified for a GET request, objects on the current version will be queried. As shown below, the GET request will return the current version (latest version) of the 123.txt object.

![](https://main.qcloudimg.com/raw/375ad2944ab9fd93fb0922c9848f66c1.png)

If version ID is specified for the GET request, objects on the specified version will be queried. As shown below, the GET versionId request will query objects on the specified version (which can be the current version).

![](https://main.qcloudimg.com/raw/1a6fb6adbe2320ff3b69a2ca50d41a6c.png)


#### Querying Object Version Metadata
If you only need to query object metadata instead of object content, you can perform a HEAD operation which will get metadata on the latest version by default. To query metadata on the specified object version, you need to specify the version ID when submitting the request.
Directions:
- Set versionId to the version ID of the object metadata to be queried
- Submit the HEAD operation request with the specified versionId.

#### Deleting Objects
You can delete unnecessary object versions at any time as needed. You can use a DELETE request in two scenarios:
1. Perform a common DELETE operation with no version ID specified.
This is similar to putting the deleted objects to the "recycle bin" without deleting them permanently, and the data can still be restored if needed.
As shown below, if version ID is not specified, the DELETE operation will not delete objects with Key 123.txt; instead, it will insert a deletion flag and add a new version ID.
![](https://main.qcloudimg.com/raw/71628c83c377584a0045a399f37d3aa4.png)
> COS will insert a deletion flag for the deleted objects in the bucket which will have a new version ID and become the current version of the deleted objects. When you try to perform a GET operation on the objects with this deletion flag, COS will assume that the objects do not exist and will return a 404 error.

2. If you perform a deletion operation with a version ID specified, the objects on the specified version will be deleted permanently.
![](https://main.qcloudimg.com/raw/7edd4dcc932f0afbee61a9acb2e6e948.png)

#### Deletion Flag
Deletion flags are used for versioned objects, indicating that the objects have already been deleted in COS. They have the same object key and version ID as the objects. The differences lie in that:
- The content of a deletion flag is empty.
- A deletion flag has no ACL value.
- If there is a deletion flag, the GET request will return a 404 error with the response header of `x-cos-delete-marker: true`.
- A deletion flag only support DELETE operations initiated under the root account.

#### Deleting a Deletion Flag
To delete a deletion flag, you can specify its version ID in the DELETE Object versionId request for permanent deletion. If you initiate a DELETE request for the deletion flag without specifying a version ID, COS will not delete the deletion flag; instead, it will insert a new one.
As shown below, performing a common DELETE request for a deletion flag will not delete any content but add a new deletion flag in the bucket.
![](https://main.qcloudimg.com/raw/3df4d8e412e8e8ad5365464501491554.png)

In a versioning-enabled bucket, a newly added deletion flag will have a unique version ID. Therefore, the same object in the bucket may have multiple deletion flags. To delete a deletion flag permanently, its version ID must be specified in the DELETE Object versionId request.
You can do so as shown below:
![](https://main.qcloudimg.com/raw/090263da37eb56817e21d6f13b116ebe.png)

> Only the root account can delete a deletion flag permanently.

Directions:
1. Set versionId to the version ID of the deletion flag.
2. Send the DELETE Object versionId request.

#### Restoring to a Previous Version
Versioning can be used to query previous versions of objects in two ways:
1. Copy the objects on a previous version to the same bucket
The copied objects will become the current version of the objects, and all object versions will be retained
2. Delete the objects on the current version permanently
When the current object version is deleted, the previous version will actually become the current version of the objects.


### Managing Objects in a Versioning-suspended Bucket
Suspending versioning will not change the objects in the bucket; instead, it will change the way how COS processes objects in subsequent requests. The section below describes how to manage objects in a bucket where versioning is suspended.


#### Adding Objects

After bucket versioning is suspended, when you perform PUT, POST, or COPY operations, COS will automatically add a null version ID to the objects in the bucket as shown below:
![](https://main.qcloudimg.com/raw/d54464a301c2e3fb882dac0ab48bbe2a.png)

If there are versioned objects in the bucket, the objects newly added to the bucket will become the current version with a null version ID as shown below:
![](https://main.qcloudimg.com/raw/112935abc0a47a4e80b9b38c096b59d1.png)

If there is already a null version in the bucket, it will be overwritten, and the original object content will also be replaced accordingly as shown below:
![](https://main.qcloudimg.com/raw/3c03cbb7d7249edeeb5f306447970de9.png)

#### Querying Data Version
If you initiate a GET Object request in a bucket where versioning is suspended, the current version of objects will be returned.

#### Deleting Objects
If versioning is suspended, performing a DELETE request will have one of the following results:
- If there are objects with null version ID in the bucket, such objects will be deleted.
When you perform a common DELETE operation, COS will insert a deletion flag for objects with null version ID as shown below.
![](https://main.qcloudimg.com/raw/0be8e3683ba1b24cee559fdc94d4e548.png)
> A deletion flag has no content. When a deletion flag is used to replace objects with null version, the original content of the objects will be lost.

- If there are no objects with null version in the bucket, a new deletion flag will be added to the bucket.
If there are no objects with null version in the bucket, when you perform the DELETE operation, COS will not delete any content; instead, it will insert a deletion flag as shown below:
![](https://main.qcloudimg.com/raw/03051debe6fd7d9f3a15a3d9403e0356.png)

	Even if in a bucket where versioning is suspended, the root account can delete the specified version permanently.
	Deleting the specified version will delete the objects permanently as shown below.
	![](https://main.qcloudimg.com/raw/b690a7576475cb96b14df44a097bab3c.png)

	> Only the root account can delete specified object versions permanently.
