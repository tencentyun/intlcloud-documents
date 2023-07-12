>!When adding access policies to a sub-user or collaborator, be sure to grant the minimum set of API access permissions needed to satisfy your business needs. There may be data security risks associated with granting excessive access to all of your resources `(resource:*)` or all operations `(action:*)`.
>

## Overview

An access policy that employs the JSON-based access policy language is used to grant access to Cloud Object Storage (COS) resources. You can authorize a specified principal to perform actions on a specified COS resource through the access policy language.

The language describes the basic elements and usage of a bucket policy. For more information, see [CAM Policy Management](https://intl.cloud.tencent.com/document/product/598/10600).

## Elements in an Access Policy

The access policy language contains the following basic elements:

- **principal**: describes the entity to be authorized by the policy. This includes users (root accounts, sub-accounts, anonymous users) and user groups. This element can only be used in bucket access policies, rather than user access policies.
- **statement**: describes the detailed information of one or more permissions. This element includes a permission or a permission set of multiple elements such as effect, action, resource, and condition. A policy has only one statement.
- **effect**: describes the result of a statement. The result can be "allow" or an explicit "deny". This element is required.
- **action**: describes the allowed or denied operation. An operation can be an API (described using the prefix "name") or a feature set (a set of specific APIs prefixed with "permid"). This element is required.
- **resource**: describes the resource to which the permission applies. A resource is described in a six-segment format. Detailed resource definitions vary by product. For more information on how to specify a resource, see the documentation for the product whose resources you are writing a statement for. This element is required.
- **condition**: describes the condition for the policy to take effect. A condition consists of operator, action key, and action value. A condition value may contain information such as time and IP address. Some services allow you to specify additional values in a condition. This element is optional.

## How to Use Elements

### Specifying a principal

A principal is used to specify the user, account, service, or another entity that is allowed or not allowed to access resources. It only works in buckets, and is not required in user policies because these policies are directly added to the specific user. The following example specifies a principal.

```json
"principal":{
"qcs":[
"qcs::cam::uin/100000000001:uin/100000000001"
]
}
```

Grant permissions to an anonymous user:

```json
"principal":{
"qcs":[
"qcs::cam::anonymous:anonymous"
]
}
```

Grant permissions to a root account (UIN: 100000000001):

```json
"principal":{
"qcs":[
"qcs::cam::uin/100000000001:uin/100000000001"
]
}
```

Grant permissions to a sub-account (UIN: 100000000011) under the root account (UIN: 100000000001):

>! Before performing the operation, make sure that the sub-account has been added to the sub-account list of the root account.
>

```json
"principal":{
"qcs":[
"qcs::cam::uin/100000000001:uin/100000000011"
]
}
```

### Specifying an effect

If you don't explicitly grant access to (`allow`) a resource, access is implicitly denied (`deny`). You can also deny access to a resource, which you might do to make sure that a user cannot access it, even if a different policy grants access. The following example specifies an `allow` effect.

```json
"effect" : "allow"
```

### Specifying an action

COS defines actions that you can specify in a policy. The actions are exactly the same as COS API operations. The following lists only part of the actions on buckets and objects. For more information, see [Operation List](https://intl.cloud.tencent.com/document/product/436/10111).

#### Actions on buckets


| Description | API |
| --------------------- | ------------------------ |
| name/cos:GetService | GET Service |
| name/cos:GetBucket | GET Bucket (List Objects) |
| name/cos:PutBucket | PUT Bucket |
| name/cos:DeleteBucket | DELETE Bucket |

#### Actions on objects

| Description | API |
| --------------------- | --------------- |
| name/cos:GetObject | GET Object |
| name/cos:PutObject | PUT Object |
| name/cos:HeadObject | HEAD Object |
| name/cos:DeleteObject | DELETE Object |

The following example specifies an action that is allowed:

```json
"action":[
"name/cos:GetObject",
"name/cos:HeadObject"
]
```

### Specifying a resource

The `resource` element describes one or multiple operation objects including COS buckets or objects. All the resources can be described using the following 6-segment format.

```json
qcs:project_id:service_type:region:account:resource
```

The parameters are described as follows:

Parameter | Description | Required
--|--|--
qcs | Abbreviation of the qcloud service, which refers to Tencent Cloud services. | Yes
project_id | Describes the project information, which is only used to enable compatibility with legacy CAM logic. | No
service_type | Describes the abbreviation of the product such as COS. | Yes
region | Describes the region information. For more information, see [Regions & Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) supported by Tencent Cloud COS. | Yes
account | Describes the root account information of the resource owner. Currently, `uin` or `uid` can be used to describe the resource owner. `uin` is the UIN of the root account. It is expressed in the format of `uin/${OwnerUin}`, for example, `uin/100000000001`. `uid` is the app ID of the root account. It is expressed in the format of `uid/${appid}`, for example, `uid/1250000000`. Currently, COS resource owners are all described using `uid`, i.e., the app ID of the root account. | Yes
resource | Describes the detailed resource information. In COS, a resource is described using the bucket XML API access domain name. | Yes

The following example specifies the bucket `examplebucket-1250000000`.

```json
"resource": ["qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"]
```

The following example specifies all objects in the `/folder/` folder in the bucket `examplebucket-1250000000`.

```json
"resource": ["qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/folder/*"]
```

The following example specifies the `/folder/exampleobject` object in the bucket `examplebucket-1250000000`.

```json
"resource": ["qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/folder/exampleobject"]
```

### Specifying a condition

The access policy language allows you to specify conditions when granting permissions, for example, to limit the access source of a user. Here is a list of supported conditional operators as well as general condition keys and examples.

| Conditional Operator | Description | Condition Name | Example |
| ----------------------- | ------------ | ---------------- | ------------------------------------------------------------ |
| Ip_equal | IP is equal to | qcs:ip | {"ip_equal":{"qcs:ip ":"10.121.2.0/24"}} |
| Ip_not_equal | IP is not equal to | qcs:ip | {"ip_not_equal":{"qcs:ip":["10.121.1.0/24","10.121.2.0/24"]}} |


The following example allows access to only IPs in the `10.121.2.0/24` IP range.

```json
"ip_equal":{"qcs:ip ":"10.121.2.0/24"}
```

The following example allows access to only the IPs 101.226.100.185 and 101.226.100.186.

```json
"ip_equal":{
    "qcs: ip": [
        "101.226.100.185",
        "101.226.100.186"
    ]
}
```

## Examples

If, when the access source IPs are 101.226.100.185 and 101.226.100.186, the root account allows anonymous users to perform GET (download) and HEAD actions on the objects in the bucket `examplebucket-1250000000` in South China, no authentication is required. For more information, see [Cases of Permission Setting](https://intl.cloud.tencent.com/document/product/436/12514).

```json
{
    "version": "2.0",
    "principal":{
        "qcs":[
            "qcs: : cam: : anonymous: anonymous"
        ]
    },
    "statement": [
        {
            "action":[
                "name/cos: GetObject",
                "name/cos: HeadObject"
            ],
            "condition":{
                "ip_equal":{
                    "qcs: ip": [
                        "101.226.100.185",
                        "101.226.100.186"
                    ]
                }
            },
            "effect": "allow",
            "resource": [
                "qcs: : cos: ap-guangzhou: uid/1250000000: examplebucket-1250000000.ap-guangzhou.myqcloud.com/*"
            ]
        }
    ]
}
```
