## Concept
You can grant access permissions by specifying a person to perform a specified action on specified resources under a specified condition. Generally, the following four elements are used to describe an access permission action: **identity, resource, action, and condition (optional)**.

## Elements for Access Permissions

### Tencent Cloud's identity

When you apply for a Tencent Cloud account, the system will create a root account for logging in to the Tencent Cloud services. The Tencent Cloud root account manages different types of users with different roles using the user management feature. User types include **collaborator, message recipient, sub-user, and role**. For more information, see CAM [Identity Management](https://cloud.tencent.com/document/product/598/13665) and [Glossary](https://cloud.tencent.com/document/product/598/18564).

### COS resources

 Bucket and Object are the basic resources of the COS service, and they have subresources associated with them.

Bucket's subresources include:

- acl and policy: access control information of a bucket
- website: static website hosting configuration of a bucket
- tagging: tag information of a bucket
- cors: cross-origin configuration of a bucket
- lifecycle: lifecycle configuration of a bucket

Object's subresources include:

- acl: access control information of an object
- restore: restore configuration of an archive object

### COS operations

COS provides a range of API operations on various resources. For more information, see [Operation List](https://cloud.tencent.com/document/product/436/10111).

## CAM Overview

### Private principle

**By default, all Tencent Cloud COS resources are private.**

The resource owner (the Tencent Cloud root account creating a bucket resource) has the highest permission on the resource, and can grant access permissions to others or anonymous users by editing and writing an access policy.

When a Tencent Cloud CAM account is used to create a bucket or upload an object, its parent root account is the resource owner.

The root account of the bucket owner can authorize other Tencent Cloud root accounts to upload objects (i.e. cross-account upload). In this case, the object owner is still the root account of the bucket owner.

### Access control policy

#### Resource-based policy

Tencent Cloud COS supports access control at both **bucket** and **object** dimensions, as detailed below:

| Dimension | Type | Language | Supported Identity | Supported Resource Granularity | Supported Action | Supported Effect |
| ------ | ---------------------- | -------- | ------------------------------------------------ | -------------------- | ------------------ | ------------- |
| Bucket | Access policy language (Policy) | JSON | Sub-accounts, roles, Tencent Cloud services, other root accounts, anonymous users, etc. | Buckets, objects, prefixes, etc. | Each specific action | Allow/Deny |
| Bucket | Access Control List (ACL) | XML | Other root accounts, anonymous users, etc. | Buckets | Read and write actions | Allow |
| Object | Access Control List (ACL) | XML | Other root accounts, anonymous users, etc. | Objects | Read and write actions | Allow |

**Bucket Policy**

A bucket policy is described in JSON language, and supports granting anonymous identities or any Tencent Cloud CAM account the permissions to access and perform operations on buckets and objects. In Tencent Cloud COS, the bucket policy can be used to manage almost all operations in the bucket. It is recommended that you use a bucket policy to manage access policies that cannot be described using ACLs.

>!A Tencent Cloud root account has the highest permission on its resources (including buckets). Even if you can set limits on almost all operations in the bucket policy, the root account always has the permission for the PUT Bucket Policy operation, and can call this operation without checking the bucket policy.

The following policy allows anonymous users to access all objects in the bucket `examplebucket-1250000000` in Guangzhou, and to download all objects (GetObject) in the bucket without signature verification. In this case, any anonymous user who knows the URL can download the objects (similar to public-read):

```json
{
  "Statement": [
    {
      "Principal": "*",
      "Effect": "Allow",
      "Action": ["cos:GetObject"],
      "Resource": ["qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"]
    }
  ],
  "Version": "2.0"
}
```

**ACL**

An ACL is described in the XML language. It is a list of specified grantees and permissions granted, which is associated with resources. Each bucket and object has an associated ACL to grant basic read and write permissions to anonymous users or other Tencent Clouds root accounts.

>!The resource owner always has FULL_CONTROL permission on the resource, regardless of whether this is described in the issued ACL.

The bucket ACL in this example describes the full control permission of the bucket owner (UIN: 1250000000):

```xml
<AccessControlPolicy>
  <Owner>
    <ID>qcs::cam::uin/1250000000:uin/1250000000</ID>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RootAccount">
        <ID>qcs::cam::uin/1250000000:uin/1250000000</ID>
      </Grantee>
      <Permission>FULL_CONTROL</Permission>
    </Grant>
  </AccessControlList>
</AccessControlPolicy>
```

The object ACL in this example describes the full control permission of the object owner (UIN: 1250000000) and grants the read permission to all users (the public-read permission to anonymous users):

```xml
<AccessControlPolicy>
  <Owner>
    <ID>qcs::cam::uin/1250000000:uin/1250000000</ID>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee>
        <ID>qcs::cam::uin/1250000000:uin/1250000000</ID>
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

### User-based policy

In CAM, you can grant different permissions to different types of users under the root account.

The biggest difference between a user policy and a bucket policy is that the user policy only describes the effect, the action, the resource, and the condition (optional), and does not describe the identity (principal). Therefore, after you write a user policy, associate it with a sub-user, a user group or a role. Besides, the user policy does not support granting anonymous users the permissions to access resources and perform operations.

You can [associate a preset policy for authorization](https://cloud.tencent.com/document/product/598/10602), or [write a user policy](https://cloud.tencent.com/document/product/598/10603) and associate it with a specified identity to manage access for your users.

The following policy example grants the permission to perform all COS operations on the bucket `examplebucket-1250000000` in Guangzhou. You need to save the policy and then associate it with a CAM sub-user, a user group or a role before it takes effect.

```json
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["cos:*"],
      "Resource": [
          "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*",
          "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/"
      ]
    }
  ],
  "Version": "2.0"
}
```


