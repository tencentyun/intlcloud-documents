## ACL Overview
Access Control List (ACL) is one of the resource-based access policy options you can use to manage access to your buckets and objects. It can be used to grant basic read and write permissions to other root accounts, sub-accounts and user groups.

#### Different from an access policy, there are some restrictions when managing permissions with an ACL:
- Permissions can only be granted to Tencent Cloud account.
- Only five action sets are supported, including reading objects, writing to objects, reading ACLs, writing to ACLs, and all permissions.
- Specifying conditions in which a policy takes effect is not allowed.
- Deny effect is not supported.

#### Control granularities supported by ACLs:
- Bucket
- Object key prefix
- Object

## Control Elements on ACLs
When a bucket or object is created, the primary account to which its resources belong have all of the permissions on these resources, which cannot be modified or deleted. You can use ACLs to grant other Tencent Cloud accounts the access permission. Here is an example of a bucket ACL.
```xml
<AccessControlPolicy>
  <Owner>
    <ID>qcs::cam::uin/12345:uin/12345</ID>
    <DisplayName>qcs::cam::uin/12345:uin/12345</DisplayName>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RootAccount">
        <ID>qcs::cam::uin/12345:uin/12345</ID>
        <DisplayName>qcs::cam::uin/12345:uin/12345</DisplayName>
      </Grantee>
      <Permission>FULL_CONTROL</Permission>
    </Grant>
    <Grant>
      <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RootAccount">
        <ID>qcs::cam::uin/54321:uin/54321</ID>
        <DisplayName>qcs::cam::anyone:anyone</DisplayName>
      </Grantee>
      <Permission>READ</Permission>
    </Grant>
  </AccessControlList>
</AccessControlPolicy>
```
The above ACL contains an owner element to identify the bucket. The bucket owner have all permissions on the bucket. The Grant element grants anonymous users the READ permission, which is described in the format of `qcs::cam::anyone:anyone`.

### Grantees
#### Root account
You can grant access permissions to other root accounts using the definition of the principal in CAM, as described below:
```
qcs::cam::uin/1238423:uin/1238423
```

#### Sub-account
You can grant permissions to sub-accounts under your root account or those under other root accounts using the definition of the principal in CAM, as described below:
```
qcs::cam::uin/1238423:uin/3232
```

### Anonymous user
You can grant access permissions to anonymous users using the definition of the principal in CAM, as described below:
```
qcs::cam::anyone:anyone
```

### Action set
The following table lists the action sets supported by ACLs.

| Action Set | Bucket | Prefix | Object |
| ------------ | ----------------- | ---------------- | --------- |
| READ | Lists and reads objects in the bucket | Lists and reads objects in the directory | Reads objects |
| WRITE | Creates, overwrites and deletes any object in the bucket | Creates, overwrites and deletes any object in the directory | Overwrites and deletes objects |
| READ_ACP | Reads the ACL for the bucket | Reads the ACL under the directory | Reads the ACL for the object |
| WRITE_ACP | Modifies the ACL for the bucket | Modifies the ACL under the directory | Modifies the ACL for the object |
| FULL_CONTROL | Performs any operation on buckets and objects | Performs any operation on objects in the directory | Performs any operation on objects |

### Standard ACL description
COS supports a range of predefined authorizations, called standard ACLs. The following table lists the meaning of each standard ACL.
> **Notes:**
> Since the primary account always has the FULL_CONTROL permission, no other explanations will be described below.

| Standard ACL | Meaning |
| ----------------- | --------------------------------------- |
| (Null) | This is the default policy. Others do not have permissions. Resources inherit the permissions from upper level. |
| private | Others do not have permissions |
| public-read | The anonymous user group has the READ permission |
| public-read-write | The anonymous user group has the READ and WRITE permissions, which is generally not recommended for buckets. |

## ACL Examples
### Set an ACL for a bucket
The following example grants another root account the read access to a bucket:
![](//mc.qcloudimg.com/static/img/7088f7b6c3336668b4b04f63392e069d/image.jpg)

### Set an ACL for an object
The following example grants another root account the read access to an object:
![](//mc.qcloudimg.com/static/img/9ed379e66236d84bdd3c070e99f95e7d/image.jpg)

