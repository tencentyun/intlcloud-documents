## ACL Overview
Access Control List (ACL) is a resource-based access policy option that manages access to buckets and objects. You can grant read and write permissions to other root accounts, sub-accounts and user groups using ACLs.

**Unlike an access policy, an ACL in Tencent Cloud has the following limits on the permissions:**
- Only supports permission grants to Tencent Cloud accounts.
- Only supports five operation sets: Read Objects, Write to Objects, Read ACLs, Write to ACLs, and All Permissions.
- Does not support additional conditions for the ACL rules to take effect.
- Does not support explicit deny.

**Control granularities supported by ACLs**
- Bucket
- Object Key Prefix
- Object

## Control Elements of ACLs
When a bucket or object is created, the root account to which the bucket or object's resources belong has full access to these resources, and the access cannot be modified or deleted. You can use ACLs to grant other Tencent Cloud accounts the access permissions.
The following is an ACL example for a bucket. 100000000001 is the root account, 100000000011 is its sub-account, and 100000000002 is another root account. The ACL contains an Owner element that identifies the bucket owner, who has full access to the bucket. The Grant element grants anonymous read permission, which is expressed as READ permission of `http://cam.qcloud.com/groups/global/AllUsers`.

```shell
<AccessControlPolicy>
  <Owner>
    <ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
    <DisplayName>qcs::cam::uin/100000000001:uin/100000000001</DisplayName>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RootAccount">
        <ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
        <DisplayName>qcs::cam::uin/100000000001:uin/100000000001</DisplayName>
      </Grantee>
      <Permission>FULL_CONTROL</Permission>
    </Grant>
    <Grant>
      <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="Group">
        <URI>http://cam.qcloud.com/groups/global/AllUsers</URI>
      </Grantee>
      <Permission>READ</Permission>
    </Grant>
  </AccessControlList>
</AccessControlPolicy>
```



#### Grantees
**Root account**
You can grant access permissions to other root accounts using the definition of the principal in CAM, as described below:
```bash
qcs::cam::uin/100000000002:uin/100000000002
```

**Sub-account**
You can grant access permissions to sub-accounts (such as 100000000011) under your root account or those under other root accounts using the definition of the principal in CAM, as described below:
```bash
qcs::cam::uin/100000000001:uin/100000000011
```

**Anonymous user**
You can grant access permissions to anonymous users using the definition of the principal in CAM, as described below:
```bash
http://cam.qcloud.com/groups/global/AllUsers
```

#### Operation Set
The operation sets supported by ACLs are listed below.

| Operation Set | Access to Bucket | Access to Prefix | Access to Object |
| ------------ | ----------------- | ---------------- | --------- |
| READ | Lists and reads objects in the bucket | Lists and reads objects in the directory | Reads objects |
| WRITE | Creates, overwrites and deletes any object in the bucket | Creates, overwrites and deletes any object in the directory | Not supported |
| READ_ACP | Reads the ACL of bucket | Reads the ACL in the directory | Reads the ACL of object |
| WRITE_ACP | Modifies the ACL of bucket | Modifies the ACL in the directory | Modifies the ACL of object |
| FULL_CONTROL | Any operations on the bucket and objects | Any operations on the objects in the directory | Any operations on the objects |

#### Standard ACL
COS supports a range of predefined authorizations, which are called standard ACLs. The meanings of the standard ACLs are listed below.

>!A root account always has the FULL_CONTROL permission, which is not described here.

| Standard ACL            | Description |
| ----------------- | --------------------------------------- |
| (Null) | This is the default policy. Others do not have permissions. The permissions for resources are inherited from upper level. |
| private | Other users do not have permissions |
| public-read | Anonymous user group has the READ permission |
| public-read-write | Anonymous user group has the READ and WRITE permissions. This is not recommended for buckets. |

## Directions

### Using ACLs in the console

**Set an ACL for a bucket**
The following example grants another root account the read access to a **bucket**:
![](https://main.qcloudimg.com/raw/d7fdfdcf75abd5b34fa3fc704f134ed1.png)

**Set an ACL for an object**
The following example grants another root account the read access to an **object**:
![](https://main.qcloudimg.com/raw/436257b395fd84afe85a5448d9b3280c.png)

>!If the message **You have no access to it** appears when you access a bucket or object using a sub-account, grant the sub-account the access to the bucket through the root account. For more information, see [Accessing Bucket List Using Sub-Account](https://intl.cloud.tencent.com/document/product/436/17061).

### Using ACLs via APIs

**Bucket ACL**

| API | Operation | Description |
| :----------------------------------------------------------- | :------------- | :-------------------------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | Setting bucket ACL | Sets the ACL for a specified bucket |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | Querying bucket ACL | Queries the ACL of a bucket |

**Object ACL**

| API | Operation | Description |
| :----------------------------------------------------------- | :----------- | :-------------------------------------------- |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting object ACL | Sets the ACL for a specified object in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying object ACL | Queries the ACL of an object |

