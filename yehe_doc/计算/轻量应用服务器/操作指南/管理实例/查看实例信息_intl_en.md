## Overview
After creating a Lighthouse instance, you can view its details in the console.

## Directions
### Viewing instance list information
Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index), and you can view instances in different regions and statuses on the instance list page.
![](https://qcloudimg.tencent-cloud.cn/raw/ef8cdca543a670653a2b6763e03ba897.png)


### Viewing instance details
 In the instance list, find the target instance and enter its details page to view its information.


<dx-accordion>
::: Overview
On this tab, you can view the basic, monitoring, network, image, application, billing, and TencentCloud Automation Tools information of the instance as detailed below:
<table>
	<tr><th width="17%">Information Category</th><th>Description</th></tr>
	<tr><td>Instance information</td>
	<td>You can view the following basic instance information:<ul  style="margin: 0;">
	<li>Name/ID: The instance name can be modified.</li>
	<li>Region and availability zone: Instance region and AZ.</li>
	<li>Bundle type: Type of the bundle used by the instance.</li>
	<li>Instance specification: CPU and memory specification.</li>
	<li>System disk: Storage space of the system disk.</li>
	<li>Data transfer: Bandwidth and traffic package.</li>
	<li>SSH key: SSH key pair bound with the instance.</li>
	<li>Tag: Tags bound with the instance.</li>
	</ul>
	</td></tr>
	<tr><td>Instance monitoring information</td>
	<td>You can view the following basic monitoring data of the instance:<ul  style="margin: 0;">
	<li>CPU utilization (%).</li>
	<li>Memory usage (MB).</li>
	<li>Public network (Mbps).</li>
	<li>System disk IO (KB/s).</li>
  </ul></td></tr>
	<tr><td>Remote login</td>
	<td>You can select an instance login method as needed.</td></tr>
	<tr><td>Resources</td>
	<td>You can directly view the instance traffic package and system disk usage.</td></tr>	
	<tr><td>Network information</td>
	<td>You can view the following instance network information:<ul  style="margin: 0;">
	<li>IP: Public IP address (for instance access over the public network) and private IP address (for inter-instance communication).</li>
	<li>Firewall: You can configure instance firewall rules.</li>
	</ul></td></tr>
	<tr><td>Security information</td>
	<td>You can view the following DDoS protection information of the instance:<ul  style="margin: 0;">
	<li>Protection type: You can purchase an Anti-DDoS instance as needed.</li>
	<li>Protection specification: Anti-DDoS instance specification.</li>
	<li>Security status: Anti-DDoS status of the instance.</li>
	</ul></td></tr>
	<tr><td>Image details</td>
	<td>You can view the following basic instance image information:<ul  style="margin: 0;">
	<li>Image name: Specific image name. You can reset the application or create a custom image.</li>
	<li>Image type: Specific image type.</li>
	<li>Operating system: Image operating system version.</li>
	</ul>
	</td>
	</tr>
	<tr>
	<td>Application information</td>
	<td>You can view the instance application information:<br>
For an instance created by using an application image, you can view the pre-installed software information and manage applications on the pre-installed application page.
	</td></tr>
	<tr><td>Billing information</td>
	<td>You can view the following instance billing information and terminate the instance:<ul  style="margin: 0;">
	<li>Creation time: Instance creation time.</li>
	<li>Expiry time: Instance expiration time. To renew the instance, click <b>Renew</b>.</li>
	<li>Auto-renewal: Whether auto-renewal is enabled for the instance. To set auto-renewal, click <b>Enable</b>.</li>
	<li>Upgrade bundle: Click <b>Upgrade bunble</b> to upgrade the instance bundle.</li>
	<li>Terminate instance: Click <b>Terminate</b> to terminate the instance if you no longer need it.</li>
	</ul></td></tr>
	<tr>
	<td>TencentCloud Automation Tools</td>
	<td>You can view the TencentCloud Automation Tools status information and perform relevant operations on the **Run commands** tab.
	</td></tr>
</table>
	On this tab, you can perform operations including instance <b>shutdown</b>, <b>restart</b>, <b>password resetting</b>, <b>remote login</b>, <b>application resetting</b>, and <b>image creation</b>.
:::
::: Pre-installed application
On this tab, you can view the basic application information, such as the application name, version number, and instance status. You can also reset the application and shut down, restart, or log in to the instance.
In addition, the **Pre-installed application** tab also displays the details of the pre-installed software in the application, such as configuration file directory, admin account and password, and application software installation path.

<dx-alert infotype="explain" title="">
As custom images don't have a unified template and are created based on your own data, the instances created by using them don't have the <b>Pre-installed application</b> tab.
</dx-alert>

:::
::: Cloud disk
View and manage instance data disks.
:::
::: Firewall
View and manage instance firewall rules.
:::
::: Key pair
View and manage key pairs bound to the instance.
:::
::: Snapshot
View, manage, and create instance snapshots.
:::
::: Monitoring
View instance CPU, memory, public network bandwidth, and disk usage monitoring data.
:::
::: Run commands
View the command execution details of TencentCloud Automation Tools and create and run commands.
:::
</dx-accordion>



