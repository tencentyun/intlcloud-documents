## Overview

Access policies can be used to grant access to TMP instances. They use JSON-based access policy syntax. You can authorize specified principals to perform specified operations on specified TMP resources through the access policy syntax.

The access policy syntax describes the basic elements and usage of the policy. For the description of the policy syntax, please see [Permission](https://intl.cloud.tencent.com/document/product/598/10600).

## Elements in Access Policy

An access policy contains the following elements with basic meanings:

- **statement**: it describes the details of one or more permissions. It contains a permission or permission set of multiple other elements such as `effect`, `action`, `resource`, and `condition`. One policy must and can have only one `statement`.
- **effect**: it is required and describes the result of a statement. The result can be an "allow" or "explicit deny".
- **action**: it is required and describes the allowed or denied action (operation). An operation can be an API (prefixed with "name") or a feature set (a set of specific APIs prefixed with "permid").
- **resource**: it is required and describes the details of authorization. A resource is described in a six-segment format. Detailed resource definitions vary by product.
- **condition**: it is optional and describes the condition for the policy to take effect. A condition consists of operator, action key, and action value. A condition value may contain information such as time and IP address. Some services allow you to specify additional values in a condition.

## Element Usage

### Specifying effect

If access to a resource is not explicitly granted (allowed), then it is implicitly denied. It can also be explicitly denied, which ensures that users cannot access the resource even if they are granted the access permission by other policies. Below is an example of specifying the "allow" effect:

```json
"effect" : "allow"
```

### Specifying action

Cloud Monitor defines console operations that can be specified in a policy. The specified operations are divided into reading part of APIs (monitor:Describe\*) and all APIs (monitor:\*) according to the operation nature.

Below is an example of specifying the allowed operations:

```
"action": [
  "name/monitor:Describe*"
]
```

### Specifying resource

The `resource` element describes one or more operation objects, such as TMP resources. All resources can use the following six-segment format:

```plaintext
qcs:project_id:service_type:region:account:resource
```

The parameters are as detailed below:

| Parameter | Description | Required |
| ------------ | ------------------------------------------------------------ | -------- |
| qcs | Tencent Cloud service abbreviation, which indicates a service of Tencent Cloud | Yes |
| project_id | Project information, which is only used to enable compatibility with legacy CAM logic and generally can be left empty | No |
| service_type | Product abbreviation, which is `monitor` here | Yes |
| region | Region information | Yes |
| account | Root account information of the resource owner, i.e., root account ID in the format of `uin/${OwnerUin}`, such as uin/100000000001 | Yes |
| resource | Resource details prefixed with `instance` | Yes |

Below is a sample six-segment TMP resource description:

```plaintext
"resource":["qcs::monitor:ap-guangzhou:uin/100000000001:prom-instance/prom-73jingds"]
```

### Specifying condition

The access policy syntax allows you to specify the condition when granting permissions, which is mainly used to set tag authentication. The tag condition takes effect only for clusters bound with the tag. Below is a sample tag policy:

```json
"condition": {
    "for_any_value:string_equal": {
        "qcs:tag": [
            "testkey&testvalue"
        ]
    }
}
```

This statement means that the policy contains resources whose tag key is `testkey` and tag value is `testvalue`.

## Use Cases

### Based on tag

In the following case, the policy is to allow access to the resource whose instance ID is `prom-73jingds` under UIN 1250000000 and the resources whose tag key is `testkey` and tag value is `testvalue` (if this instance doesn't have the `testkey& testvalue` tag, it cannot be accessed).

```json
{
   "version": "2.0",
    "statement": [
        {
            "action": [
                "name/monitor:*"
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
                "qcs::monitor:ap-guangzhou:uin/1250000000:prom-instance/prom-73jingds"
            ]
        }
    ]
}
```

### Based on resource

Grant the read and write permissions of specified resources based on resource ID. The root account ID is 1250000000:

- Configure read-only access to resources in the Guangzhou region.
Sample: granting the sub-user read-only access to the instance1(prom-73jingds) and instance2(prom-65jidfafk) resources.
```
{
	"version": "2.0",
	"statement": [{
		"effect": "allow",
		"action": [
			"name/monitor:Describe*"
		],
		"resource": [
			"qcs::monitor:ap-guangzhou:uin/1250000000:prom-instance/prom-73jingds",
			"qcs::monitor:ap-guangzhou:uin/1250000000:prom-instance/prom-65jidfafk"
		],
		"condition": []
	}]
}
```

- Configure partial read/write access to resources in the Guangzhou region.
Sample: granting the sub-user the permission to delete the instance1(prom-73jingds) resource
```
{
	"version": "2.0",
	"statement": [{
		"effect": "allow",
		"resource": [
			"qcs::monitor:ap-guangzhou:uin/1250000000:prom-instance/prom-73jingds"
		],
		"action": [
			"name/monitor:TerminatePrometheusInstances"
		]
	}]
}
```

