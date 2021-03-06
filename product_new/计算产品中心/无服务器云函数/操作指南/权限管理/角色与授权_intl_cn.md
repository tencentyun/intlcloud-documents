## 操作场景
[角色（Role）](https://cloud.tencent.com/document/product/598/19420) 是腾讯云 [访问管理（Cloud Access Management，CAM）](https://cloud.tencent.com/document/product/598/10583)提供的拥有一组权限的虚拟身份，主要用于对角色载体授予腾讯云中服务、操作和资源的访问权限，这些权限附加到角色后，通过将角色赋予腾讯云的服务，允许服务代替用户完成对授权资源的操作。

您在创建云函数（SCF）时，可能会需要操作部分其他产品的权限，例如 COS 触发器创建和删除所需的 COS 权限、API 网关触发器创建和删除所需的 API 网关权限、COS 代码文件的 zip 包读取权限等。

## 角色详情

- 角色名：`SCF_QcsRole` 
- 角色载体：`产品服务-scf.qcloud.com`
- 角色描述：SCF 默认配置角色。该服务角色用于提供 SCF 配置对接其他云上资源的权限，包括但不限于代码文件访问、触发器配置。配置角色的预设策略可支持函数执行的基本操作。
- 角色所拥有策略：此角色所拥有 `QcloudAccessForScfRole` 策略，具备以下功能：
 - 配置 COS 对象存储触发器时向 Bucket 配置中写入触发配置信息。 
 - 读取 COS 对象存储 Bucket 中的触发器配置信息。 
 - 在使用 COS 对象存储更新代码时，从 Bucket 完成代码 zip 包的读取操作。 
 - 配置 API 网关触发器时，完成 API 网关的服务、API 创建，以及服务发布等操作。 

>用户可前往 [CAM 控制台](https://console.cloud.tencent.com/cam/overview) 查看并修改当前配置角色 `SCF_QcsRole` 所关联的策略，但修改角色的关联策略可能会造成 SCF 无法正常执行等问题，故不建议修改。
>


## 操作步骤
`SCF_QcsRole` 角色用于授予 SCF 在配置过程中读取和操作用户资源的权限。如果您在管理函数（如使用命令行工具或 VS Code 插件更新函数代码）时，收到相应无角色或无权限报错，则需要配置 `SCF_QcsRole` 角色。
>如果您当前是子用户/协作者，则需要主账号按照以下步骤进行授权。授权完成后，主账号和子用户登录均可以使用云函数服务。
>
1. 如果您是首次使用 SCF，打开 [SCF 控制台](<https://console.cloud.tencent.com/scf/index?rid=1>) 时会提示您进行服务授权。
2. 选择【前往访问管理】进入“角色管理”页面，单击【同意授权】确认授权。
3. 确认授权后，将会为您自动创建角色 `SCF_QcsRole`。

## 附录
<spoan id="Strategy"></span>
### 用户策略更新说明
SCF 于2019年12月完善了预设策略权限，针对预设策略 `QcloudSCFFullAccess` 和 `QcloudSCFReadOnlyAccess` 完成修改，针对配置角色 `SCF_QcsRole` 添加了 `QcloudAccessForScfRole` 策略。详情如下：
- 在预设策略 QcloudSCFFullAccess 中添加了以下权限：
<table>
	<tr>
	<th>权限</th><th>描述</th>
	</tr>
	<tr>
	<td><code>cls:getLogset</code></td><td>用于获取日志信息</td>
	</tr>
	<tr>
	<td><code>cls:getTopic</code></td><td>用于获取日志信息</td>
	</tr>
	<tr>
	<td><code>monitor:DescribeSortObjectList</code></td><td>用于获取函数监控信息</td>
	</tr>
</table>
- 预设策略 QcloudSCFFullAccess 当前权限如下：
``` json
{
   "version":"2.0",
   "statement":[
      {
         "action":[
            "scf:*",
            "tag:*",
            "cam:DescribeRoleList",
            "cam:GetRole",
            "cam:ListAttachedRolePolicies",
            "apigw:DescribeServicesStatus",
            "apigw:DescribeDomain",
            "cos:GetService",
            "cos:HeadObject",
            "cmqtopic:ListTopicDetail",
            "cmqqueue:ListQueueDetail",
            "ckafka:ListInstance",
            "vpc:DescribeVpcEx",
            "vpc:DescribeSubnetEx",
            "cls:listLogset",
            "cls:listTopic",
            "cls:getLogset",
            "cls:getTopic",
            "monitor:GetMonitorData",
            "monitor:DescribeBasicAlarmList",
            "monitor:DescribeSortObjectList"
         ],
         "resource":"*",
         "effect":"allow"
      }
   ]
}
```
- 在预设策略 QcloudSCFReadOnlyAccess 中添加了以下权限：
<table>
	<tr>
	<th>权限</th><th>描述</th>
	</tr>
	<tr>
	<td><code>monitor:GetMonitorData</code></td><td>用于获取函数监控信息</td>
	</tr>
	<tr>
	<td><code>monitor:DescribeBasicAlarmList</code></td><td>用于获取函数监控信息</td>
	</tr>
	<tr>
	<td><code>cam:GetRole</code></td><td>用于获取用户角色信息</td>
	</tr>
	<tr>
	<td><code>cam:ListAttachedRolePolicies</code></td><td>用于获取用户角色策略信息</td>
	</tr>
	<tr>
	<td><code>vpc:DescribeVpcEx</code></td><td>用于获取网络信息</td>
	</tr>
	<tr>
	<td><code>vpc:DescribeSubnetEx</code></td><td>用于获取网络信息</td>
	</tr>
	<tr>
	<td><code>apigw:DescribeDomain</code></td><td>用于获取网关信息 </td>
	</tr>
	<tr>
	<td><code>cls:getLogset</code></td><td>用于获取日志信息</td>
	</tr>
  <tr>
	<td><code>cls:getTopic</code></td><td>用于获取日志信息 </td>
	</tr>
</table>
- 预设策略 QcloudSCFReadOnlyAccess 当前权限如下：
``` json
{
   "version":"2.0",
   "statement":[
      {
         "action":[
            "scf:Get*",
            "scf:List*",
            "monitor:GetMonitorData",
            "monitor:DescribeBasicAlarmList",
            "name/cam:GetRole",
            "name/cam:ListAttachedRolePolicies",
            "vpc:DescribeVpcEx",
            "vpc:DescribeSubnetEx",
            "apigw:DescribeDomain",
            "cls:getLogset",
            "cls:getTopic"
         ],
         "resource":"*",
         "effect":"allow"
      }
   ]
}
```
- 预设策略 QcloudAccessForScfRole 当前权限如下：
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
                "cmqtopic:*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```
预设策略 QcloudAccessForScfRole 具备以下功能：
 - 配置 COS 对象存储触发器时，向 Bucket 配置中写入触发配置信息。 
 - 读取 COS 对象存储 Bucket 中的触发器配置信息。 
 - 在使用 COS 对象存储更新代码时，从 Bucket 完成代码 zip 包的读取操作。 
 - 配置 API 网关触发器时，完成 API 网关的服务、API 创建以及服务发布等操作。 
