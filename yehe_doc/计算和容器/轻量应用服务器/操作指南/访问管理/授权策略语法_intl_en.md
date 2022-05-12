### Policy syntax
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

<table>
<tr>
<th width="25%">Element</th><th>Description</th>
</tr>
<tr>
<td>version</td><td>It is required. Currently, only the value "2.0" is allowed.</td>
</tr>
<tr>
<td>statement</td><td>It describes the details of one or more permissions. It contains a permission or permission set of multiple other elements such as `effect`, `action`, `resource`, and `condition`. One policy has only one `statement`.</td>
</tr>
<tr>
<td>effect</td><td>It is required and describes whether the statement result is an "allow" or an explicit "deny".</td>
</tr>
<tr>
<td>action</td><td>It is required and describes the allowed or denied action (operation). An operation can be an API (prefixed with "name") or a feature set (a set of specific APIs prefixed with "permid").</td>
</tr>
<tr>
<td>resource</td><td>It is required and describes the details of authorization. A resource is described in a six-segment format. Detailed resource definitions vary by product. For more information on how to specify a resource, see the product documentation corresponding to the resource statement you are writing.</td>
</tr>
<tr>
<td>condition</td><td>It is optional and describes the condition for the policy to take effect. A condition consists of an operator, action key, and action value. A condition value may contain information such as time and IP address. Some services allow you to specify additional values in a condition.</td>
</tr>
</table>


### Sample CAM Policy for Lighthouse
The following policy grants the permission to view the list of Lighthouse instances and prohibits the user `xxxxxx` from viewing the details of the instance `lhins-e31oxxxx`. 
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "lighthouse:DescribeInstances"
            ],
            "resource": [
                "*"
            ]
        },
        {
            "effect": "deny",
            "action": [
                "lighthouse:DescribeInstances"
            ],
            "resource": [
                "qcs::lighthouse::uin/xxxxxx:instance/lhins-e31oxxxx"
            ]
        }
    ]
}
```

### Lighthouse Resource Path
Each Lighthouse policy statement has its own applicable resources generally in the following format:
```
qcs:project_id:service_type:region:account:resource
```
**project_id**: Describes the project information, which is only used to enable compatibility with legacy CAM logic and can be left empty.
**service_type**: Describes the product abbreviation such as `lighthouse`.
**region**: Describes the region information, such as `ap-guangzhou`.
**account**: Describes the root account of the resource owner, such as `uin/xxxxxx`.
**resource**: Detailed resource information of each product, for example, instance/instance_id1 or instance/*.

