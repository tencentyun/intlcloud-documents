The syntax structure of a policy is as shown in the following figure. The policy consists of a `version` and a `statement`, and can also contain `principal` information. `principal` can only be used in policy syntax-related parameters in policy management APIs.
A `statement` is composed of several sub-statements. Each sub-statement contains four elements: `action`, `resource`, `condition`, and `effect`, where `condition` is optional.
![](https://mc.qcloudimg.com/static/img/06d3b1a6be4d9798286256ce2ecebbed/poly.png)

### JSON Format

The policy syntax is based on the JSON format as defined in RFC 7159. If a created or updated policy does not meet the JSON format requirement, it cannot be successfully submitted. Therefore, you must ensure that the JSON format is correct. You can check the policy format with an online JSON validator.   

### Syntax Conventions  

Here we list some syntax conventions:

- These characters are JSON characters included in policy syntax:

```
 { } [ ] " , :
```

- These characters are special characters used to describe policy syntax and are not included in policies: 

```
 = < > ( ) |
```

- If an element allows multiple values, the values will be described with comma separators and ellipsis; for example:

```
 [<resource_string>, < resource_string>, ...]  
 <principal_map> = { <principal_map_entry>, <principal_map_entry>, ... }
```

When multiple values are allowed, you can also choose to include only one value. When an element has only one value, the trailing comma must be removed, and the brackets "[]" are optional; for example:

```
 "resource": [<resource_string>]     
 "resource": <resource_string>
```

- The question mark "?" behind an element indicates that the element is optional; for example:

 ```   
 <condition_block?>
 ```

- If an element is enumerated, use vertical line "|" to separate the values and use parenthesis "()" to define the range of the enumerated values; for example:

```      
("allow" | "deny")
```

- String elements are enclosed in double quotation marks; for example:     

```
<version_block> = "version" : "2.0"
```

### Syntax Description

```
policy  = {
     <version_block>
     <principal_block?>,
     <statement_block>
}

<version_block> = "version" : "2.0"

<statement_block> = "statement" : [ <statement>, <statement>, ... ]

<statement> = {     
    <effect_block>,
    <action_block>,
    <resource_block>,
    <condition_block?>
}

<effect_block> = "effect" : ("allow" | "deny")  

<principal_block> = "principal": ("*" | <principal_map>)

<principal_map> = { <principal_map_entry>, <principal_map_entry>, ... }

<principal_map_entry> = "qcs":   
    [<principal_id_string>, <principal_id_string>, ...]

<action_block> = "action": 
    ("*" | [<action_string>, <action_string>, ...])

<resource_block> = "resource": 
    ("*" | [<resource_string>, <resource_string>, ...])

<condition_block> = "condition" : { <condition_map> }
<condition_map> { 
  <condition_type_string> : { <condition_key_string> : <condition_value_list> },
  <condition_type_string> : { <condition_key_string> : <condition_value_list> }, ...
}  
<condition_value_list> = [<condition_value>, <condition_value>, ...]
<condition_value> = ("string" | "number")
```

**Syntax description:**

- One policy may contain multiple `statement`.
  The maximum length of a policy is 6144 characters (without spaces). For more information, please see [Limits](/doc/product/598/10609).
  The display order of blocks is unrestricted; for example, in a policy, `version_block` can follow `effect_block`.

- Currently supported syntax version is 2.0.

- The `principal_block` element cannot be used in the console and can only be used through policy management APIs and policy syntax-related parameters.

- Lists are supported for both `action` and `resource`.

- A condition can be a single condition or a logical combination of multiple sub-conditions. Each condition contains a condition operator `condition_type`, a condition key `condition_key`, and a condition value `condition_value`.

- The `effect` of each statement is `deny` or `allow`. If the statement of a policy contains both `allow` and `deny`, `deny` will take precedence.

### String Description

The element strings described in the syntax are as detailed below:

#### action_string

It consists of description scope, service type, and operation name.   

```
// All operations for all products
"action":"*"
"action":"*:*"
// All operations in COS
"action":"cos:*"
// Operation named `GetBucketPolicy` in COS
"action":"cos:GetBucketPolicy"
// Operation for matching some buckets in COS
"action":"cos:*Bucket*"
// Operation list named `GetBucketPolicy\PutBucketPolicy\DeleteBucketPolicy` in COS
"action":["cos:GetBucketPolicy","cos:PutBucketPolicy","cos: DeleteBucketPolicy"]
    
```

#### resource_string    

Resource is described in a six-segment format.

```
qcs: project :serviceType:region:account:resource
```

Below are examples:

```
// COS object. Region: Shanghai. Resource owner uid: 10001234. Resource name: bucket1/object2.
qcs::cos:sh:uid/10001234:prefix//10001234/bucket1/object2
// CMQ queue. Region: Shanghai. Resource owner uin: 12345678. Resource name: 12345678/queueName1. Resource prefix: queueName
qcs::cmqqueue:sh:uin/12345678:queueName/12345678/queueName1
// CVM instance. Region: Shanghai. Resource owner uin: 12345678. Resource name: ins-abcdefg. Resource prefix: instance
qcs::cvm:sh:uin/12345678:instance/ins-abcdefg
```

For more information on product-specific resource definitions, please see the corresponding product documentation in [CAM-Enabled Tencent Cloud Products](https://intl.cloud.tencent.com/document/product/598/10588).

#### condition_type_string

Condition operator describes the type of test conditions, such as `string_equal`, `string_not_equal`, `date_equal`, `date_not_equal`, `ip_equal`, `ip_not_equal`, `numeric_equal`, and `numeric_not_equal`. Below are examples:

```
"condition":{
         "string_equal":{"cvm:region":["sh","gz"]},
         "ip_equal":{"qcs:ip":"10.131.12.12/24"}
}
```

#### condition_key_string

Condition keys are used with a condition operator to determine whether the condition is met. CAM defines a set of condition keys that can be used in all products, including `qcs:current_time`, `qcs:ip`, `qcs:uin`, `qcs:owner_uin`, etc. For more information, please see [Condition](/doc/product/598/10608).
    

#### principal_id_string    

For CAM, users are also its resources. Therefore, the `principal` also uses a six-segment description. Below is an example. For more information, please see [Resource Description Method](/doc/product/598/10606).

```
"principal":   {"qcs":["qcs::cam::uin/1238423:uin/3232",
             "qcs::cam::uin/1238423:groupid/13"]}
```

