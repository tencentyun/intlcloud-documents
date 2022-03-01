**COS resources (buckets and objects) are private by default.** Only Tencent Cloud root accounts (resource owners) can access and modify buckets and objects. Other users (such as sub-accounts and anonymous users) cannot access objects by using URLs without authorization.

After creating a Tencent Cloud sub-account, you can configure an access policy to authorize the sub-account. If you want to open up resources (buckets, objects, and directories) to non-Tencent Cloud users, you only need to set the permissions of the resources to Public Read.

![](https://qcloudimg.tencent-cloud.cn/raw/90b71308a1e1e6f1a842d0c7bd8c44d6.png)

## Elements for Access Permissions

You can grant access permissions by specifying a person to perform a specified action on specified resources under a specified condition. Generally, the following four elements are used to describe an access permission action: **identity, resource, action, and condition (optional)**.

![](https://qcloudimg.tencent-cloud.cn/raw/76920126347974448795fd58f7b8d26d.png)

## Access Permission Elements

#### Tencent Cloud identity (principal)

When you apply for a Tencent Cloud account, the system will create a root account for logging in to Tencent Cloud services. The Tencent Cloud root account manages different types of users with different roles using the user management feature. User types include **collaborator, message recipient, sub-user, and role**. For more information, see [User Types](https://intl.cloud.tencent.com/document/product/598/32633) and [Glossary](https://intl.cloud.tencent.com/document/product/598/18564) of CAM.

>?Assume that you are to authorize an employee in your enterprise, you need to create a sub-account in the [CAM console](https://console.cloud.tencent.com/cam) and then set specific permissions for the sub-account by using one or more of the following methods: [Bucket Policy](link), [ACL](link), and [User Policy](link).

#### COS resources

Buckets and objects are basic resources of the COS service. Folders are a special type of object. You can authorize objects in folders by authorizing the folders. For more information, see [Setting Folder Permissions](https://intl.cloud.tencent.com/document/product/436/35261).

Buckets and objects have subresources associated with them.

Subresources of buckets include:

- acl and policy: access control list of a bucket
- website: static website hosting configuration of a bucket
- tagging: tag information of a bucket
- cors: cross-origin resource sharing (CORS) configuration of a bucket
- lifecycle: lifecycle configuration of a bucket

Subresources of objects include:

- acl: access control information of an object
- restore: restoration configuration of an archive object

#### COS operations (actions)

COS provides a range of API operations on various resources. For more information, see [Operation List](https://intl.cloud.tencent.com/document/product/436/10111).

#### COS conditions (optional)

COS conditions refer to conditions for permissions to take effect, such as VPC and VIP. For more information, see [Condition](https://intl.cloud.tencent.com/document/product/598/10608).

## Private Principle

>?Tencent Cloud COS resources are private by default.

- The resource owner (the Tencent Cloud root account creating a bucket resource) has the highest permission on the resource, and can grant access permissions to others or anonymous users by writing or modifying an access policy.
- When a Tencent Cloud [CAM](https://intl.cloud.tencent.com/document/product/598/10583) account is used to create a bucket or upload an object, its parent root account is the resource owner.
- The root account of the bucket owner can authorize other Tencent Cloud root accounts to upload objects (i.e. cross-account upload). In this case, the object owner is still the root account of the bucket owner.

## Access Control Methods

COS provides multiple permission setting methods to implement access control, including bucket policies, user policies (CAM policies), bucket ACLs, and object ACLs.

These methods can be classified into resource-based authorization and user-based authorization according to the starting point of policy setting, and classified into policy-based authorization and ACL-based authorization according to the authorization mode.

![](https://qcloudimg.tencent-cloud.cn/raw/332efdd73dc362ef889257cdfbd4d686.png)

**Classification method 1: resource-based authorization vs user-based authorization**
![](https://qcloudimg.tencent-cloud.cn/raw/fdc1f3434c0e75425f2a650a4ece79ec.png)
- Resource-based authorization: resource policies associate permissions with specific resources, including bucket policies, bucket ACLs, and object ACLs. Resource policies can be configured by using the COS console or APIs.
- User-based authorization: user policies (CAM policies) associate permissions with users. When configuring a user-based policy, you do not need to specify users. Instead, you only need to specify resources, operations, conditions, and so on. User policies can be configured in the [CAM console](https://console.cloud.tencent.com/cam).

**Classification method 2: policy-based authorization vs ACL-based authorization**
![](https://qcloudimg.tencent-cloud.cn/raw/5949e32de545aad4e878400e42dfef4c.png)
- Policy-based authorization: both user policies (CAM policies) and bucket policies implement authorization based on complete policy syntax. They authorize refined actions specific to each API and allow specifying the `allow` or `deny` effect.
- ACL-based authorization: bucket ACLs and object ACLs are implemented based on ACLs. An ACL is a list of specified grantees and permissions granted, and is associated with resources and corresponds to organized and abstracted permissions. ACLs allow specifying only the `allow` effect.


### Resource-based policy

Resource-based policies are classified into three types: bucket policies, bucket ACLs, and object ACLs. COS supports access control at both the **bucket** and **object** dimensions, as detailed below:

| Dimension | Type | Language | Supported Identity | Supported Resource Granularity | Supported Action | Supported Effect |
| ------ | ---------------------- | -------- | ------------------------------------------------ | -------------------- | ------------------ | ------------- |
| Bucket | Access policy language (Policy) | JSON | Sub-accounts, roles, Tencent Cloud services, other root accounts, anonymous users, etc. | Buckets, objects, prefixes, etc. | Each specific action | Allow/Deny |
| Bucket | Access Control List (ACL) | XML | Other root accounts, anonymous users, etc. | Buckets | Read and write actions | Allow |
| Object | Access Control List (ACL) | XML | Other root accounts, anonymous users, etc. | Objects | Read and write actions | Allow |

<span id="Bucket policy"></span>
#### Bucket policy

A bucket policy is described in JSON language, and supports granting anonymous identities or any Tencent Cloud [CAM](https://intl.cloud.tencent.com/document/product/598/10583) account the permissions to access and perform operations on buckets and objects. In Tencent Cloud COS, the bucket policy can be used to manage almost all operations in the bucket. It is recommended that you use a bucket policy to manage access policies that cannot be described using ACLs. For more information, see [Bucket Policy](link).

>!A Tencent Cloud root account has the highest permission on its resources (including buckets). Even if you can set limits on almost all operations in the bucket policy, the root account always has the permission for the PUT Bucket Policy operation, and can call this operation without checking the bucket policy.


The following policy allows anonymous users to access all objects in the bucket `examplebucket-1250000000` in Guangzhou, and to download all objects (via `GetObject`) in the bucket without signature verification. In this case, any anonymous user who knows the URLs can download the objects (similar to Public Read):

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

<span id="ACL"></span>
#### ACL

An ACL is described in the XML language. It is a list of specified grantees and permissions granted, which is associated with resources. Each bucket and object has an associated ACL to grant basic read and write permissions to anonymous users or other Tencent Clouds root accounts. For more information, see [ACL](link).

>!The resource owner always has the FULL_CONTROL permission on the resource, regardless of whether this is described in the issued ACL.
>

The bucket ACL in this example describes the full control permission of the bucket owner (UIN: 100000000001):

```xml
<AccessControlPolicy>
  <Owner>
    <ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RootAccount">
        <ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
      </Grantee>
      <Permission>FULL_CONTROL</Permission>
    </Grant>
  </AccessControlList>
</AccessControlPolicy>
```

The object ACL in this example describes the full control permission of the object owner (UIN: 100000000001) and grants the read permission to all users (the public-read permission to anonymous users):

```xml
<AccessControlPolicy>
  <Owner>
    <ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee>
        <ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
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


<span id="User policy"></span>
#### User policy

In [CAM](https://intl.cloud.tencent.com/document/product/598/10583), you can grant different permissions to different types of users under the root account.

The biggest difference between a user policy and a bucket policy is that the user policy only describes effect, action, resource, and condition (optional), but not principal. Therefore, you have to write a user policy first, and then associate it manually with a sub-user, a user group or a role. Besides, the user policy cannot grant anonymous users access to resources or operations.

You can [associate a preset policy for authorization](https://intl.cloud.tencent.com/document/product/598/10602), or [write a user policy](https://intl.cloud.tencent.com/document/product/598/10603) and associate it with a specified identity to manage access for your users. For more information, see [User Policy](link).

The following policy example grants the permission to perform all COS operations on the bucket `examplebucket-1250000000` in Guangzhou. You need to save the policy and then associate it with a [CAM](https://intl.cloud.tencent.com/document/product/598/10583) sub-user, a user group or a role before it takes effect.

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


