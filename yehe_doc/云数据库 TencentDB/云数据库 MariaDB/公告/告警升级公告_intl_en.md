## Background
TencentDB for MariaDB upgraded the monitoring items for server and component services on April 1, 2021 by replacing the legacy alarm policy type and modifying hundreds of monitoring and alarm metrics. You can configure alarm policies of the [MariaDB](https://intl.cloud.tencent.com/document/product/248/40015) type in the Cloud Monitor console.

The original MariaDB (legacy) policy type will no longer be maintained in the future, and the backend will gradually migrate all the MariaDB policies you previously configured to the new alarm policy type. We recommend you migrate the alarms on your own, so that you can try out the new alarm feature earlier. Subsequently, please configure new alarm policies under the new alarm policy type.

#### Comparison of the legacy and new alarm policy types
| Policy Type | Metric Coverage | Support and Maintenance |
| ------------- | -------------------------- | ----------------------- |
| MariaDB (legacy) | 22 metrics | You can continue to use this policy type, but it will no longer be maintained or updated, and your instances will be automatically migrated to the new policy type gradually. |
| MariaDB | 37 metrics | This policy type was released on April 1, 2021 with ongoing maintenance available. |

>!
>- The MariaDB policy type will cover all metrics of the original MariaDB (legacy) policy type. For more information, please see [Comparison Table of New and Legacy Metrics](#jump).
>- For the new alarm policies, please see [New Metric Description](#jump2).

## Alarm Policy Migration
After the MariaDB (legacy) policy type is deactivated, the system will automatically migrate previously configured alarm policies to the new MariaDB policy type on the backend.
>?Alarms may not be automatically migrated to the new alarm policy type by the system for certain instances or users. If this is the case for you, we will notify you through Message Center, email, or SMS. Then, please follow the manual migration steps below to manually migrate the alarms.

#### Manual migration steps
1. Sort out exiting alarm metrics and policies.
  1. Log in to the [Cloud Monitor console](https://console.cloud.tencent.com/monitor/alarm2/policy), select **Alarm Configuration** > **Alarm Policy** on the left sidebar, and click **Advanced Filter**.
  2. On the pop-up page, select the alarm policy type corresponding to **MariaDB (legacy)** in **Policy Type**, query alarm policies in this category, and download the previously configured alarm policies of the original **MariaDB (legacy)** policy type.
![](https://main.qcloudimg.com/raw/ed7a4d614743d251b63c83e24714735a.png)
2. Configure new alarm policies.
  1. On the **[Alarm Policy](https://console.cloud.tencent.com/monitor/alarm2/policy)** page, click **Create**.
  2. On the **Create Alarm Policy** page, select **MariaDB** for **Policy Type** and configure alarms according to the policies downloaded in step 1. For the configuration method, please see [Creating Alarm Policy](https://intl.cloud.tencent.com/document/product/248/38916).
3. Verify whether the MariaDB alarm policies are enabled and can successfully trigger alarms.
Set a minimum trigger threshold in **Metric alarm** on the **Create Alarm Policy** page, choose to set a **recipient** or **recipient group**, and select the notification channel (email or SMS) to test a policy. For example, you can configure an alarm policy for the CPU utilization metric that triggers an alarm once per minute when the threshold is greater than or equal to 1% for one statistical period of one minute.
4. After the new policy type is verified, delete the alarm policies previously configured under the original MariaDB (legacy) policy type.
On the **[Alarm Policy](https://console.cloud.tencent.com/monitor/alarm2/policy)** page, filter alarm policies by the "MariaDB (legacy)" policy type and delete the filtered policies according to the policy list downloaded in step 1.
If you encounter any issues during the migration, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

## [Comparison Table of New and Legacy Metrics](id:jump)
<table>
<thead><tr><th><strong>Original Policy Type</strong></th><th><strong>Metric/Event Alarm</strong></th><th><strong>Original Metric/Event Alarm Name</strong></th><th><strong>New Policy Type</strong></th><th><strong>New Metric/Event Alarm Name</strong></th></tr></thead>
<tbody><tr>
<td rowspan="22">TencentDB for MariaDB (legacy)</td>
<td>Metric alarm</td><td>CPU utilization	</td>
<td>MariaDB - instance summary</td><td>CPU utilization		</tr>
<tr>
<td>Metric alarm</td><td>Primary/Replica switch	</td>
<td>MariaDB - instance summary</td><td>Number of primary/replica switches		</tr>
<tr>
<td>Metric alarm</td><td>	Available disk space	</td>
<td>MariaDB - instance summary</td><td>	Available data disk space		</tr>
<tr>
<td>Metric alarm</td><td>	Log disk space	</td>
<td>MariaDB - instance summary</td><td>	Minimum remaining binlog disk space		</tr>
<tr>
<td>Metric alarm</td><td>	Query count (SELECT)	</td>
<td>MariaDB - instance summary</td><td>	Aggregated number of SELECT requests		</tr>
<tr>
<td>Metric alarm</td><td>	Slow query count	</td>
<td>MariaDB - instance summary</td><td>	Slow query count		</tr>
<tr>
<td>Metric alarm</td><td>	Update count (UPDATE)	</td>
<td>MariaDB - instance summary</td><td>	Number of UPDATE requests		</tr>
<tr>
<td>Metric alarm</td><td>	Insertion count (INSERT)	</td>
<td>MariaDB - instance summary</td><td>	Number of INSERT requests		</tr>
<tr>
<td>Metric alarm</td><td>	Deletion count (DELETE)	</td>
<td>MariaDB - instance summary</td><td>	Number of DELETE requests		</tr>
<tr>
<td>Metric alarm</td><td>	Available memory size	</td>
<td>MariaDB - instance summary</td><td>	Available cache space		</tr>
<tr>
<td>Metric alarm</td><td>	Disk IOPS	</td>
<td>MariaDB - instance summary</td><td>	IO utilization		</tr>
<tr>
<td>Metric alarm</td><td>	Number of active connections	</td>
<td>MariaDB - instance summary</td><td>	Aggregated number of active threads		</tr>
<tr>
<td>Metric alarm</td><td>	Connection utilization	</td>
<td>MariaDB - instance summary</td><td>	Maximum database connection utilization		</tr>
<tr>
<td>Metric alarm</td><td>	Disk utilization	</td>
<td>MariaDB - instance summary</td><td>	Data disk space utilization		</tr>
<tr>
<td>Metric alarm</td><td>	Replacement count	</td>
<td>MariaDB - instance summary</td><td>	Number of REPLACE_SELECT requests		</tr>
<tr>
<td>Metric alarm</td><td>	Number of InnoDB disk reads	</td>
<td>MariaDB - instance summary</td><td>	Aggregated number of InnoDB disk reads		</tr>
<tr>
<td>Metric alarm</td><td>	Number of InnoDB buffer pool reads	</td>
<td>MariaDB - instance summary</td><td>	Aggregated number of InnoDB buffer pool reads		</tr>
<tr>
<td>Metric alarm</td><td>	Number of InnoDB buffer pool read-aheads	</td>
<td>MariaDB - instance summary</td><td>	Aggregated number of InnoDB buffer pool read-aheads		</tr>
<tr>
<td>Metric alarm</td><td>	Number of deleted InnoDB rows	</td>
<td>MariaDB - instance summary</td><td>	Number of deleted InnoDB rows		</tr>
<tr>
<td>Metric alarm</td><td>	Number of inserted InnoDB rows	</td>
<td>MariaDB - instance summary</td><td>	Number of inserted InnoDB rows		</tr>
<tr>
<td>Metric alarm</td><td>	Number of updated InnoDB rows	</td>
<td>MariaDB - instance summary</td><td>	Number of updated InnoDB rows		</tr>
<tr>
<td>Metric alarm</td><td>	Used log disk space	</td>
<td>MariaDB - instance summary</td><td>	Used binlog disk space		</tr>
</tbody></table>

## [New Metric Description](id:jump2)
<table>
<thead><tr><th><strong>Policy Type</strong></th><th><strong>Metric/Event Alarm</strong></th><th><strong>Metric/Event Alarm Name</strong></th></tr></thead>
<tbody><tr>
<td rowspan="30">TencentDB for MariaDB</td>
<td>Metric alarm</td><td>	Aggregated number of read InnoDB rows		</td></tr>
<td>Metric alarm</td><td>	Minimum replica delay		</td></tr>
<td>Metric alarm</td><td>	Cache hit rate		</td></tr>
<td>Metric alarm</td><td>	Number of REPLACE requests		</td></tr>
<td>Metric alarm</td><td>	Number of requests lasting for less than 5 ms		</td></tr>
<td>Metric alarm</td><td>	Number of requests lasting for 5–20 ms		</td></tr>
<td>Metric alarm</td><td>	Number of requests lasting for 21–30 ms		</td></tr>
<td>Metric alarm</td><td>	Number of requests lasting for more than 30 ms		</td></tr>
<td>Metric alarm</td><td>	Total number of SQL requests		</td></tr>
<td>Metric alarm</td><td>	Number of SQL errors		</td></tr>
<td>Metric alarm</td><td>Number of SQL successes</td></tr>
<td>Metric alarm</td><td>	Total number of connections to clients		</td></tr>
<td>Metric alarm</td><td>	Aggregated number of requests to primary/replica nodes		</td></tr>
<td>Metric alarm</td><td>	Aggregated number of active connections		</td></tr>
<td>Metric alarm</td><td>	Aggregated maximum number of connections		</td></tr>
</tbody></table>
