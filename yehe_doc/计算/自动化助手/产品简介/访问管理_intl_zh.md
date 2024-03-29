## 简介
[访问管理](https://intl.cloud.tencent.com/document/product/598/10583)（Cloud Access Management，CAM）是腾讯云提供的 Web 服务，主要用于帮助用户对腾讯云账户下资源的访问权限的安全管理。您可以通过 CAM 创建、管理和销毁用户或用户组，并使用身份管理和策略管理控制其他用户使用腾讯云资源的权限。策略能够授权或者拒绝用户使用指定资源完成指定任务，当您在使用 CAM 时，可以将策略与一个用户或一组用户关联起来进行权限控制。

自动化助手已接入 CAM，您可以使用 CAM 对自动化助手服务的相关资源进行权限控制。

## 支持 CAM 的粒度
自动化助手支持资源级授权、按标签授权两种方式：
* **资源级授权**：您可以通过策略语法给子账号单个资源的管理的权限，详细请参考 [授权指南](https://intl.cloud.tencent.com/document/product/598/35596)。
* **按标签授权**：您可以通过给资源标记标签，实现基于标签管理项目资源。

## 预设策略

|预设策略名|授权范围描述|
|--|--|
|QcloudTATReadOnlyAccess|自动化助手只读访问权限|
|QcloudTATFullAccess|自动化助手全读写访问权限|

## 可授权的资源类型

自动化助手支持资源级授权，您可以指定子账号拥有特定资源的接口权限。

在访问管理中对自动化助手可授权的资源类型如下：

|资源类型|授权策略中的资源描述方法|
|--|--|
|远程命令相关|`qcs::tat:$region:$account:command/$commandId`|

支持操作级授权的接口列表如下：

|API 名|API 描述|资源|
|--|--|--|
|CreateCommand|创建命令|\*|

支持资源级授权的接口列表如下：

<table>
<thead>
<tr>
<th>API 接口<br>接口描述</th>
<th>资源类型</th>
<th>资源六段式</th>
</tr>
</thead>
<tbody><tr>
<td>DeleteCommand<br>删除命令</td>
<td>命令</td>
<td><code>qcs::tat:$region:$account:command/$commandId</code></td>
</tr>
<tr>
<td>DescribeAutomationAgents<br>查询 Agent 运行状态</td>
<td>云服务器实例、轻量应用服务器实例</td>
<td><code>qcs::cvm:$region:$account:instance/$instanceId</code> <br> <code>qcs::lighthouse:$region:$account:instance/$instanceId</code></td>
</tr>
<tr>
<td>DescribeCommands<br>查询命令</td>
<td>命令</td>
<td><code>qcs::tat:$region:$account:command/$commandId</code></td>
</tr>
<tr>
<td>DescribeInvocations<br>查询执行结果</td>
<td>命令</td>
<td><code>qcs::tat:$region:$account:command/$commandId</code></td>
</tr>
<tr>
<td>DescribeInvocationTasks<br>查询执行任务</td>
<td>命令、云服务器实例、轻量应用服务器实例</td>
<td><code>qcs::tat:$region:$account:command/$commandId</code><br><code>qcs::cvm:$region:$account:instance/$instanceId</code><br><code>qcs::lighthouse:$region:$account:instance/$instanceId</code></td>
</tr>
<tr>
<td>InvokeCommand<br>触发命令</td>
<td>命令、云服务器实例、轻量应用服务器实例</td>
<td><code>qcs::tat:$region:$account:command/$commandId</code><br><code>qcs::cvm:$region:$account:instance/$instanceId</code><br><code>qcs::lighthouse:$region:$account:instance/$instanceId</code></td>
</tr>
<tr>
<td>ModifyCommand<br>修改命令</td>
<td>命令</td>
<td><code>qcs::tat:$region:$account:command/$commandId</code></td>
</tr>
<tr>
<td>PreviewReplacedCommandContent<br>查询渲染后命令</td>
<td>命令</td>
<td><code>qcs::tat:$region:$account:command/$commandId</code></td>
</tr>
<tr>
<td>RunCommand<br>运行命令</td>
<td>命令、云服务器实例、轻量应用服务器实例</td>
<td><code>qcs::tat:$region:$account:command/$commandId</code><br><code>qcs::cvm:$region:$account:instance/$instanceId</code><br><code>qcs::lighthouse:$region:$account:instance/$instanceId</code></td>
</tr>
</tbody></table>

## 授权方案示例

您可通过以下示例，快速了解如何使用 CAM 进行权限控制：
 - [允许修改和删除命令](#example1)
 - [允许查看命令详情](#example2)
 - [允许查看命令执行结果](#example3)
 - [禁止用户执行命令](#example4)
 - [禁止用户执行任何命令](#example5)
 - [禁止用户在云服务器实例上执行任何命令](#example6)
 - [禁止用户在任何云服务器实例上执行命令](#example7)
 - [禁止用户在轻量应用服务器实例上执行任何命令](#example8)
 - [禁止用户在任何轻量应用服务器实例上执行命令](#example9)
 - [允许用户在云服务器实例上执行命令](#example10)
 - [允许用户在轻量应用服务器实例上执行命令](#example11)
 - [禁止用户查看云服务器实例的命令执行任务结果](#example12)
 - [禁止用户查看轻量应用服务器实例的命令执行任务结果](#example13)
 - [禁止用户查看云服务器实例的 Agent 运行状态](#example14)
 - [禁止用户查看轻量应用服务器实例的 Agent 运行状态](#example15)

>?示例均以广州地域为例，其中的 `$account` 需要替换为用户主账号。
>
- 允许修改和删除命令 cmd-xxxxxxxx。[](id:example1)
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "resource": [
                "qcs::tat:ap-guangzhou:$account:command/cmd-xxxxxxxx"
            ],
            "action": [
                "tat:ModifyCommand",
                "tat:DeleteCommand"
            ]
        }
    ]
}
```
- 允许查看命令 cmd-xxxxxxxx 的详情。[](id:example2)
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "resource": [
                "qcs::tat:ap-guangzhou:$account:command/cmd-xxxxxxxx"
            ],
            "action": [
                "tat:DescribeCommands"
            ]
        }
    ]
}
```
- 允许查看命令 cmd-xxxxxxxx 的执行结果。[](id:example3)
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "resource": [
                "qcs::tat:ap-guangzhou:$account:command/cmd-xxxxxxxx"
            ],
            "action": [
                "tat:DescribeInvocations",
                "tat:DescribeInvocationTasks"
            ]
        }
    ]
}
```
- 禁止用户执行命令 cmd-xxxxxxxx。[](id:example4)
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "deny",
            "resource": [
                "qcs::tat:ap-guangzhou:$account:command/cmd-xxxxxxxx"
            ],
            "action": [
                "tat:InvokeCommands"
            ]
        }
    ]
}
```
- 禁止用户执行任何命令。[](id:example5)
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "deny",
            "resource": [
                "qcs::tat:ap-guangzhou:$account:command/*"
            ],
            "action": [
                "tat:InvokeCommand",
                "tat:RunCommand"
            ]
        }
    ]
}
```
- 禁止用户在云服务器实例 ins-xxxxxxxx 上执行任何命令。[](id:example6)
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "deny",
            "resource": [
                "qcs::cvm:ap-guangzhou:$account:instance/ins-xxxxxxxx"
            ],
            "action": [
                "tat:InvokeCommand",
                "tat:RunCommand"
            ]
        }
    ]
}
```
- 禁止用户在任何云服务器实例上执行命令。[](id:example7)
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "deny",
            "resource": [
                "qcs::cvm:ap-guangzhou:$account:instance/*"
            ],
            "action": [
                "tat:InvokeCommand",
                "tat:RunCommand"
            ]
        }
    ]
}
```
- 禁止用户在轻量应用服务器实例 lhins-xxxxxxxx 上执行任何命令。[](id:example8)
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "deny",
            "resource": [
                "qcs::lighthouse:ap-guangzhou:$account:instance/lhins-xxxxxxxx"
            ],
            "action": [
                "tat:InvokeCommand",
                "tat:RunCommand"
            ]
        }
    ]
}
```
- 禁止用户在任何轻量应用服务器实例上执行命令。[](id:example9)
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "deny",
            "resource": [
                "qcs::lighthouse:ap-guangzhou:$account:instance/*"
            ],
            "action": [
                "tat:InvokeCommand",
                "tat:RunCommand"
            ]
        }
    ]
}
```
- 允许用户在云服务器实例 ins-xxxxxxxx 上执行命令 cmd-xxxxxxxx 或 cmd-yyyyyyyy。[](id:example10)
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "resource": [
                "qcs::cvm:ap-guangzhou:$account:instance/ins-xxxxxxxx",
                "qcs::tat:ap-guangzhou:$account:command/cmd-xxxxxxxx",
                "qcs::tat:ap-guangzhou:$account:command/cmd-yyyyyyyy"
            ],
            "action": [
                "tat:InvokeCommand"
            ]
        }
    ]
}
```
- 允许用户在轻量应用服务器实例 lhins-xxxxxxxx 上执行命令 cmd-xxxxxxxx 或 cmd-yyyyyyyy。[](id:example11)
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "resource": [
                "qcs::lighthouse:ap-guangzhou:$account:instance/lhins-xxxxxxxx",
                "qcs::tat:ap-guangzhou:$account:command/cmd-xxxxxxxx",
                "qcs::tat:ap-guangzhou:$account:command/cmd-yyyyyyyy"
            ],
            "action": [
                "tat:InvokeCommand"
            ]
        }
    ]
}
```
- 禁止用户查看云服务器实例 ins-xxxxxxxx 的命令执行任务结果。[](id:example12)
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "deny",
            "resource": [
                "qcs::cvm:ap-guangzhou:$account:instance/ins-xxxxxxxx"
            ],
            "action": [
                "tat:DescribeInvocationTasks"
            ]
        }
    ]
}
```
- 禁止用户查看轻量应用服务器实例 lhins-xxxxxxxx 的命令执行任务结果。[](id:example13)
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "deny",
            "resource": [
                "qcs::lighthouse:ap-guangzhou:$account:instance/lhins-xxxxxxxx"
            ],
            "action": [
                "tat:DescribeInvocationTasks"
            ]
        }
    ]
}
```
-  禁止用户查看云服务器实例 ins-xxxxxxxx 的 Agent 运行状态。[](id:example14)
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "deny",
            "resource": [
                "qcs::cvm:ap-guangzhou:$account:instance/ins-xxxxxxxx"
            ],
            "action": [
                "tat:DescribeAutomationAgentStatus"
            ]
        }
    ]
}
```
- 禁止用户查看轻量应用服务器实例 lhins-xxxxxxxx 的 Agent 运行状态。[](id:example15)
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "deny",
            "resource": [
                "qcs::lighthouse:ap-guangzhou:$account:instance/lhins-xxxxxxxx"
            ],
            "action": [
                "tat:DescribeAutomationAgentStatus"
            ]
        }
    ]
}
```
