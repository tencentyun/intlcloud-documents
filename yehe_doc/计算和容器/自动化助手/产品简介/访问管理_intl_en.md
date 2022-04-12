## Overview
[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583) is a web-based Tencent Cloud service that helps you with the security management of access permissions for resources under your Tencent Cloud account. With CAM, you can create, manage, and terminate users or user groups, and can use identity and policy management to control the permissions other users have to use Tencent Cloud resources. Policies can be used to authorize or block the use of specified resources by users to complete specified tasks. When you use CAM, you can associate policies with a user or user group to perform permissions control.

TAT is connected with CAM for permission controlling.  

## Access Control Levels
TAT supports the access control by resources and tags.
* **Resource-level control**: Specify a policy to assign a sub-account with permissions to a single resource. For details, see [Creating Custom Policy](https://intl.cloud.tencent.com/document/product/598/35596).
* **Control by tags**: Add tags to resources for access control

## Preset Policies

| Preset policy | Permissions granted |
|--|--|
|QcloudTATReadOnlyAccess| TAT read-only permission  |
|QcloudTATFullAccess|TAT read/write permission|

## Types of Manageable Resources

TAT supports resource-level authorization. You can grant a specified sub-account the API permission of a specified resource.

In CAM, the types of TAT resources that can be authorized are as follows:

| Resource Type | Resource Description Method in Authorization Policy |
|--|--|
|Remote command-related|`qcs::tat:$region:$account:command/$commandId`|

APIs supporting action-level authorization include:

| API name | Description | Resource |
|--|--|--|
|CreateCommand| Create a command |\*|

APIs supporting resource-level authorization include:

<table>
<thead>
<tr>
<th>API name<br>API description</th>
<th>Resource type</th>
<th>Resource (in six-segment format)</th>
</tr>
</thead>
<tbody><tr>
<td>DeleteCommand<br>Delete a command</td>
<td>Command</td>
<td><code>qcs::tat:$region:$account:command/$commandId</code></td>
</tr>
<tr>
<td>DescribeAutomationAgents<br>Query the agent running status</td>
<td>CVM instances, Lighthouse instances</td>
<td><code>qcs::cvm:$region:$account:instance/$instanceId</code> <br> <code>qcs::lighthouse:$region:$account:instance/$instanceId</code></td>
</tr>
<tr>
<td>DescribeCommands<br>Query a command</td>
<td>Command</td>
<td><code>qcs::tat:$region:$account:command/$commandId</code></td>
</tr>
<tr>
<td>DescribeInvocations<br>Query the execution result</td>
<td>Command</td>
<td><code>qcs::tat:$region:$account:command/$commandId</code></td>
</tr>
<tr>
<td>DescribeInvocationTasks<br>Query the execution tasks</td>
<td>Command, CVM instances, Lighthouse instances</td>
<td><code>qcs::tat:$region:$account:command/$commandId</code><br><code>qcs::cvm:$region:$account:instance/$instanceId</code><br><code>qcs::lighthouse:$region:$account:instance/$instanceId</code></td>
</tr>
<tr>
<td>InvokeCommand<br>Invoke a command</td>
<td>Command, CVM instances, Lighthouse instances</td>
<td><code>qcs::tat:$region:$account:command/$commandId</code><br><code>qcs::cvm:$region:$account:instance/$instanceId</code><br><code>qcs::lighthouse:$region:$account:instance/$instanceId</code></td>
</tr>
<tr>
<td>ModifyCommand<br>Modify a command</td>
<td>Command</td>
<td><code>qcs::tat:$region:$account:command/$commandId</code></td>
</tr>
<tr>
<td>PreviewReplacedCommandContent<br>Query the command after rendering</td>
<td>Command</td>
<td><code>qcs::tat:$region:$account:command/$commandId</code></td>
</tr>
<tr>
<td>RunCommand<br>Run a command</td>
<td>Command, CVM instances, Lighthouse instances</td>
<td><code>qcs::tat:$region:$account:command/$commandId</code><br><code>qcs::cvm:$region:$account:instance/$instanceId</code><br><code>qcs::lighthouse:$region:$account:instance/$instanceId</code></td>
</tr>
</tbody></table>

## Examples

Check the examples below to learn about how to control permissions by using CAM.
 - [Allow a user to modify and delete commands](#example1)
 - [Allow a user to check command details](#example2)
 - [Allow a user to check command execution results](#example3)
 - [Disallow a user from executing a specified command](#example4)
 - [Disallow a user from executing any commands](#example5)
 - [Disallow a user from executing any commands on a specified CVM](#example6)
 - [Disallow a user from executing commands on any CVMs](#example7)
 - [Disallow a user from executing any commands on a specified Lighthouse instance](#example8)
 - [Disallow a user from executing commands on any Lighthouse instances](#example9)
 - [Allow a user to execute the specified commands on the specified CVM](#example10)
 - [Allow a user to execute the specified commands on the specified Lighthouse instance](#example11)
 - [Disallow a user to check the command execution result on a CVM](#example12)
 - [Disallow a user to check the command execution result on a Lighthouse instance](#example13)
 - [Disallow a user to check the Agent status on a CVM](#example14)
 - [Disallow a user to check the Agent status on a Lighthouse instance](#example15)

>? Guangzhou region is used for all the examples below. Replace `$account` with the Tencent Cloud root account of the user.
>
- Allow a user to modify and delete the command `cmd-xxxxxxxx`[](id:example1)
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
- Allow a user to check the details of the command `cmd-xxxxxxxx`[](id:example2)
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
- Allow a user to check the result of the command `cmd-xxxxxxxx`[](id:example3)
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
- Disallow a user from executing the command `cmd-xxxxxxxx`[](id:example4)
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
- Disallow a user from executing any commands[](id:example5)
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
- Disallow a user from executing any commands on the CVM `ins-xxxxxxxx`[](id:example6)
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
- Disallow a user from executing commands on any CVMs[](id:example7)
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
- Disallow a user from executing any commands on the Lighthouse instance `lhins-xxxxxxxx`[](id:example8)
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
- Disallow a user from executing commands on any Lighthouse instances[](id:example9)
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
- Allow a user to execute the command `cmd-xxxxxxxx` or `cmd-yyyyyyyy` on the CVM `ins-xxxxxxxx`[](id:example10)
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
- Allow a user to execute the command `cmd-xxxxxxxx` or `cmd-yyyyyyyy` on the Lighthouse instance `lhins-xxxxxxxx`[](id:example11)
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
- Disallow a user from checking the command execution result on the CVM `ins-xxxxxxxx`[](id:example12)
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
- Disallow a user from checking the command execution result on the Lighthouse instance `lhins-xxxxxxxx`[](id:example13)
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
- Disallow a user from checking the Agent status on the CVM `ins-xxxxxxxx`[](id:example14)
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
- Disallow a user from checking the Agent status on the Lighthouse instance `lhins-xxxxxxxx`[](id:example14)
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
