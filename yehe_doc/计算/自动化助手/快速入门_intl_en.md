TAT lets you manage Tencent Cloud services by using the console, API and SDK. This document guides you through the usage of TAT by taking Lighthouse console as an example.

## Step 1. Installing TAT agent

<dx-alert infotype="explain" title="">
- TAT agent is pre-installed for instances created using public images after Dec 15, 2020. For instances created before this time, you need to install it manually.
- TAT agent is only available for VPC-based instances.
</dx-alert>

See [Installing TAT Agent](https://intl.cloud.tencent.com/document/product/1147/46042).


## Step 2. Create a command
1. Log in to the Lighthouse console and select [My Commands](https://console.cloud.tencent.com/lighthouse/command) under **Automation Tools** on the left sidebar.
2. In the **My commands** page, click **Create command**.
3. Configure the parameters in the **Create command** page.
<img src="https://qcloudimg.tencent-cloud.cn/raw/81724cc3c157d55c8492839bcb9b5ad8.png" style="width:70%"/>
<table>
<tr>
<th style="width:14%">Parameter</th>
<th>Description</th>
</tr>
<tr>
<td>Command name</td>
<td>Enter the command name.</td>
</tr>
<tr>
<td>Command type</td>
<td>Select a command type.
</td>
</tr>
<tr>
<td>Execution path</td>
<td>Enter the execution path of the command.
<ul style="margin-bottom:0px">
<li>For Linux instances, the path defaults to the /home of the root account.</li>
<li>For Windows instances, it defaults to C:\\Program Files\\qcloud\\tat_agent\\workdir of the System user</li>
</ul>
</td>
</tr>
<td>Execution user</td>
<td>The user who executes the command.
<ul style="margin-bottom:0px">
<li>For Linux instances, it defaults to the root user.</li>
<li>For Windows instances, it defaults to the System user.</li>
</ul>
</td>
</tr>
<tr>
<td>Timeout period</td>
<td>Set the timeout period of the command in the instance. When the task executing the command times out, the task process is terminated. It defaults to 60 seconds, and the range of values is [1, 86400].</td>
</tr>
<tr>
<td>Command content</td>
<td>Edit or paste your command.</td>
</tr>
<tr>
<td>Use parameters</td>
<td>Specify whether to use parameters in the command. You can configure the variable values in the command in the format of <code>{{key}}</code>.</td>
</tr>
</table>
4. Click **Save command** to complete the creation.

## Step 3. Execute the command

<dx-alert infotype="explain" title="">
The target instance must be based on a VPC.
</dx-alert>


1. In the **My commands** page, select the target command and click **Execute**.
2. In the **Execute command** window, select the target instance.
3. Click **Execute command**. 
After the task execution, you can check the task result in **My commands - Logs - Log details**.
