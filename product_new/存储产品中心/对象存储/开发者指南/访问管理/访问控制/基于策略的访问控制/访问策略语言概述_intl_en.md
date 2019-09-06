## Overview

An access policy which employs the JSON-based access policy language is used to grant the access to COS resources. You can authorize a specified principal to perform actions on a specified COS resource through the access policy language.

The language describes the basic elements and usage of a bucket policy. For more information, see [CAM Policy Management](https://intl.cloud.tencent.com/document/product/598/10600).

## Elements in an Access Policy

The access policy language contains the following basic elements:

- **Principal**: describes the entity to be authorized by the policy. This includes users (root accounts, sub-accounts, anonymous users), and user groups. This element can only be used in bucket access policies, rather than user access policies.
- **Statement**: describes the detailed information of one or more permissions. This element includes a permission or a permission set of multiple elements such as effect, action, resource, and condition. A policy has only one statement.
  - **Effect**: Describes whether the result of the statement is "allowed" or "explicitly denied". This includes two situations: allow and deny. This element is required.
  - **Action**: Describes allowed or denied actions. An action can be an API (described using the prefix "name") or a feature set (a set of specific APIs, described using the prefix "permid"). This element is required.
  - **Resource**: Describes the detailed data of authorization. A resource is described in a six-piece format. Detailed resource definitions vary by product. For more information on how to specify a resource, see the documentation for the product whose resources you are writing a statement for. This element is required.
  - **Condition**: Describes the condition for the policy to take effect. A condition consists of operator, action key, and action value. A condition value may contain information such as time and IP address. Some services allow you to specify additional values in conditions. This element is optional.

## How to Use Elements

### Specifying a Principal

A principal is used to specify the user, account, service, or entity that is allowed or disallowed to access resources. It only works in buckets and is not required in user policies because these policies are directly added to the specific user. The following example specifies a principal.

```json
"principal": {
  "qcs": [
    "qcs::cam::uin/100000000001:uin/100000000001"
  ]
}
```

Grant permissions to an anonymous user:

```json
"principal": {
  "qcs": [
    "qcs::cam::anonymous:anonymous"
  ]
}
```

Grant permissions to a root account (UIN: 100000000001):

```json
"principal": {
  "qcs": [
    "qcs::cam::uin/100000000001:uin/100000000001"
  ]
}
```

Grant permissions to a sub-account (UIN: 100000000011) under the root account (UIN: 100000000001):

> Before performing the operation, make sure that the sub-account has been added to the sub-account list of the root account.

```json
"principal": {
  "qcs": [
    "qcs::cam::uin/100000000001:uin/100000000011"
  ]
}
```

### Specifying an Effect

If you don't explicitly grant access to (allow) a resource, the access is implicitly denied. You can also explicitly deny access to a resource, which you might do to make sure that a user cannot access it, even if a different policy grants it access. The following example specifies an "allow" effect.

```json
"effect" : "allow"
```

### Specifying an Action

COS defines COS actions that you can specify in a policy. The specified actions are just like initiation of API requests.

#### Actions on Buckets

| Description | API |
| --------------------- | ------------------------ |
| name/cos:GetService | GET Service |
| name/cos:GetBucket | GET Bucket (List Object) |
| name/cos:PutBucket | PUT Bucket |
| name/cos:DeleteBucket | DELETE Bucket |

#### Actions on Objects

| Description | API |
| --------------------- | --------------- |
| name/cos:GetObject | GET Object |
| name/cos:PutObject | PUT Object |
| name/cos:HeadObject | HEAD Object |
| name/cos:DeleteObject | DELETE Object |

The following example specifies an action that is allowed:

```json
"action": [
  "name/cos:GetObject",
  "name/cos:HeadObject"
]
```

### Specifying a Resource

A resource element describes one or multiple action objects including COS buckets and objects. All the resources can be described in the following six-piece format.

```json
qcs:project_id:service_type:region:account:resource
```

Parameter description:

Parameter | Description | Required
--|--|--
 qcs | The abbreviation of qcloud service, which refers to Tencent Cloud services. | Yes
project_id | Describes the project information, which is only used to enable compatibility with legacy CAM logic. | No
service_type | Describes the abbreviation of the product such as COS. | Yes
region | Describes the region information. For more information, see [Regions & Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) supported by Tencent Cloud COS. | Yes
 account | Describes the root account information of the resource owner. "uin" and "uid" can be used to describe a resource owner. <br>The former is QQ number of the root account in the format of `uin/${OwnerUin}`, such as uin/100000000001. <br>The latter is APPID of the root account in the format of `uid/${appid}`, such as uid/1250000000. For now, COS resource owner is always described using uid, i.e., the APPID of the root account. | Yes
resource | Describes the detailed resource information. In COS, a resource is described using the bucket XML API access domain name. | Yes

The following example specifies the bucket examplebucket-1250000000.

```json
"resource": ["qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"]
```

The following example specifies all objects in the /folder/ folder in the bucket examplebucket-1250000000.

```json
"resource": ["qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/folder/*"]
```

The following example specifies the /folder/exampleobject object in the bucket examplebucket-1250000000.

```json
"resource": ["qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/folder/exampleobject"]
```

### Specifying a Condition

The access policy language allows you to specify conditions when granting permissions, such as limiting the access source of a user or the authorization time. The list below contains supported conditional operators as well as general condition keys and examples.

| Conditional Operator | Meaning | Condition Name | Example |
| ----------------------- | ------------ | ---------------- | ------------------------------------------------------------ |
| Ip_equal | IP is equal to | qcs:ip | {"ip_equal":{"qcs:ip ":"10.121.2.0/24"}} |
| Ip_not_equal | IP is not equal to | qcs:ip | {"ip_not_equal":{"qcs:ip":["10.121.1.0/24","10.121.2.0/24"]}} |
| date_not_equal | Time is not equal to | qcs:current_time | {"date_not_equal":{"qcs:current_time":"2016-06-01T00:01:00Z"}} |
| date_greater_than | Time is greater than | qcs:current_time | {"date_greater_than":{"qcs:current_time":"2016-06-01T00:01:00Z"}} |
| date_greater_than_equal | Time is greater than or equal to | qcs:current_time | {"date_greater_than_equal":{"qcs:current_time":"2016-06-01T00:01:00Z"}} |
| date_less_than | Time is less than | qcs:current_time | {"date_less_than":{"qcs:current_time":"2016-06-01T 00:01:00Z"}} |
| date_less_than_equal | Time is less than or equal to | qcs:current_time | {"date_less_than":{"qcs:current_time":"2016-06-01T 00:01:00Z"}} |
| date_less_than_equal | Time is less than or equal to | qcs:current_time | {"date_less_than_equal":{"qcs:current_time":"2016-06-01T00:01:00Z"}} |

The following example specifies that the access IP is within the IP range of 10.121.2.0/24.

```json
"ip_equal":{"qcs:ip ":"10.121.2.0/24"}
```

The following example specifies that the access IPs are 101.226.\*\*\*.185 and 101.226.\*\*\*.186.

```json
"ip_equal": {
  "qcs:ip": [
    "101.226.***.185",
    "101.226.***.186"
  ]
}
```

## Examples

If, when the access source IPs are 101.226.\*\*\*.185/101.226.\*\*\*.186, the root account allows anonymous users to perform GET (download) and HEAD actions on the objects in the bucket examplebucket-1250000000 in South China, no authentication is required. For more information, see [Cases of Permission Setting](https://intl.cloud.tencent.com/document/product/436/12514).

```json
{
   "version": "2.0",
   "principal": {
      "qcs": [
         "qcs::cam::anonymous:anonymous"
      ]
   },
    "statement": [
        {
            "action": [
                "name/cos:GetObject",
                "name/cos:HeadObject"
            ],
            "condition": {
                "ip_equal": {
                    "qcs:ip": [
                        "101.226.***.185",
                        "101.226.***.186"
                    ]
                }
            },
            "effect": "allow",
            "resource": [
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000.ap-guangzhou.myqcloud.com/*"
            ]
        }
    ]
}
```
