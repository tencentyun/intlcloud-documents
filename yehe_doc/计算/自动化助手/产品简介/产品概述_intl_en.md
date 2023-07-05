## What is TencentCloud Automation Tools?
TencentCloud Automation Tools (TAT) is a native Ops deployment tool for Tencent Cloud CVM and Lighthouse instances. TAT provides an automated approach for batch execution of commands (Shell, PowerShell, Python, etc.) for common daily tasks, such as running automated Ops scripts, polling processes, installing/uninstalling software, updating applications, and installing patches, without the need of instance login and password. 

### Batch execution
TAT enables you to remotely manage large-scale instances in a secure and reliable manner. TAT can execute Shell, PowerShell and Python commands in batches without using jump servers. You can use it for the automatic operation of common management tasks.

### Interactive session management
TAT provides a browser-based interactive Shell, which enables you to manage instances without the need to open inbound ports or manage SSH keys.

### Public command library
Tencent Cloud provides commands for common instance management and Ops tasks. You can also configure custom parameters as needed. For more requirements, please [contact us](https://intl.cloud.tencent.com/document/product/1147/46052).



## Command Execution Status[](id:Status)
When you execute a command on an instance, the instance-level command [execution status](https://intl.cloud.tencent.com/document/product/1147/46053) include the following: 
<table>
<tr>
<th>API return message</th><th>Status in console</th><th>Description</th>
</tr>
<tr>
<td>PENDING</td><td>Waiting to be delivered</td>
<td>The command is waiting to be delivered by the system.</td>
</tr>
<tr>
<td>DELIVERING</td><td>Delivering</td>
<td>The command is being delivered to the target instance</td>
</tr>
<tr>
<td>DELIVER_DELAYED</td><td>Delayed delivery</td>
<td>The command delivery is delayed.</td>
</tr>
<tr>
<td>DELIVER_FAILED</td><td>Delivery failed</td>
<td>Failed to deliver the command</td>
</tr>
<tr>
<td>RUNNING</td><td>Executing</td>
<td>The command is being executed.</td>
</tr>
<tr>
<td>TIMEOUT</td><td>Command timeout</td>
<td>The command failed to complete in the specified timed out period.</td>
</tr>
<tr>
<td>SUCCESS</td><td>Command completed</td>
<td>The command execution is completed. Note that it does not mean that the task is successful. You need to check the `Output` and `ExitCode` of the result to see whether it’s successful. </td>
</tr>
<tr>
<td>TASK_TIMEOUT</td><td>Task execution timeout</td>
<td>The task is ended due to the command execution timeout.</td>
</tr>
<tr>
<td>FAILED</td><td>Command failed</td>
<td>Unable to execute the command, or the command execution failed.</td>
</tr>
</table>
