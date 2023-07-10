## Concepts

An ACL is described in the XML language. It is a list of specified grantees and permissions granted, which is associated with resources. Each bucket and object has an associated ACL to grant basic read and write permissions to anonymous users or other Tencent Cloud root accounts.

>!Here are some limits on the use of ACLs associated with resources:
>- The resource owner always has the FULL_CONTROL permission on the resource, which cannot be revoked or modified.
>- An anonymous user cannot be the resource owner. In this case, the object owner is the bucket owner (Tencent Cloud root account).
>- Permissions can only be granted to Tencent Cloud CAM root accounts or preset user groups, but not custom user groups. Besides, it's not recommended to grant permissions to any sub-users.
>- No conditions should be imposed on the permissions.
>- "Deny" permission is not supported.
>- A resource can have up to 100 ACL policies.
>

## Use Cases

>! Enabling anonymous access (Public Read) is highly risky due to hotlinking risks. In cases where Public Read is required, you can [set hotlink protection](https://intl.cloud.tencent.com/document/product/436/13319) to improve security.
>

Use ACLs if you only need to set some simple access permissions for buckets and objects or enable anonymous access. However, in most cases, you are advised to use bucket policies or user policies, which are more flexible. ACLs are recommended in scenarios where you want to:

- Set simple access permissions.
- Set access permissions quickly in the console.
- Make an object, directory, or bucket accessible to all anonymous internet users.


## ACL Elements

### Identity (Grantee)

A supported grantee can be a CAM root account or a preset CAM user group.

>!
>- When you grant access permissions to another Tencent Cloud root account, this root account can grant access permissions to its sub-users, user groups or roles.
>- In COS, it is strongly recommended not to grant the WRITE, WRITE_ACP or FULL_CONTROL permission to any anonymous user or CAM user group. Otherwise, the user group can upload, download or delete your resources, which will bring security risks to your account, such as data loss and fee deduction.
>


Grantees supported in bucket or object ACLs include:

- Cross-account: use the root account ID to get the account ID, e.g., `100000000001`, in [Account Info](https://console.cloud.tencent.com/developer).
- Preset user group: tag a preset user group using a URI tag. The following user groups are supported:
  - Anonymous user group - `http://cam.qcloud.com/groups/global/AllUsers`, which indicates that anyone can access resources without authorization, regardless of whether the request is signed or unsigned.
  - Authenticated user group - `http://cam.qcloud.com/groups/global/AuthenticatedUsers`, which indicates that users who have registered a Tencent Cloud CAM account can access resources.


### Action permissions

Tencent Cloud COS supports a range of action sets on resource ACLs, which include different actions on bucket ACLs and object ACLs respectively.

**Actions on buckets**

Here is a list of actions supported in bucket ACLs:

| Action Set | Description | Allowed Actions |
| ------------ | -------------------- | ------------------------------------------------------------ |
| READ | Lists objects | HeadBucket, GetBucketObjectVersions, ListMultipartUploads |
| WRITE | Uploads, overwrites and deletes objects | PutObject, PutObjectCopy, PostObject, InitiateMultipartUpload, UploadPart, UploadPartCopy, CompleteMultipartUpload, DeleteObject |
| READ_ACP | Reads bucket ACLs | GetBucketAcl |
| WRITE_ACP | Writes to bucket ACLs | PutBucketAcl |
| FULL_CONTROL | A collection of the above sets | A collection of the above actions |

>!Please proceed with caution when you grant the WRITE, WRITE_ACP or FULL_CONTROL permission on buckets. Granting the WRITE permission will allow the grantee to overwrite or delete any existing object.
>

**Actions on objects**

Here is a list of actions supported in object ACLs:

| Action Set | Description | Allowed Actions |
| ------------ | ------------------ | --------------------------------------- |
| READ | Reads objects | GetObject, GetObjectVersion, HeadObject |
| READ_ACP | Reads object ACLs | GetObjectAcl, GetObjectVersionAcl |
| WRITE_ACP | Writes to object ACLs | PutObjectAcl, PutObjectVersionAcl |
| FULL_CONTROL | A collection of the above sets | A collection of the above action sets |

>?The WRITE action set is not supported for objects.

### Preset ACL

Tencent Cloud COS supports a group of preset ACLs for authorization, making it much easier to describe simple permissions. When using a preset ACL for description, you need to put the `x-cos-acl` header in the PUT Bucket/Object or PUT Bucket/Object ACL and describe the required permission. If an XML description is also carried in the request body, the description in the header is used and the XML description in the request body is ignored.

**Preset ACLs for buckets**

| Name | Description |
| ------------------ | ------------------------------------------------------------------ |
| private | The creator (root account) has the FULL_CONTROL permission, while others have no permissions. (Default) |
| public-read | The creator has the FULL_CONTROL permission, and the anonymous user group has the READ permission. |
| public-read-write | Both the creator and the anonymous user group have the FULL_CONTROL permission, which is generally not recommended. |
| authenticated-read | The creator has the FULL_CONTROL permission, and the authenticated user group has the READ permission. |

**Preset ACLs for objects**

| Name                  | Description                                                                         |
| ------------------------- | ---------------------------------------------------------------------------- |
| default                   | An empty description. The explicit settings of each level of directory and the settings of the bucket are used to determine whether a request is allowed. (Default) |
| private | The creator (root account) has the FULL_CONTROL permission, while others have no permissions. |
| public-read | The creator has the FULL_CONTROL permission, and the anonymous user group has the READ permission. |
| authenticated-read | The creator has the FULL_CONTROL permission, and the authenticated user group has the READ permission. |
| bucket-owner-read | The creator has the FULL_CONTROL permission, and the bucket owner has the READ permission. |
| bucket-owner-full-control | Both the creator and the bucket owner have the FULL_CONTROL permission. |

>?The public-read-write permission is not supported for objects.
>

## Example
### Bucket ACL
When you create a bucket, COS creates a default ACL to grant the resource owner the full control over the resource (FULL_CONTROL), as shown in the following example:

```xml
<AccessControlPolicy>
  <Owner>
    <ID>Owner-Cononical-CAM-User-Id</ID>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee>
        <ID>Owner-Cononical-CAM-User-Id</ID>
      </Grantee>
      <Permission>FULL_CONTROL</Permission>
    </Grant>
  </AccessControlList>
</AccessControlPolicy>
```

### Object ACL

**When you create an object, COS does not create an ACL by default, and the object owner is the bucket owner.** The object's permissions inherited from its bucket are the same with the access permissions of the bucket. Since the object does not have a default ACL, it will follow the definition of visitors and behaviors in the bucket policy to determine if the request is granted. For more information, see [Access Policy Language Overview](https://intl.cloud.tencent.com/document/product/436/18023).

If you need to grant additional access permissions to the object, you can add more ACLs to describe the access permissions of the object. For example, grant an anonymous user the permission to read a single object, as shown below:

```xml
<AccessControlPolicy>
  <Owner>
    <ID>Owner-Cononical-CAM-User-Id</ID>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee>
        <ID>Owner-Cononical-CAM-User-Id</ID>
      </Grantee>
      <Permission>FULL_CONTROL</Permission>
    </Grant>
    <Grant>
      <Grantee>
        <URI>http://cam.qcloud.com/groups/global/AllUsers</URI>
      </Grantee>
      <Permission>READ</Permission>
    </Grant>
  </AccessControlList>
</AccessControlPolicy>
```



