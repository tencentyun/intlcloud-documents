## Background
TencentDB for MariaDB upgraded the monitoring items for server and component services on April 1, 2021 by replacing the legacy alarm policy type and modifying hundreds of monitoring and alarm metrics. You can configure alarm policies of the [MariaDB](https://intl.cloud.tencent.com/document/product/248/40015) type in the Cloud Monitor console.

The legacy MariaDB policy type was deactivated on July 29, 2021. You cannot configure new alarm policies in this type any more, and your previously configured MariaDB alarm polices will be gradually transferred to the new policy type.

#### Comparison of the legacy and new alarm policy types
| Policy Type | Metric Coverage | Support and Maintenance |
| ------------- | -------------------------- | ----------------------- |
| MariaDB | 22 metrics | This policy type was deactivated on July 29, 2021 and cannot be configured subsequently. All legacy alarm policies will be transferred to the new policy type. |
| Cloud Database - MariaDB | 37 metrics | This policy type was released on April 1, 2021 with ongoing maintenance available. |

>!
>- The new MariaDB policy type will cover all metrics of the legacy MariaDB policy type. For more information, please see [Comparison Table of New and Legacy Metrics](#jump).
>- For the new alarm policies, please see [New Metric Description](#jump2).

## Alarm Policy Transfer
After the legacy MariaDB policy type is deactivated, the system will automatically transfer previously configured alarm policies to the new MariaDB policy type on the backend.
>?Alarms may not be automatically transferred to the new alarm policy type by the system for certain instances or users. If this is the case for you, we will notify you through Message Center, email, or SMS. Then, please follow the manual transfer steps below to manually transfer the alarms.

#### Manual transfer steps
1. Sort out exiting alarm metrics and policies.
  1. Log in to the [Cloud Monitor console](https://console.cloud.tencent.com/monitor/alarm2/policy), select **Alarm Configuration** > **Alarm Policy** on the left sidebar, and click **Advanced Filter**.
  2. On the pop-up page, select the alarm policy type corresponding to **MariaDB** in **Policy Type**, query alarm policies in this category, and download the previously configured alarm policies of the legacy **MariaDB** policy type.
![](https://main.qcloudimg.com/raw/ed7a4d614743d251b63c83e24714735a.png)
2. Configure new alarm policies.
  1. On the **[Alarm Policy](https://console.cloud.tencent.com/monitor/alarm2/policy)** page, click **Create**.
  2. On the **Create Alarm Policy** page, select **MariaDB** for **Policy Type** and configure alarms according to the policies downloaded in step 1. For the configuration method, please see [Creating Alarm Policy](https://intl.cloud.tencent.com/document/product/248/38916).
3. Verify whether the MariaDB alarm policies are enabled and can successfully trigger alarms.
Set a minimum trigger threshold in **Metric alarm** on the **Create Alarm Policy** page, choose to set a **recipient** or **recipient group**, and select the notification channel (email or SMS) to test a policy. For example, you can configure an alarm policy for the CPU utilization metric that triggers an alarm once per minute when the threshold is greater than or equal to 1% for one statistical period of one minute.
4. After the new policy type is verified, delete the alarm policies previously configured under the legacy MariaDB policy type.
On the **[Alarm Policy](https://console.cloud.tencent.com/monitor/alarm2/policy)** page, filter alarm policies by the "MariaDB" policy type and delete the filtered policies according to the policy list downloaded in step 1.
If you encounter any issues during the transfer, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

## [Comparison Table of New and Legacy Metrics](id:jump)
<table>
<thead><tr><th><strong>Legacy Policy Type</strong></th><th><strong>Metric/Event Alarm</strong></th><th><strong>Legacy Metric/Event Alarm Name</strong></th><th><strong>New Policy Type</strong></th><th><strong>New Metric/Event Alarm Name</strong></th></tr></thead>
<tbody><tr>
<td rowspan="22">MariaDB</td>
<td>Metric alarm</td><td>CPU utilization	</td>
<td>Cloud Database - MariaDB - Instance</td><td>CPU utilization</tr>
<tr>
<td>Metric alarm</td><td>Primary-Replica switch</td>
<td>Cloud Database - MariaDB - Instance</td><td>Primary-Replica switches</tr>
<tr>
<td>Metric alarm</td><td>	Available disk space	</td>
<td>Cloud Database - MariaDB - Instance</td><td>Available data disk space</tr>
<tr>
<td>Metric alarm</td><td>	Log disk space	</td>
<td>Cloud Database - MariaDB - Instance</td><td>Minimum remaining binlog disk space</tr>
<tr>
<td>Metric alarm</td><td>	SELECT queries	</td>
<td>Cloud Database - MariaDB - Instance</td><td>Total SELECT requests</tr>
<tr>
<td>Metric alarm</td><td>	Slow queries	</td>
<td>Cloud Database - MariaDB - Instance</td><td>Slow queries</tr>
<tr>
<td>Metric alarm</td><td>	UPDATE queries	</td>
<td>Cloud Database - MariaDB - Instance</td><td>UPDATE requests</tr>
<tr>
<td>Metric alarm</td><td>	INSERT queries	</td>
<td>Cloud Database - MariaDB - Instance</td><td>INSERT requests</tr>
<tr>
<td>Metric alarm</td><td>	DELETE queries	</td>
<td>Cloud Database - MariaDB - Instance</td><td>DELETE requests</tr>
<tr>
<td>Metric alarm</td><td>	Available memory size	</td>
<td>Cloud Database - MariaDB - Instance</td><td>Available cache space</tr>
<tr>
<td>Metric alarm</td><td>	Disk IOPS	</td>
<td>Cloud Database - MariaDB - Instance</td><td>IO utilization</tr>
<tr>
<td>Metric alarm</td><td>	Active connections	</td>
<td>Cloud Database - MariaDB - Instance</td><td>Total active threads</tr>
<tr>
<td>Metric alarm</td><td>	Connection utilization	</td>
<td>Cloud Database - MariaDB - Instance</td><td>Maximum database connection utilization</tr>
<tr>
<td>Metric alarm</td><td>	Disk utilization	</td>
<td>Cloud Database - MariaDB - Instance</td><td>Data disk utilization</tr>
<tr>
<td>Metric alarm</td><td>	REPLACE_SELECT queries	</td>
<td>Cloud Database - MariaDB - Instance</td><td>REPLACE_SELECT requests</tr>
<tr>
<td>Metric alarm</td><td>	Logical reads from InnoDB disk	</td>
<td>Cloud Database - MariaDB - Instance</td><td>Total logical reads from InnoDB disk</tr>
<tr>
<td>Metric alarm</td><td>	Logical reads from InnoDB buffer pool	</td>
<td>Cloud Database - MariaDB - Instance</td><td>Total logical reads from InnoDB buffer pool</tr>
<tr>
<td>Metric alarm</td><td>	Pages read into InnoDB buffer pool by read-ahead thread	</td>
<td>Cloud Database - MariaDB - Instance</td><td>Total pages read into InnoDB buffer pool by read-ahead thread</tr>
<tr>
<td>Metric alarm</td><td>	Rows deleted from InnoDB tables	</td>
<td>Cloud Database - MariaDB - Instance</td><td>Rows deleted from InnoDB Tables</tr>
<tr>
<td>Metric alarm</td><td>	Rows inserted into InnoDB tables	</td>
<td>Cloud Database - MariaDB - Instance</td><td>Rows inserted into InnoDB tables</tr>
<tr>
<td>Metric alarm</td><td>	Rows updated to InnoDB tables	</td>
<td>Cloud Database - MariaDB - Instance</td><td>Rows updated to InnoDB tables</tr>
<tr>
<td>Metric alarm</td><td>	Used log disk space	</td>
<td>Cloud Database - MariaDB - Instance</td><td>Used binlog disk space</tr>
</tbody></table>

## [New Metric Description](id:jump2)
<table>
<thead><tr><th><strong>Policy Type</strong></th><th><strong>Metric/Event Alarm</strong></th><th><strong>Metric/Event Alarm Name</strong></th></tr></thead>
<tbody><tr>
<td rowspan="30">Cloud Database - MariaDB</td>
<td>Metric alarm</td><td>	Total rows read from InnoDB tables		</td></tr>
<td>Metric alarm</td><td>	Minimum replica node delay		</td></tr>
<td>Metric alarm</td><td>Buffer cache hit ratio</td></tr>
<td>Metric alarm</td><td>	REPLACE count		</td></tr>
<td>Metric alarm</td><td>	Requests consuming less than 5 ms		</td></tr>
<td>Metric alarm</td><td>	Requests consuming 5–20 ms		</td></tr>
<td>Metric alarm</td><td>	Requests consuming 21–30 ms		</td></tr>
<td>Metric alarm</td><td>	Requests consuming more than 30 ms		</td></tr>
<td>Metric alarm</td><td>	SQL throughput		</td></tr>
<td>Metric alarm</td><td>	SQL error throughput		</td></tr>
<td>Metric alarm</td><td>	SQL success throughput		</td></tr>
<td>Metric alarm</td><td>	Total client connections		</td></tr>
<td>Metric alarm</td><td>	Total requests of primary and replica nodes		</td></tr>
<td>Metric alarm</td><td>	Total open connections		</td></tr>
<td>Metric alarm</td><td>	Total maximum connections		</td></tr>
</tbody></table>
