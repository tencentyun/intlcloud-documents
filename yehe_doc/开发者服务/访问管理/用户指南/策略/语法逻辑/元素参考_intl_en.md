A policy is made up of elements that describe specific information of the authorization. Core elements include `principal`, `action`, `resource`, `condition`, and `effect`. These elements must be lowercase. The order of the elements does not matter. The `condition` element is optional. The `principal` element cannot be used in the console and can only be used through policy management APIs and policy syntax-related parameters.

### 1. version

This required element defines the version of policy syntax. At present, the only available value is "2.0".

### 2. principal
This element specifies the entity to be authorized by the policy. This includes users (root accounts and sub-accounts). In the future, more entities will be included, such as roles and federated users. This element can only be used in trust policies for roles and COS bucket policies.

### 3. statement
This element describes the details of one or more permissions. It contains a permission or permission set of multiple other elements such as `action`, `resource`, `condition`, and `effect`. One policy has only one `statement`.

### 4. action
This required element describes the action (operation) to be allowed or denied. An operation can be an API (prefixed with `name`) or a feature set (a set of specific APIs prefixed with `actionName`).

### 5. resource
This required element describes the objects the statement covers. A resource is described in a six-segment format. Detailed resource definitions vary by product. For more information on how to specify a resource, please see the documentation for the product whose resources you are writing a statement for.

### 6. condition
This optional element describes the condition for the policy to take effect. A condition consists of operator, action key, and action value. A condition value may contain information such as time and IP address. Some services allow you to specify additional values in a condition.

### 7. effect
This required element describes whether the statement result is an "allow" or "explicit deny".

### 8. Sample policy
The following sample policy grants a sub-account (ID: 3232523) of a root account (APPID: 1238423) permissions to use all COS read APIs, write objects, and send message queues for the COS bucket "bucketA" in the Beijing region and the COS object "object2" in the bucket "bucketB" in the Guangzhou region when the access IP falls within the IP range of `10.121.2.*`. 
```
{
  "version": "2.0",
  "statement": [
    {
      "principal": {
        "qcs": [
          "qcs::cam::uin/1238423:uin/3232523"
        ]
      },
      "effect": "allow",
      "action": [
        "cos:PutObject",
        "cos:GetObject",
        "cos:HeadObject",
        "cos:OptionsObject",
        "cos:ListParts",
        "cos:GetObjectTagging"
      ],
      "resource": [
        "qcs::cos:ap-beijing:uid/1238423:bucketA-1238423/*",
        "qcs::cos:ap-guangzhou:uid/1238423:bucketB-1238423/object2"
      ],
      "condition": {
        "ip_equal": {
          "qcs:ip": "10.121.2.10/24"
        }
      }
    },
    {
      "principal": {
        "qcs": [
          "qcs::cam::uin/1238423:uin/3232523"
        ]
      },
      "effect": "allow",
      "action": "cmqqueue:SendMessage",
      "resource": "*"
    }
  ]
}
```

### Relevant documents
For more information on `resource` in CAM, please see [Resource Description Method](https://intl.cloud.tencent.com/document/product/598/10606).
