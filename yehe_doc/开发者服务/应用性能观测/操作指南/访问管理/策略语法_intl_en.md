## Overview

An access policy that employs the JSON-based access policy language is used to grant access to APM resources. You can authorize a specified principal to perform actions on a specified CM resource through the access policy language.

The access policy syntax describes the basic elements and usage of the policy. For the description of the policy syntax, see [Concepts](https://www.tencentcloud.com/document/product/598/10600).

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

#### Element usage
- **version** is required. Currently, only the value "2.0" is allowed.
- **statement** describes the details of one or more permissions. This element contains a permission or permission set of other elements such as `effect`, `action`, `resource`, and `condition`. One policy has only one statement.
 1. **effect** is required. It describes whether the declaration result is `allow` or explicit `deny`.
 2. **action** is required. It specifies whether to allow or deny the operation. The operation can be an API (prefixed with `name`) or a feature set (a group of APIs, prefixed with `permid`).
 3. **resource** is required. It describes the details of authorization. A resource is described in a six-segment format. Detailed resource definitions vary by product. For more information on how to specify resources, see the product documentation corresponding to the resource statement you are writing.
 4. **condition** is optional. It describes the condition for the policy to take effect. A condition consists of operator, action key, and action value. A condition value may contain information such as time and IP address. Some services allow you to specify additional values in a condition.



### Specifying an effect

If you don't explicitly grant access to (`allow`) a resource, access is implicitly denied. You can also explicitly `deny` access to a resource to ensure that a user cannot access it, even if another policy has granted access to it. The following example specifies an `allow` effect.

```json
"effect" : "allow"
```

### Specifying an action

APM defines console operations that can be specified in a policy. The specified operations are divided into reading part of APIs (`apm:Describe\*`) and all APIs (`apm:\*`) based on the operation nature.

Below is an example of specifying the allowed operations:

```
"action": [
  "name/apm:Describe*"
]
```

### Specifying a resource

The `resource` element describes one or multiple operation objects, such as APM resources. All the resources can be described in the following 6-segment format.

```plaintext
qcs:project_id:service_type:region:account:resource
```

The parameters are as described below:

| Parameter | Description | Required |
| ------------ | ------------------------------------------------------------ | -------- |
| qcs | Abbreviation for "qcloud service", which indicates a Tencent Cloud service | Yes |
| project_id | Project information, which is only used to enable compatibility with legacy CAM logic and generally can be left empty | No |
| service_type | Product name abbreviation, which is `apm` here | Yes |
| region | Region information | Yes |
| account | Root account information of the resource owner, which is the root account ID in the format of `uin/${OwnerUin}`, such as `uin/100000000001` | Yes |
| resource | Resource details prefixed with `instance` | Yes |

Below is a sample six-segment description of an APM resource:

```plaintext
"resource":["qcs::apm:ap-guangzhou:uin/1250000000:apm/apm-btzsrI123"]
```

## Samples
Grant the read and write permissions of specified resources based on resource ID. The root account ID is `1250000000`:

Sample: Granting the sub-user the permission to modify the business system (ID: apm-btzsrI123)

```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "apm:ModifyApmInstance"
            ],
            "resource": [
                "qcs::apm:ap-guangzhou:uin/1250000000:apm-instance/apm-btzsrI123"
            ]
        }
    ]
}
```


### List of APIs supporting resource-level authorization

| API | Description |
| --------------------------- | ------------------ |
| DescribeApmAgent            | Gets the APM agent     |
| DescribeApmInstances        | Queries APM business systems   |
| DescribeApmRegions          | Gets APM regions      |
| DescribeGeneralSpanList     | Queries spans  |
| DescribeInstanceBriefs      | Queries the business system overview           |
| DescribeMetricLineData      | Pulls metric curve data   |
| DescribeMetricRecords       | Queries the list of metrics       |
| DescribePAASGeneralSpanList | Queries spans |
| DescribePAASMetricLineData  | Queries the metric curve data   |
| DescribePAASMetricPointData | Queries the metric point data     |
| DescribePAASTagValues       | Queries the dimension information       |
| DescribePAASTopology        | Queries the topology data       |
| DescribeServiceNodes        | Gets the list of services       |
| DescribeServiceOverview     | Gets the APM system overview    |
| CreateApmInstance    | Creates an APM business system      |
| CreatePAASInstance   | Creates a PaaS APM business system |
| DeletePAASInstance   | Deletes an APM business system     |
| ModifyApmInstance    | Modifies an APM business system       |
| TerminateApmInstance | Terminates an APM business system        |
