>!Since the product logic no longer meets the technical development of game industry, Game Player Matching GPM will be deprecated on June 1st, 2022. Please complete service migration before May 31 , 2022.

<span id = "celueyufa"></span>

### Policy syntax

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
- **version** is required. Currently, only the value "2.0" is allowed.
- **statement** describes the details of one or more permissions, and therefore contains the permission(s) of other elements such as `action`, `resource`, `condition`, and `effect`. One policy has only one `statement`.
  - **effect** is required. It describes the result of a statement. The result can be "allow" or an explicit "deny".
  - **action** is required. It describes the allowed or denied operation. An operation can be an API (prefixed with “name”) or a feature set (a set of specific APIs prefixed with "permid").
  - **resource** is required. It describes the details of authorization. A resource is described in a six-segment format. Detailed resource definitions vary by product. For more information on how to specify a resource, see the documentation for the product whose resources you are writing a statement for.
  - **condition** is required. It describes the condition for the policy to take effect. A condition consists of operator, action key, and action value. A condition value may contain information such as time and IP address. Some services allow you to specify additional values in a condition.


<span id = "caozuo"></span>

### GPM operations

You can use CAM policy statements to authorize any API operations for any services that support CAM. To authorize GPM operations, please specify the APIs prefixed with "gpm:" such as `gpm:DescribeMatch` or `gpm:DescribeRule`.
To specify multiple operations in a single statement, separate them with commas as shown below:
```
"action":["gpm:action1","gpm:action2"]
```
You can also specify multiple operations using a wildcard. For example, you can specify all operations whose names begin with "Describe" as shown below:
```
"action":["gpm:Describe*"]
```
To specify all GPM operations, use only the wildcard `*` as follows:
```
"action":["gpm:*"]
```

<span id = "ziyuanlujing"></span> 

### GPM resource path

Each CAM policy statement has its own applicable resources.
The general form of a resource path is as follows:
```
qcs:project_id:service_type:region:account:resource
```
- **project_id**: describes the project information and is only used to enable compatibility with legacy CAM logic. It can be left empty.
- **service_type**: describes the product’s abbreviation, such as `gpm`.
- **region**: region information, for example `ap-shanghai`.
- **account**: the root account of the resource owner, for example, `uin/164256472`.
- **resource**: describes detailed resource information of each product, such as `rule/RuleCode1` or `match/*`.

For example, you can specify a rule (rule-rzj1xxx) to specify the resource path in the statement as shown below:
```
"resource":[ "qcs::gpm:ap-shanghai:uin/16425xxxx:rule/rule-rzj1xxx"]
```
You can also use the wildcard (*) to specify all rules that belong to a specific account as shown below:
```
"resource":[ "qcs::gpm:ap-shanghai:uin/16425xxxx:rule/*"]
```
If you want to specify all resources or if a specific API operation does not support resource-level permission control, you can use the wildcard (*) in the `resource` element as shown below:
```
"resource": ["*"]
```
To specify multiple resources in one policy, separate them with a comma. In the following example, two resources are specified:
```
"resource":["resource1","resource2"]
```
The table below describes the resources that can be used by GPM and the corresponding resource description methods. In the following table, the words prefixed with $ are all alternative names.
<table>
<thead>
<tr>
<th>Resource</th>
<th>Resource Description Method in Authorization Policy</th>
</tr>
</thead>
<tbody><tr>
<td>Matchmaking</td>
<td><code>qcs::gpm:$region:$account:rule/$RuleCode</code></td>
</tr>
<tr>
<td>Rule</td>
<td><code>qcs::gpm:$region:$account:match/$MatchCode</code></td>
</tr>
</tbody></table>

- “project” refers to project ID.
- “region” refers to region.
- “account” refers to account ID.

