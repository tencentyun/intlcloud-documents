
<span id = "celueyufa"></span>
## Policy Syntax
CAM policy:
```json
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
- **version**: Required. It must be `"2.0"`.
- **statement**: Detailed information of one or more permissions. Each permission is composed of a set of elements including effect, action, resource, and condition. A policy has only one statement element.
 1. **action**: Required. It describes the operations to be allowed or denied, which can be APIs (described with the "name" prefix) or a feature set (a set of specific APIs described with the "permid" prefix).
 2. **resource**: Required. It describes the specific data to be authorized in a six-segment format. Detailed resource definitions vary by product.
 3. **condition**: Optional. It describes the conditions for the policy to take effect. A condition consists of an operator, operation key, and operation value. A condition value may contain information such as a time and IP address. Some services allow you to specify other information in conditions.
 4. **effect**: Required. It describes the result returned by the statement, that is, whether the permission is allowed ("allow") or denied ("deny").


## CBS Operations[](id:caozuo)

In a CAM policy statement, you can specify any API operation from any service that supports CAM. For CBS, use the APIs prefixed with `name/cvm:`, for example, `name/cvm:CreateDisks` or `name/cvm:DescribeDisks`.
To specify multiple operations in a single statement, separate them with commas, as shown below.
```
"action":["name/cvm:action1","name/cvm:action2"]
```
You can also use a wildcard to specify multiple operations. For example, you can specify all operations whose names begin with "Describe", as shown below.
```
"action":["name/cvm:Describe*"]
```
To specify all operations in CVM, use the wildcard `*` as follows.
```
"action":["name/cvm:*"]
```


## CBS Resource Paths[](id:ziyuanlujing)
Every CAM policy statement contains the resources applicable to the policy itself. The general format of a resource path is shown below.
```
qcs:project_id:service_type:region:account:resource
```
- **project_id**: (Optional) Project information, which is only used to enable compatibility with earlier CAM logics. 
- **service_type**: Short name of a Tencent Cloud product, for example, "CVM".
- **region**: Region information, for example, "bj".
- **account**: Root account of a resource owner, for example, "uin/164256472".
- **resource**: Specific resources of a product, for example, "volume/diskid1" or "volume/*".

You can specify a CBS resource in the statement, for example, "disk-abcdefg", as shown below.
```
"resource":[ "qcs::cvm:bj:uin/164256472:volume/disk-abcdefg"]
```
You can also use the wildcard `*` to specify all CBS resources under an account, as shown below.
```
"resource":[ "qcs::cvm:bj:uin/164256472:volume/*"]
```

To specify all resources, or if an API operation does not support resource-level permission control, you can use the wildcard `*` in the resource element, as shown below.
```
"resource": ["*"]
```
To specify multiple resources in one statement, separate them with commas. In the following example, two resources are specified.
```
"resource":["resource1","resource2"]
```


## CBS Condition Keys(id:tiaojianmiyue)

In a policy statement, you can choose to specify the conditions for the policy to take effect. Each condition contains one or more key-value pairs. Condition keys are case-insensitive.

- If you specify multiple conditions or keys in one condition, the condition is evaluated with the "AND" logical operator.
- If you specify a key with multiple values in one condition, the condition is evaluated with the "OR" logical operator. The permission can be granted only after all conditions are met.
The following table describes the CBS condition keys that are used for specific services.
<table class="tableblock frame-all grid-all spread">
<colgroup>
<col style="width: 15%;">
<col style="width: 15%;">
<col style="width: 70%;">
</colgroup>
<thead>
<tr>
<th class="tableblock halign-left valign-top">Condition Key</th>
<th class="tableblock halign-left valign-top">Reference Type</th>
<th class="tableblock halign-left valign-top">Key-Value Pair</th>
</tr>
</thead>
<tbody>
<tr>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:region</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>String</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:region=<code>region</code></p>
</div>
<div class="ulist">
<ul>
<li>
where <code>region</code> indicates a region (for example, "ap-guangzhou").</p>
</li>
</ul>
</div></div></td>
</tr>
<tr>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:disk_type</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>String</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm_disk_type=<code>disk_type</code></p>
</div>
<div class="ulist">
<ul>
<li>
<p>where <code>disk_type</code> indicates a disk type (for example, "CLOUD_PREMIUM").</p>
</li>
</ul>
</div></div></td>
</tr>
</tbody>
</table>
