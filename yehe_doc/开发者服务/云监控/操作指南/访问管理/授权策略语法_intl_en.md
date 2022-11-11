## Overview

An access policy that employs the JSON-based access policy language is used to grant access to Cloud Monitor (CM) resources. You can authorize a specified principal to perform actions on a specified CM resource through the access policy language.

## Policy Syntax
CAM policy:

```
{	 
        "version":"2.0", 
        "statement": 
        [ 
           { 
              "effect":"effect", 
              "action":["action"], 
              "resource":["resource"], 
               "condition": {"key":{"value"}} 
           } 
       ] 
} 

```

#### Element description
- **version** is required. Currently, only "2.0" is allowed.
- **statement** describes the details of one or more permissions. This element contains a permission or permission set of other elements such as `effect`, `action`, `resource`, and `condition`. One policy has only one statement.
 - **effect** is required. It describes whether the declaration result is `allow` or explicit `deny`.
 - **action** is required. It specifies whether to allow or deny the operation. The operation can be an API (prefixed with `name`) or a feature set (a group of APIs, prefixed with `permid`).
 - **resource** is required. It describes the authorization details. For more information on how to specify a resource, see the documentation for the product for which you are writing a resource declaration.
 - **condition** describes the condition for the policy to take effect. Conditions consist of operators, operation keys, and operation values, while condition values include information such as time and IP addresses. CM currently does not support special conditions, so this element can be left empty.



### Specifying `effect`

If you don't explicitly grant access to (`allow`) a resource, access is implicitly denied. You can also explicitly `deny` access to a resource to ensure that a user cannot access it, even if another policy has granted access to it. The following example specifies an `allow` effect.

```json
"effect" : "allow"
```

### Specifying `action`

You can specify any API operation from any CAM-enabled service in a CAM policy statement. If the service is CM, use an API prefixed with `name/monitor:`, such as `name/monitor:GetMonitorData`.

You can also specify multiple API operations using a wildcard. For example, you can specify all operations whose names begin with "Describe" as shown below:

```
"action": [
  "name/monitor:Describe*"
]
```

To specify all operations in CM, use a wildcard (*) as follows:

```
"action"：["name/monitor:*"]

```

### Specifying `resource`

The `resource` element describes one or multiple operation objects, such as CM resource. All the resources can be described with the following 6-segment format.

```plaintext
qcs:service_type:account:resource
```

The parameters are described as follows:

| Parameter | Description | Required |
| ------------ | ------------------------------------------------------------ | -------- |
| qcs | Abbreviation for “qcloud service”, which indicates a Tencent Cloud service | Yes |
| service_type | Product name abbreviation, which is `monitor` here | Yes |
| account | Root account information of the resource owner, which is the root account ID in the format of `uin/${OwnerUin}`, such as `uin/100000000001` | Yes |
| resource     | Resource information description, such as `cm-policy/policy-p1234abc`     | Yes       |

You can control the access to the following resources:

| Resource Type | Resource Description Method in Authorization Policy |
| :----------------- | :----------------------------------------- |
| Alarm policy/cm-policy | `qcs::monitor::uin/:cm-policy/${policyId}` |
| Notification template/cm-notice | `qcs::monitor::uin/:cm-notice/${noticeId}` |

**Example of specifying a resource**

You can specify a resource by its ID as follows:

```
"resource":["qcs::monitor:uin/1250000000:cm-policy/policy-p1234abc"]
```


If you want to specify all resources or if a specific API operation does not support resource-level permission, you can use the wildcard (*) in the `resource` element as shown below:

```
"resource": ["*"]
```

## Console Example

**Granting particular alarm policy permissions to a user**

1. Create a custom policy as instructed in [Creating Custom Policy](https://intl.cloud.tencent.com/document/product/598/35596).
The sample policy grants the operation permission for two alarm policies (IDs: `policy-p1234abc` and `policy-p5678abc`). You can refer to the following policy syntax to configure the policy content:

```
{
    "version": "2.0",
    "statement": [
        {
            "action": "monitor:*",
            "resource": [
                        "qcs::monitor:uin/1250000000:cm-policy/policy-p1234abc",
                        "qcs::monitor:uin/1250000000:cm-policy/policy-p5678abc"
                        ],
            "effect": "allow"
        }
    ]
}
```

2. Find the created policy and click **Associate Users/Groups** in the **Operation** column.
3. In the pop-up window, select the user/group you want to authorize and click **OK**.







