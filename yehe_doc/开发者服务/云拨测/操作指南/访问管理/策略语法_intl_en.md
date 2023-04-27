## Overview

An access policy that employs the JSON-based access policy language is used to grant access to CAT resources. You can authorize a specified principal to perform actions on a specified CAT resource through the access policy language.

The access policy syntax describes the basic elements and usage of the policy. For the description of the policy syntax, see [Concepts](https://intl.cloud.tencent.com/document/product/598/10600).

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
  1. **effect** describes whether the statement result is `allow` or `deny`. This element is required.
  2. **action** specifies whether to allow or deny the operation. The operation can be an API (prefixed with `name`) or a feature set (a group of APIs, prefixed with `permid`). This element is required.
  3. **resource** describes the details of an authorization. A resource is described in a six-part format. Detailed resource definitions vary by product. For more information on how to specify a resource, see the corresponding documentation for the product for which you want to write a resource statement. This element is required.
  4. **condition** describes the condition for the policy to take effect. A condition consists of an operator, an action key, and an action value. A condition value may contain information such as time and IP address. Some services allow you to specify additional values in a condition. This element is optional.



### Specifying an effect
If you don't explicitly grant access to (`allow`) a resource, access is implicitly denied. You can also explicitly `deny` access to a resource to ensure that a user cannot access it, even if another policy has granted access to it. The following example specifies an `allow` effect.
```json
"effect" : "allow"
```

### Specifying an action
CAT defines console operations that can be specified in a policy. The specified operations are divided into reading part of APIs (`cat:Describe\*`) and all APIs (`cat:\*`) according to the operation nature.
The following example specifies an action that is allowed:
```
"action":[
  "name/cat:Describe*"
]
```

### Specifying a resource

The `resource` element describes one or multiple operation objects, such as CAT resource. All the resources can be described with the following four-segment format.

```plaintext
qcs:project_id:account:resource
```

The parameters are described as follows:

| Parameter | Description | Required |
| ------------ | ------------------------------------------------------------ | -------- |
| qcs          |  Abbreviation for "qcloud service", which indicates a Tencent Cloud service.               | Yes       |
| service_type | Product name abbreviation, which is `cat` here.                                         | Yes       |
| account      | Root account information of the resource owner, which is the root account ID in the format of `uin/${OwnerUin}`, such as `uin/100000000001`. | Yes       |
| resource     | Resource details prefixed with `task`, such as `task-a4iiv123`.            | Yes       |

Below is a sample four-segment description of a CAT resource:
```plaintext
"resource":["qcs::cat:uin/1250000000:TaskId/task-a4iiv123"]
```

## Examples
Grant the read and write permissions of specified resources based on resource ID. The root account ID is `1250000000`:

Sample: Granting the sub-user the permission to modify a test task (ID: `task-12345678`).
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action":[
                "cat:ModifyProbeTask"
            ],
            "resource": [
                "qcs::cat:uin/1250000000:TaskId/task-a4iiv123"
            ]
        }
    ]
}
```


### List of APIs supporting resource-level authorization

| API      | Description |
| -------------------------------- | ------------------------------------------------------ |
| CreateProbeTasks                 | Creates test tasks in batch.                                       |
| DeleteProbeTask                  | Deletes a test task.                                           |
| DescribeConsoleConfig            | Gets the console configuration, for example, whether the tag is required when the current user is creating a task. |
| DescribeDetailedSingleProbeData  | Queries the details of a test task based on time range, task ID, ISP, etc. |
| DescribePaymentState             | Queries the billing status.                                           |
| DescribeProbeMetricData          | Lists the detailed data of a CAT metric.                                 |
| DescribeProbeMetricTagValues     | Lists the tag values of a CAT metric.                                   |
| DescribeProbeNodeGroups          | Queries node groups.                                             |
| DescribeProbeNodes               | Queries testing nodes.                                           |
| DescribeProbeTasks               | Queries the list of test tasks.                                       |
| DescribeProbeTasksByAddresses    | Lists the tasks aggregated by address.                                 |
| ModifyProbeTask                  | Modifies a test task.                                           |
| ResumeProbeTask                  | Resumes a test task.                                           |
| SuspendProbeTask                 | Suspends a test task.                                           |
| UpdateProbeTaskAttributes        | Updates the attributes of a test task.                                       |
| UpdateProbeTaskConfigurationList | Updates the configuration of test tasks in batch.                                   |

