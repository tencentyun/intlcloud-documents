### Use Cases

In many cases, you may need to add conditions to created policies for tighter control. Policies only take effect when configured conditions are met.
Scenario 1: if you want to restrict the access source of users calling a TencentCloud API, you can add an IP condition to the existing policy.
Scenario 2: when a CAM user calls the VPC peering connection API, in addition to checking whether the user has access to the API and related resources, you also need to check whether the user has access to the VPC associated with the peering connection.
    

### Syntax Structure	

The syntax structure of condition is as shown below. A condition block consists of multiple subblocks. Each subblock corresponds to one condition operator and several condition keys. Each condition key contains several condition values.
![](https://mc.qcloudimg.com/static/img/4c47f9d1a72dfcdd76a7c3837711ae07/600.png)
    
    

### Evaluation Logic

The evaluation logic that makes a condition take effect is as follows:


> ? Authorization by tag only supports `for_any_value`. For more information, please see [Authorizing by tag](https://intl.cloud.tencent.com/document/product/598/35596#authorizing-by-tag).

1. A condition key can contain multiple condition values. The condition is met as long as the key in the context matches any of the condition values upon execution of the associated condition operator.

2. If a subblock has multiple condition keys, the subblock is met only if all conditions that correspond to all condition keys are satisfied.

3. If a block contains multiple subblocks, the entire condition is met only if all subblocks are satisfied.

4. For a condition operator ending in `_if_exist`, the condition is met even if the context does not include the condition key associated with the condition operator.

5. `for_all_value` is a qualifier that restricts the condition operator. It is applicable to scenarios where the condition key in the context contains multiple values. The entire condition is met only if all values of the condition key is satisfied upon execution of the associated condition operator.

6. `for_any_value` is a qualifier that restricts the condition operator. It is applicable to scenarios where the condition key in the context contains multiple values. The entire condition is met as long as any value of the condition key is satisfied upon execution of the associated condition operator.

### Samples

1. In the following example, to call the `cos:PutObject` API, the user must be in the `10.217.182.3/24` or `111.21.33.72/24` IP range:

```
{
    "version": "2.0",
    "statement":[
    {
        "effect": "allow",
        "action": "cos:PutObject",
        "resource": "*",
        "condition": {
            "ip_equal": {
                "qcs:ip": [
                    "10.217.182.3/24",
                    "111.21.33.72/24"
                ]
            }
        }
    }
  ]  
}
```

2. In the following example, the VPC region must be `Shanghai` in order for it to be bound to a specified peering connection:

```
{
    "version": "2.0",
    "statement": [
    {
        "effect": "allow",
        "action": "name/vpc:AcceptVpcPeeringConnection",
        "resource": "qcs::vpc:sh::pcx/2341",
        "condition": {
            "string_equal_if_exist": {
                "vpc:region": "sh"
            }
        }
    }
   ]
}
```

### Condition Operator List

The following table lists condition operators, condition names, and examples. For more information on customizing condition keys for individual products, please see the corresponding product documentation.


| Condition Operator | Description | Condition Name | Example |
| ---------------------------- | -------------------------- | ---------------- | ------------------------------------------------------------ |
| string_equal                 | String is equal to (case-sensitive)     | qcs:tag          | {"string_equal":{"qcs:tag/tag_name1":"tag_value1"}}          |
| string_not_equal             | String is not equal to (case-sensitive)   | qcs:tag          | {"string_not_equal":{"qcs:tag/tag_name1":"tag_value1"}}      |
| string_equal_ignore_case     | String is equal to (case-insensitive)   | qcs:tag          | {"string_equal_ignore_case":{"qcs:tag/tag_name1":"tag_value1"}} |
| string_not_equal_ignore_case | String is not equal to (case-insensitive) | qcs:tag          | {"string_not_equal_ignore_case":{"qcs:tag/tag_name1":"tag_value1"}} |
| binary_equal                 | String is equal to (case-sensitive)     | qcs:tag          | {"binary_equal":{"qcs:tag/tag_name1":"tag_value1"}}          |
| date_not_equal               | Time is not equal to                 | qcs:current_time | {"date_not_equal":{"qcs:current_time":"2016-06-01T00:01:00Z"}} |
| date_greater_than            | Time is greater than                   | qcs:current_time | {" date_greater_than ":{"qcs:current_time":"2016-06-01T00:01:00Z"}} |
| date_greater_than_equal      | Time is greater than or equal to               | qcs:current_time | {" date_greater_than_equal ":{"qcs:current_time":"2016-06-01T00:01:00Z"}} |
| date_less_than               | Time is less than                   | qcs:current_time | {" date_less_than ":{"qcs:current_time":"2016-06-01T 00:01:00Z"}} |
| date_less_than_equal         | Time is less than or equal to               | qcs:current_time | {" date_less_than_equal ":{"qcs:current_time":"2016-06-01T 00:01:00Z"}} |
| date_equal                   | Time is equal to                   | qcs:current_time | {"date_equal ":{"qcs:current_time":"2016-06-01T00:01:00Z"}}  |
| ip_equal                     | IP is equal to                    | qcs:ip           | {"ip_equal":{"qcs:ip ":"10.121.2.10/24"}}                    |
| ip_not_equal                 | IP is not equal to                  | qcs:ip           | {"ip_not_equal":{"qcs:ip ":["10.121.2.10/24", "10.121.2.20/24"]}} |
| numeric_not_equal            | Value is not equal to                 | qcs:mfa          | {" numeric_not_equal":{"mfa":1}}                             |
| numeric_greater_than         | Value is greater than                   | -                | {"numeric_greater_than ":{"cvm_system_disk_size":10}}        |
| numeric_greater_than_equal   | Value is greater than or equal to               | -                | {"numeric_greater_than_equal ":{"cvm_system_disk_size":10}}  |
| numeric_less_than            | Value is less than                   | -                | {"numeric_less_than ":{"cvm_system_disk_size":10}}           |
| numeric_less_than_equal      | Value is less than or equal to               | -                | {"numeric_less_than_equal ":{"cvm_system_disk_size":10}}     |
| numeric_equal                | Value is equal to                   | qcs:mfa          | {" numeric_equal":{"mfa":1}}                                 |
| bool_equal                   | Boolean matches                 | -                | -                                                            |
| null_equal                   | Condition key matches empty string             | -                | -                                                            |

Note:

1. Time is displayed in a format that conforms to the ISO8601 standard, and UTC time is required.

2. The IP format must comply with the CIDR standard.

3. A condition operator (excluding `null_equal`) ending in `if_exist` indicates that the condition is met even if the context does not include the corresponding key value.

4. `for_all_value` is a qualifier that needs to be used with the condition operator, which means that a condition is met only if all values of the condition key in the context are satisfied.

5. `for_any_value` is a qualifier that needs to be used with the condition operator, which means that a condition is met as long as any value of the condition key in the context is satisfied.

6. Some services do not support or only partially support conditions. For more information, please see the corresponding product documentation.
