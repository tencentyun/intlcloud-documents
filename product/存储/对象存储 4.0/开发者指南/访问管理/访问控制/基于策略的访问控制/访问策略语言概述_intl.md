## Overview
An access policy which employs the JSON-based access policy language is used to grant the access to COS resources. You can authorize a specified principal to perform actions on a specified COS resource through the access policy language.

The access policy language describes the basic elements and usage for the bucket policy. For more information, see [CAM Policy Management](https://cloud.tencent.com/document/product/598/10600).

## Elements in an Access Policy

The access policy language contains the following basic elements:
- Principal: Describes the entity to be authorized by the policy. This includes users (developers, sub accounts, anonymous users), and user groups. This element can only be used in bucket access policies, rather than user access policies.
- Statement: Describes the detailed information of one or more permissions. This element includes a permission or a permission set of multiple elements such as effect, action, resource and condition. A policy has only one statement.
  - Effect: Describes whether the result produced by the declaration is "Allow" or "Deny". This includes two situations: allow and deny. This element is required.
  - Action: Describes allowed or disallowed actions. An action can be an API (described using the prefix "name") or a feature set (a set of specific APIs, described using the prefix "permid"). This element is required.
  - Resource: Describes the detailed data of authorization. A resource is described using 6-piece format. Detailed resource definition for each product is different. For information on how to specify a resource, see the documentation for the product whose resources you're writing a statement for. This element is required.
  - Condition: Describes the condition for the policy to become effective. A condition consists of operator, operational key and operate value. A condition value may include information such as time and IP address. Some services allow you to specify additional values in conditions. This element is optional.

## How to Use Elements
### Specify a principal
A principal is used to specify the user, account, service, or another entity that is allowed or not allowed to access resources. It only works in buckets, and is not required in user policies because these policies are directly added to the specific user. The following example specifies a principal.
```json
"principal": {
  "qcs": [
    "qcs::cam::uin/1:uin/1"
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
Grant permissions to the primary account (UIN is 1200000313):
```json
"principal": {
  "qcs": [
    "qcs::cam::uin/1200000313:uin/1200000313"
  ]
}
```
Grant permissions to a sub-account (UIN is 3030313, and the primary account' UIN is 1200000313):
>**Note:**
>Before performing the operation, make sure the sub-account has been added to the sub-account list of the primary account.

```json
"principal": {
  "qcs": [
    "qcs::cam::uin/1200000313:uin/3030313"
  ]
}
```

### Specify an effect
If you don't explicitly grant access to (allow) a resource, access is implicitly denied. You can also deny access to a resource, which you might do to make sure that a user cannot access it, even if a different policy grants access. The following example specifies an Allow effect.
```json
"effect" : "allow"
```

### Specify an action
COS defines a COS action that you can specify in a policy. The specified action is just like initiation of an API request.
#### Actions on buckets
| Description | API |
| --------------------- | ------------------------ |
| name/cos:GetService   | GET Service              |
| name/cos:GetBucket    | GET Bucket (List Object) |
| name/cos:PutBucket    | PUT Bucket               |
| name/cos:DeleteBucket | DELETE Bucket            |

#### Actions on object
| Description | API |
| --------------------- | ------------- |
| name/cos:GetObject    | GET Object    |
| name/cos:PutObject    | PUT Object    |
| name/cos:HeadObject   | HEAD Object   |
| name/cos:DeleteObject | DELETE Object |

The following example specifies an action that is allowed:
```json
"action": [
  "name/cos:GetObject",
  "name/cos:HeadObject"
]
```

### Specify a resource
A resource element describes one or multiple operation objects including COS buckets or objects. All the resources can be described using the following six-piece format.
```json
qcs:project_id:service_type:region:account:resource
```

Where:
1. "qcs" is the abbreviation of qcloud service, which refers to the cloud resources of Tencent Cloud.
2. "project_id" describes the project information, which is only used to be compatible with the earlier CAM logics. It is not required in this case.
3 "service_type" describes the abbreviation of the product, for example, COS.
4. "region" describes the region information. See [Available Regions](https://cloud.tencent.com/document/product/436/6224) supported by Tencent Cloud COS.
5. "account" describes the root account information of the resource owner. "uin" and "uid" can be used to describe a resource owner. The former is QQ number of the root account. Format is uin/${uin}, e.g. uin/164256472. The latter is appid of the root account. Format is uid/${appid}, e.g. uid/1000382392. For now, the COS resource owner is described using uid, i.e., the appid of the root account.
6. "resource" describes the detailed resource information. In COS, a resource is described using the bucket XML API access name.

The following example specifies the bucket burningtest-1251500699.
```json
"resource": ["qcs::cos:ap-guangzhou:uid/1251500699:burningtest-1251500699/*"]
```

The following example specifies all objects under the folder /test/ in the bucket burningtest-1251500699.
```json
"resource": ["qcs::cos:ap-guangzhou:uid/1251500699:burningtest-1251500699/test/*"]
```

The following example specifies the object /test/1.txt in the bucket burningtest-1251500699.
```json
"resource": ["qcs::cos:ap-guangzhou:uid/1251500699:burningtest-1251500699/test/1.txt"]
```

### Specify a condition
The access policy language allows you to specify conditions when granting permissions, for example, to limit the access source of a user. Here is a list of supported conditional operators as well as general condition keys and examples.

| Conditional Operator | Description | Condition Name | Example |
| ----------------------- | ------ | ---------------- | ---------------------------------------- |
| Ip_equal | IP is equal to | qcs:ip | {"ip_equal":{"qcs:ip ":"10.121.2.0/24"}} |
| Ip_not_equal | IP is not equal to | qcs:ip | {"ip_not_equal":{"qcs:ip":["10.121.1.0/24","10.121.2.0/24"]}} |
| date_not_equal | Date is not equal to | qcs:current_time | {"date_not_equal":{"qcs:current_time":"2016-06-01T00:01:00Z"}} |
| date_greater_than | Date is greater than | qcs:current_time | {"date_greater_than":{"qcs:current_time":"2016-06-01T00:01:00Z"}} |
| date_greater_than_equal | Date is greater than or equal to | qcs:current_time | {"date_greater_than_equal":{"qcs:current_time":"2016-06-01T00:01:00Z"}} |
| date_less_than | Date is less than | qcs:current_time | {"date_less_than":{"qcs:current_time":"2016-06-01T 00:01:00Z"}} |
| date_less_than_equal | Date is less than or equal to | qcs:current_time | {"date_less_than":{"qcs:current_time":"2016-06-01T 00:01:00Z"}} |
| date_less_than_equal | Date is less than or equal to | qcs:current_time | {"date_less_than_equal":{"qcs:current_time":"2016-06-01T00:01:00Z"}} |

The following example specifies that the access IP is within the IP address range 10.121.2.0/24.

```json
"ip_equal":{"qcs:ip ":"10.121.2.0/24"}
```

The following example specifies that the access IP is 101.226.\*\*\*.185 and 101.226.\*\*\*.186.

```json
"ip_equal": {
  "qcs:ip": [
    "101.226.***.185",
    "101.226.***.186"
  ]
}
```

## Example

If, when the access source IP is 101.226.\*\*\*.185/101.226.\*\*\*.186, the root account allows anonymous users to perform GET (download) and HEAD actions on the objects in the bucket burningtest-1251500699 in South China, no authentication is required. For more information, see [Cases of Permission Setting](https://cloud.tencent.com/document/product/436/12514).

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
                "qcs::cos:cn-south:uid/1251500699:burningtest-1251500699.cn-south.myqcloud.com/*"
            ]
        }
    ]
}
```

