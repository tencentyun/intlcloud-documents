
## Policy Syntax
For more information on how to create custom policies, please see [Creating Custom Policies](https://intl.cloud.tencent.com/document/product/598/35596). SCF's policy syntax follows CAM's [syntax structure](https://intl.cloud.tencent.com/document/product/598/10604) and [resource description method](https://intl.cloud.tencent.com/document/product/598/10606), which is based on the JSON format, and all resources can be described in the six-segment style, as shown in the sample below:

```
qcs::scf:region:uin/uin—id:namespace/namespace-name/function/function-name
```

>! When configuring the policy syntax, you also need to use the monitor APIs to get the monitoring information under the account. For more information about using the monitor APIs, please see the [sample policy](#policygen).

<span id="policygen"></span>
## Sample Policy
```
{	 
        "version":"2.0", 
        "statement": 
        [ 
           { 
              "effect":"allow", 
              "action":
              [
                "scf:ListFunctions",
                "scf:GetAccountSettings",
                "monitor:*"
              ], 
              "resource":["*"]  
           }, 
          { 
             "effect": "allow",
             "action": 
             [
                "scf:DeleteFunction",
                "scf:CreateFunction",
                "scf:InvokeFunction",
                "scf:UpdateFunction",
                "scf:GetFunctionLogs",
                "scf:SetTrigger",
                "scf:DeleteTrigger",
                "scf:GetFunction",
                "scf:ListVersion"
            ],
            "resource": 
            [
                "qcs::scf:gz:uin/******:namespace/default/function/Test1",
                "qcs::scf:gz:uin/******:namespace/default/function/Test2"
            ]
         }
      ] 
} 
```
- If the `action` is an operation that needs to be associated with a resource, the resource can be defined as `*`, indicating that all resources are to be associated.
- If the `action` is an operation that does not need to be associated with a resource, the resource needs to be defined as `*`.
- This sample allows the sub-account to have the operation permissions of certain functions under the root account. The resource in `resource` is described as a function under the root account.

## Specifying Conditions
The access policy language allows you to specify conditions when granting permissions, such as limiting the user access source or authorization time. The list below contains supported condition operators as well as general condition keys and examples.

<table>
<thead>
<tr>
<th style="width:20%">Condition Operator</th>
<th style="width:15%">Description</th>
<th style="width:15%">Condition Name</th>
<th style="width:50%">Example</th>
</tr>
</thead>
<tbody><tr>
<td>ip_equal</td>
<td>The IP is equal to</td>
<td>qcs:ip</td>
<td><code>{"ip_equal":{"qcs:ip ":"10.121.2.0/24"}}</code></td>
</tr>
<tr>
<td>ip_not_equal</td>
<td>The IP is not equal to</td>
<td>qcs:ip</td>
<td><code>{"ip_not_equal":{"qcs:ip ":["10.121.1.0/24", "10.121.2.0/24"]}}</code></td>
</tr>
<tr>
<td>date_not_equal</td>
<td>The date is not equal to</td>
<td>qcs:current_time</td>
<td><code>{"date_not_equal":{"qcs:current_time":"2016-06-01T00:01:00Z"}}</code></td>
</tr>
<tr>
<td>date_greater_than</td>
<td>The date is later than</td>
<td>qcs:current_time</td>
<td><code>{"date_greater_than":{"qcs:current_time":"2016-06-01T00:01:00Z"}}</code></td>
</tr>
<tr>
<td>date_greater_than_equal</td>
<td>The date is later than or equal to</td>
<td>qcs:current_time</td>
<td><code>{"date_greater_than_equal":{"qcs:current_time":"2016-06-01T00:01:00Z"}}</code></td>
</tr>
<tr>
<td>date_less_than</td>
<td>The date is earlier than</td>
<td>qcs:current_time</td>
<td><code>{"date_less_than":{"qcs:current_time":"2016-06-01T 00:01:00Z"}}</code></td>
</tr>
<tr>
<td>date_less_than_equal</td>
<td>The date is earlier than or equal to</td>
<td>qcs:current_time</td>
<td><code>{"date_less_than":{"qcs:current_time":"2016-06-01T 00:01:00Z"}}</code></td>
</tr>
<tr>
<td>date_less_than_equal</td>
<td>The date is earlier than or equal to</td>
<td>qcs:current_time</td>
<td><code>{"date_less_than_equal":{"qcs:current_time":"2016-06-01T00:01:00Z"}}</code></td>
</tr>
</tbody></table>

- To allow access only by IPs in the `10.121.2.0/24` IP range, use the following syntax:
```json
"ip_equal":{"qcs:ip ":"10.121.2.0/24"}
```
- To allow access only by IPs `101.226.\*\*\*.185` and `101.226.\*\*\*.186`, use the following syntax:
```json
"ip_equal": {
    "qcs:ip": [
      "101.226.***.185",
      "101.226.***.186"
    ]
}
```

## User Policy Update<spoan id="Strategy"></span>
SCF improved the preset permission policies in April 2020. The preset policies `QcloudSCFFullAccess` and `QcloudSCFReadOnlyAccess` were modified, and the `QcloudAccessForScfRole` policy was added for the configuration role `SCF_QcsRole`, as shown below:
- Currently, the preset policy `QcloudSCFFullAccess` has the following permissions:

``` json
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "scf:*",
                "tag:*",
                "cam:DescribeRoleList",
                "cam:GetRole",
                "cam:ListAttachedRolePolicies",
                "apigw:DescribeServicesStatus",
                "apigw:DescribeService",
                "apigw:DescribeApisStatus",
                "cmqtopic:ListTopicDetail",
                "cmqqueue:ListQueueDetail",
                "cmqtopic:GetSubscriptionAttributes",
                "cmqtopic:GetTopicAttributes",
                "cos:GetService",
                "cos:HeadBucket",
                "cos:HeadObject",
                "vpc:DescribeVpcEx",
                "vpc:DescribeSubnetEx",
                "cls:getTopic",
                "cls:getLogset",
                "cls:listLogset",
                "cls:listTopic",
                "ckafka:List*",
                "ckafka:Describe*",
                "ckafka:ListInstance",
                "monitor:GetMonitorData",
                "monitor:DescribeBasicAlarmList",
                "monitor:DescribeBaseMetrics",
                "monitor:DescribeSortObjectList",
                "monitor:DescribePolicyConditionList",
                "cdb:DescribeDBInstances"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```
- Currently, the preset policy `QcloudSCFReadOnlyAccess` has the following permissions:

``` json
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "scf:Get*",
                "scf:List*",
                "ckafka:List*",
                "ckafka:Describe*",
                "monitor:GetMonitorData",
                "monitor:DescribeBasicAlarmList",
                "monitor:DescribeBaseMetrics",
                "monitor:DescribeSortObjectList",
                "cam:GetRole",
                "cam:ListAttachedRolePolicies",
                "vpc:DescribeVpcEx",
                "vpc:DescribeSubnetEx",
                "cls:getLogset",
                "cls:getTopic",
                "cls:listTopic",
                "apigw:DescribeService",
                "cmqtopic:GetTopicAttributes",
                "cmqtopic:GetSubscriptionAttributes",
                "cos:HeadBucket",
                "cos:GetService",
                "cos:GetObject"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```
- Currently, the preset policy `QcloudAccessForScfRole` has the following permissions:

``` json
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cos:GetBucket*",
                "cos:HeadBucket",
                "cos:PutBucket*",
                "apigw:*",
                "cls:*",
                "cos:List*",
                "cos:Get*",
                "cos:Head*",
                "cos:OptionsObject",
                "cmqqueue:*",
                "cmqtopic:*",
                "ckafka:List*",
                "ckafka:Describe*",
                "ckafka:AddRoute",
                "ckafka:CreateRoute"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```
The preset policy `QcloudAccessForScfRole` can:
 - Write trigger configuration information to the bucket configuration if a COS trigger is configured. 
 - Read the trigger configuration information from the COS bucket. 
 - Read the code zip package from the bucket when the code is updated through COS. 
 - Create API Gateway services and APIs and publish services if an API Gateway trigger is configured. 
 - Create consumers if a CKafka trigger is configured. 
