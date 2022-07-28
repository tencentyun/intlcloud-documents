## Overview
Access policies can be used to grant access to CDWPG instances. They use JSON-based access policy syntax. You can authorize specified principals to perform specified operations on specified CDWPG resources through the access policy syntax.

The access policy syntax describes the basic elements and usage of the policy. For the description of the policy syntax, see [Permissions and Policies](https://intl.cloud.tencent.com/document/product/598/10600).

## Elements in Access Policy
An access policy contains the following elements with basic meanings:
- **statement**: It describes the details of one or more permissions. It contains a permission or permission set of multiple other elements such as `effect`, `action`, `resource`, and `condition`. One policy must and can have only one `statement`.
- **effect**: It is required and describes the result of a statement. The result can be an "allow" or "explicit deny".
- **action**: It is required and describes the allowed or denied action (operation). An operation can be an API (prefixed with "name") or a feature set (a set of specific APIs prefixed with "permid").
- **resource**: It is required and describes the details of authorization. A resource is described in a six-segment format. Detailed resource definitions vary by product.
- **condition**: It is optional and describes the condition for the policy to take effect. A condition consists of operator, action key, and action value. A condition value may contain information such as time and IP address. Some services allow you to specify additional values in a condition.

## Element Usage
### Specifying effect
If access to a resource is not explicitly granted (allowed), then it is implicitly denied. It can also be explicitly denied, which ensures that users cannot access the resource even if they are granted the access permission by other policies. Below is an example of specifying the "allow" effect:
```json
"effect" : "allow"
```

### Specifying action
CDWPG defines console operations that can be specified in a policy. The specified operations are divided into reading part of APIs (cdwpg:Describe\*) and all APIs (cdwpg:\*) according to the operation nature.

Below is an example of specifying the allowed operations:
```
"action": [
  "name/cdwpg:Describe*"
]
```

### Specifying resource
The `resource` element describes one or more operation objects, such as CDWPG resources. All resources can use the following six-segment format:
```
qcs:project_id:service_type:region:account:resource
```
The parameters are as detailed below:

| Parameter | Description | Required |
| ------------ | ------------------------------------------------------------ | -------- |
| qcs | Tencent Cloud service abbreviation, which indicates a service of Tencent Cloud | Yes |
| project_id | Project information, which is only used to enable compatibility with legacy CAM logic and generally can be left empty | No |
| service_type | Product abbreviation, which is `cdwpg` here | Yes |
| region | Region information | Yes |
| account | Root account information of the resource owner, i.e., root account UIN in the format of `uin/${OwnerUin}`, such as uin/100000000001 | Yes |
| resource | Resource details prefixed with `cdwpg-instance` | Yes |

Below is a sample six-segment CDWPG resource description:
```
"resource":["qcs::cdwpg:ap-guangzhou:uin/100000000001:cdwpg-instance/snova-73jingds"]
```

### Specifying condition
The access policy syntax allows you to specify the condition when granting permissions, which is mainly used to set tag authentication in CDWPG. The tag condition takes effect only for clusters bound with the tag. Below is a sample tag policy:
```json
 "condition": {
                "for_any_value:string_equal": {
                    "qcs:tag": [
                        "jing&jingfdd"
                    ]
                }
            }
```
This statement means that the policy contains resources whose tag key is `jing` and tag value is `jingfdd`.

## Use Cases
In the following case, the policy is to allow access to the resource whose cluster ID is `snova-jidnshgdsh` under UIN 1250000000 and the resources whose tag key is `testkey` and tag value is `testvalue`.
```json
{
   "version": "2.0",
    "statement": [
        {
            "action": [
                "name/cdwpg:Describe*",
            ],
            "condition": {
               "for_any_value:string_equal": {
                    "qcs:tag": [
                        "testkey&testvalue"
                    ]
                }
            },
            "effect": "allow",
            "resource": [
                "qcs::cdwpg:ap-guangzhou:uin/1250000000:cdwpg-instance/snova-jidnshgdsh"
            ]
        }
    ]
}
```

