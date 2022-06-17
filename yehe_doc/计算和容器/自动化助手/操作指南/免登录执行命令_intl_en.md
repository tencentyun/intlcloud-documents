## Overview
This document describes how to execute TAT commands without logging in to a Lighthouse instance.

## Prerequisites
- The target instance is running.
- The TAT agent is installed on the target instance. See [Installing TAT Agent](https://intl.cloud.tencent.com/document/product/1147/46042).
- The target instance in based on a VPC.

## Directions
1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index) and select the target instance.
2. On the instance details page, select **Execute command**.
![](https://qcloudimg.tencent-cloud.cn/raw/38ce8f3f14e14c8e85ee9a7fc775742c.png)
3. On the command list page, click **Execute commmand**.
4. On the pop-up window, configure the parameters.
![](https://qcloudimg.tencent-cloud.cn/raw/b9ea8226605f2f486cc53316b851962a.png)
 - **Command source**: Select the source of the command.
 - **More**: Configure the optional parameters as needed.
<table>
<tr>
<th style="width:22%">Parameter</th>
<th>Description</th>
</tr>
<tr>
<td>Target path</td>
<td>The execution path of the command.
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
<td>Use parameters</td>
<td>Specify whether to use parameters in the command. You can configure the variable values in the command in the format of <code>{{key}}</code>.</td>
</tr>
</table>
6. Click **Execute command** to execute the command without logging in to the instance.
