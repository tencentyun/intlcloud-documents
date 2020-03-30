## Overview
By enabling versioning, you can store multiple versions of an object in the same bucket. For example, you can store multiple objects with the same object key “picture.jpg” in one bucket, but the objects have different version IDs such as 100000, 100101, and 120002. You can query, delete, or restore the objects by version ID. Versioning enables you to recover from data loss caused by accidental deletion or application failure. Versioning is ideal for the following scenarios:

- If you need to delete objects (not permanently) in a versioning-enabled bucket, COS will insert delete markers for the deleted objects, and the markers will serve as the current object versions. You can restore an object to its previous version by the **delete marker**.
- If you need to replace objects, COS will insert new version IDs for the added objects, and you can still restore the replaced objects by version ID.

## Versioning States
There are three versioning states for a bucket: not enabled, enabled, or suspended.
- **Versioning not enabled:** bucket versioning is not enabled by default.
- **Versioning enabled:** when bucket versioning is enabled, it will be applied to **all the objects** in the bucket. After versioning is enabled for the first time, objects added to the bucket thereafter will be assigned a unique version ID.
- **Versioning suspended:** Once the versioning state is changed from enabled to suspended (versioning cannot be disabled once enabled), objects added to the bucket thereafter will no longer be subject to versioning.

>1. Once versioning is enabled for the bucket, it cannot be disabled. However, you can suspend versioning to stop object versioning.
>2. For objects existing in the bucket before versioning is enabled, the version ID is "null".
>3. Enabling or suspending versioning will change the way COS makes requests when handling the objects but not the objects themselves.
>4. Only the root account and authorized sub-accounts can suspend versioning for a bucket.

## Managing Objects in Buckets with Different Versioning States

You can add, query, and delete objects in a bucket no matter what the versioning state is. When versioning is enabled or suspended, you can query and delete objects with or without version IDs.

- If versioning is not enabled, you can add, query, and delete objects in the same way as in an ordinary bucket. For more information, see the [Object Management](https://intl.cloud.tencent.com/document/product/436/13321).
- If versioning is enabled or suspended, you can specify version IDs while retrieving and deleting objects. **Delete markers** will be added to deleted objects.


### Managing Objects in a Versioning-enabled Bucket
For objects in the bucket before versioning is enabled, their version ID will be “null”. Enabling versioning will change the way COS handles the objects, such as how COS makes requests, but not the objects themselves. Objects with the same name added thereafter will be stored in the same bucket with different version IDs. You can manage objects in a bucket with versioning enabled as described below:

>The way you add objects to a bucket is the same for both buckets with versioning enabled and not enabled, but the objects added to the two types of buckets have different version IDs. If versioning is enabled, COS will assign a unique version ID to any object added to the bucket; if versioning is not enabled, the version ID will remain null.

#### Adding Objects

If versioning is enabled for a bucket, when you perform PUT, POST, and COPY operations, COS will automatically assign a unique version ID to the objects added to the bucket.
As you can see below, when an object is added to a bucket with versioning enabled, COS will assign it a unique version ID.

![](https://main.qcloudimg.com/raw/906b71f4cfd5a79ac9d6bbdf85e50254.png)

#### Listing Versioned Objects

COS stores object version information in the versions parameter associated with the bucket and returns object versions in the order of storage time from the newest to the oldest.

#### Retrieving All Versions of a Specific Object

You can retrieve all versions of a particular object using the versions parameter together with the prefix request parameter. For more information on prefix, see [GET Bucket Object Versions](https://intl.cloud.tencent.com/document/product/436/31551).
Below is a sample request for retrieving all versions of a specific object:

```
GET /?versions&prefix=OjectKey HTTP/1.1
```

#### Retrieving Historical Versions of an Object

A GET request with no version ID specified retrieves the current version of an object. The following figure shows how a GET request returns the current version (the latest version) of the 123.txt object.

![](https://main.qcloudimg.com/raw/8c4bb589985ea664a8266278877898e8.jpg)

A GET request with a version ID specified retrieves the specified version of an object. The following figure shows how a GET versionId request returns the specified version of the object. The request can also retrieve the current version.

![](https://main.qcloudimg.com/raw/f6c9cedf716a9d2b069ea8b103a79260.png)


#### Retrieving the Metadata of an Object Version 
If you only want to retrieve the metadata of an object instead of its content, you can use the HEAD operation. By default, you get the metadata of the latest version. To retrieve the metadata of a specific object version, you need to specify its version ID when submitting the request.
To retrieve the metadata of an object version:
- Set versionId to the ID of the version of the object whose metadata you want to retrieve.
- Send a HEAD operation request with the versionId specified.

#### Deleting Objects
You can delete unnecessary object versions whenever you want. When you make a DELETE request in a versioning-enabled bucket, there will be two scenarios:
1. Perform a simple DELETE operation with no version ID specified.
This is similar to putting the deleted objects to the "recycle bin". The objects are not permanently deleted and can be restored if needed.
As you can see below, if you do not specify a version ID, the DELETE operation will not delete the 123.txt object; instead, it will insert a delete marker and add a new version ID.
![](https://main.qcloudimg.com/raw/fe53cffa9dc6799ed91438c14ab1f57e.png)
>COS will insert a delete marker with a new version ID for the deleted objects. The delete marker will become the current version of the deleted objects. When you try to GET the objects with a delete marker, COS will assume that the objects do not exist and will return a 404 error.

2. If you delete an object with a version ID specified, the specified version of the object will be deleted permanently.
![](https://main.qcloudimg.com/raw/7b36446f98a66c73901ab5007a2b008d.png)

#### Delete Marker
A delete marker is a marker for versioned objects, indicating that the objects have already been deleted in COS. A delete marker has an object key and version ID like any other object. However, a delete marker differs from other objects in the following ways:
- Its content is empty.
- It does not have ACL value.
- If you try to GET a delete marker, you will get a 404 error.
- The only operation you can use on a delete marker is DELETE, and only the root account can issue such a request.

#### Deleting a Delete Marker
To delete a delete marker, you can specify its version ID in a DELETE Object versionId request to permanently delete it. If you use a DELETE request to delete a delete marker without specifying its version ID, COS will not delete the delete marker, but instead, insert another delete marker.
The following figure shows how a simple DELETE on a delete marker removes nothing, but adds a new delete marker to a bucket.
![](https://main.qcloudimg.com/raw/0f9a86359df48cda6c0a74809cffc228.png)

In a versioning-enabled bucket, a new delete marker has a unique version ID. Therefore, one object may have multiple delete markers in the same bucket. To delete a delete marker permanently, you must include its version ID in a DELETE Object versionId request.
The following figure shows how you can permanently delete a delete marker with a DELETE Object versionId request.
![](https://main.qcloudimg.com/raw/576fe70fc601d3cca7f33386fe9f2276.png)

>Only the root account can delete a delete marker permanently.

To permanently remove a delete marker:
1. Set versionId to the ID of the version of the delete marker you want to remove.
2. Send a DELETE Object versionId request.

#### Restoring Previous Versions
Versioning can be used to restore previous versions. You can do it in two ways:
1. Copy a previous version of the object into the same bucket
The copied object will become the current version of the object, and all object versions will be retained
2. Delete the current version of the object permanently
When you delete the current object version, you, in effect, turn the previous version into the current version of the object.


### Managing Objects in a Versioning-suspended Bucket
When you suspend versioning, existing objects in your bucket do not change. What changes is how COS handles objects in future requests. The section below describes how to manage objects in a bucket where versioning is suspended.


#### Adding Objects

Once you suspend bucket versioning, when you use PUT, POST, or COPY operations, COS will automatically add a “null” version ID to objects added to the bucket thereafter as shown below:
![](https://main.qcloudimg.com/raw/49119321acf671c41f227d98f7603423.png)

If there are versioned objects in the bucket, the objects newly added to the bucket will become the current version with a version ID of null as shown below:
![](https://main.qcloudimg.com/raw/325e7eff5a0e533342cb9b8ad683adc3.png)

If there is already a null version in the bucket, it will be overwritten, and the original object content will also be replaced accordingly as shown below:
![](https://main.qcloudimg.com/raw/0519c869c8431950797e9c0b76db3ac9.png)

#### Retrieving Historical Versions of an Object
A GET Object request in a versioning-suspended bucket returns the current version of an object.

#### Deleting Objects
If versioning is suspended, a DELETE request will result in one of the following:
- If an object has a null version in the bucket, the null version of the object will be deleted.
As you can see below, when you use a simple DELETE operation, COS will insert a delete marker for objects with a version ID of null.
![](https://main.qcloudimg.com/raw/6cf8895af9e63736e1ee7160628c58fd.png)
>Since a delete marker does not have content, you will lose the original content of the null version when a delete marker replaces it.

- If an object does not have a null version in the bucket, a new delete marker will be added to the bucket.
As you can see below, if an object does not have a null version in the bucket, a simple DELETE will not remove anything; COS will just insert a delete marker.
![](https://main.qcloudimg.com/raw/9bd2d397466bd981ed04fad8b4395336.png)

	Even in a bucket where versioning is suspended, the root account is still able to delete a specified version permanently.
	The following figure shows that deleting a specified object version will delete the object permanently.
	![](https://main.qcloudimg.com/raw/e814ec84e0c64b69275aef8a9dbe3d6c.png)

	>Only the root account can delete a specified object version permanently.
