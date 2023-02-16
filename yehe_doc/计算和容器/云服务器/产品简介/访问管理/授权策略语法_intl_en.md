
<span id = "celueyufa"></span>
### Policy Syntax
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
- **version** is required. Currently, only "2.0" is supported.
- **statement** describes the details of one or more permissions. This element contains a permission or permission set consisting of other elements such as effect, action, resource, and condition. One policy has only one statement.
 1. **effect** describes whether the result produced by the statement is "allowed" (allow) or "denied" (deny). This element is required.
 2. **Action** describes the allowed or denied actions. An action can be an API (described using the prefix "name") or a feature set (a set of specific APIs, described using the prefix "permit"). This element is required.
 3. **resource** describes the authorization details. A resource is described in a six-piece format. Detailed resource definitions vary by product. For more information on how to specify a resource, see the documentation for the relevant product. This element is required.
 4. **condition** describes the condition for the policy to take effect. A condition consists of operator, action key, and action value. A condition value may contain information such as time and IP address. Some services allow you to specify additional values in a condition. This element is optional.


<span id = "caozuo"></span>
### CVM Operations

A CAM policy allows you to perform API operations in any Tencent Cloud service that supports CAM. For CVM, use the prefix `name/cvm:` with any API, such as `name/cvm:RunInstances` or `name/cvm:ResetInstancesPassword`.
To specify multiple actions in a single statement, separate them with commas, as shown below:
```
"action":["name/cvm:action1","name/cvm:action2"]
```
You can also specify multiple actions using a wildcard. For example, you can specify all APIs whose names begin with "Describe", as shown below:
```
"action":["name/cvm:Describe*"]
```
To specify all CVM operations, use the wildcard "*" as follows:
```
"action": ["name/cvm:*"]
```

<span id = "ziyuanlujing"></span> 
### CVM Resource Path
Each CAM policy defines its own resources.
The general format of resource paths is as follows:
```
qcs:project_id:service_type:region:account:resource
```
**project_id**: project information, which is only used for compatibility purposes and can be left blank.
**service_type**: abbreviation of a product, such as CVM.
**region**: region of the resource, such as bj.
- **account**: the root account of the resource owner, such as uin/164256472.
**resource**: detailed resource information of each product, such as instance/instance_id1 or instance/*.

For example, you can specify a specific instance (i-15931881scv4) in the statement as follows:
```
"resource":[ "qcs::cvm:bj:uin/164256472:instance/i-15931881scv4"]
```
You can also use the wildcard "*" to specify all instances that belong to a specific account as shown below:
```
"resource":[ "qcs::redis:bj:uin/164256472:instance/*"]
```

If you want to specify all resources or if any API operation does not support resource-level permissions, you can use wildcard "*" in `resource` as shown below:
```
"resource":["*"]
```
To specify multiple resources in one instruction, separate them with commas. In the following example, two resources are specified:
```
"resource":["resource1","resource2"]
```
The following table describes CVM resources and the corresponding resource description methods.
<style>
table th:nth-of-type(1){
width:250px;
}
table th:nth-of-type(2){
width:500px;
}
</style>
In the following table, names with the prefix $ are placeholders.
- $project is the ID of the project.
- $region is the region of the resource.
- $account is the ID of the account.

| Resource | Syntax |
|-------|-------|
| Instance | qcs::cvm:$region:$account:instance/$instanceId |
| Key | qcs::cvm:$region:$account:keypair/$keyId |
| VPC | qcs::vpc:$region:$account:vpc/$vpcId |
| Subnet | qcs::vpc:$region:$account:subnet/$subnetId |
| Image | qcs::cvm:$region:$account:image/\* |
| CBS |  qcs::cvm:$region:$account:volume/$diskid|
| Security group | qcs::cvm:$region:$account:sg/$sgId |
| EIP |  qcs::cvm:$region:$account:eip/*|

 

<span id = "tiaojianmiyue"></span>
### CVM Condition Keys
You can use conditions to specify the conditions under which policies take effect. Each condition consists of one or more key pairs. These are not case-sensitive.

- If you specify multiple conditions or multiple keys in one condition, they are connected with the logical operator "AND".
- If you specify a key with multiple values in one condition, they are connected with the logical operator "OR".
The following table describes CVM condition keys for specific services.
<table class="tableblock frame-all grid-all spread">
<colgroup>
<col style="width: 25%;">
<col style="width: 25%;">
<col style="width: 50%;">
</colgroup>
<thead>
<tr>
<th class="tableblock halign-left valign-top">Condition key</th>
<th class="tableblock halign-left valign-top">Reference type</th>
<th class="tableblock halign-left valign-top">Key pair</th>
</tr>
</thead>
<tbody>
<tr>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:instance_type</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>String</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:instance_type=<code>instance_type</code></p>
</div>
<div class="ulist">
<ul>
<li>
<p><code>instance_type</code> is the model of the CVM instance, such as S1.SMALL1.</p>
</li>
</ul>
</div></div></td>
</tr>
<tr>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:image_type</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>String</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:image_type=<code>image_type</code></p>
</div>
<div class="ulist">
<ul>
<li>
<p><code>image_type</code> is the type of the image, such as IMAGE_PUBLIC.</p>
</li>
</ul>
</div></div></td>
</tr>
<tr>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>vpc:region</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>String</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>vpc:region=<code>region</code></p>
</div>
<div class="ulist">
<ul>
<li>
<p><code>region</code> is the region of the CVM instance, such as ap-guangzhou.</p>
</li>
</ul>
</div></div></td>
</tr>
<tr>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:disk_size</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>Integer</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:disk_size=<code>disk_size</code></p>
</div>
<div class="ulist">
<ul>
<li>
<p><code>disk_size</code> is the size of the disk, such as 500</p>
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
<p><code>disk_type</code> is the type of the disk, such as CLOUD_BASIC.</p>
</li>
</ul>
</div></div></td>
</tr>
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
<p><code>region</code> is the region of the CVM instance, such as ap-guangzhou.</p>
</li>
</ul>
</div></div></td>
</tr>
</tbody>
</table>
