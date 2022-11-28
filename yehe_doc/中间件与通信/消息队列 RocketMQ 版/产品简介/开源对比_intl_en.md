

The performance comparison between TDMQ for RocketMQ and Apache RocketMQ is detailed below:
<table>
<tr>
<th>Feature Type</th>
<th>Feature</th>
<th>TDMQ for RocketMQ</th>
<th>Apache RocketMQ</th>
</tr>
<tr>
<td  rowspan="3">Basic features</td>
<tr>
<td>Scheduled message</td>
<td>The scheduled time is accurate down to the second and can be customized.</td>
<td>You can only specify the delay level.</td>
</tr>
<tr>
<td>Visual management</td>
<td>Visual management for clusters, topics, and groups is supported. You can view the details of subscriptions and consumer status.</td>
<td>Visual management is supported but is less user-friendly. The console doesn’t distinguish between topic types.</td>
</tr>
</tr>
<tr>
<td  rowspan="4">Availability</td>
<tr>
<td>Elastic scaling</td>
<td>You don’t need to manually deploy, configure, or scale up underlying computing resources because operations such as node registration are automatically performed in a visual manner. You can expand the number of nodes horizontally, increase the disk capacity, and upgrade the configurations of a single node vertically as needed at any time.</td>
<td>A self-built Ops team is required, and operations are performed in a less automatic or visualized manner.</td>
</tr>
<tr>
<td>High reliability</td>
<td>With three data replicas, the server can be automatically restarted in seconds after the downtime, without affecting the message capacity and data.</td>
<td>Data can be replicated in sync or async mode. You need to design the deployment scheme and related parameters. The primary sync schemes won’t be automatically used after the failover.</td>
</tr>
<tr>
<td>Cross-AZ high-availability deployment</td>
<td>This feature is supported to avoid losses caused by data center-level failures.</td>
<td>This feature is supported, but it is time-consuming for you to design the deployment schemes and parameters.</td>
</tr>
</tr>
<tr>
<td  rowspan="3">Observability</td>
<tr>
<td>Resource dashboard</td>
<td>You can monitor core metrics at a fine granularity and view production and consumption details.</td>
<td>This feature is supported but with fewer monitoring metrics.</td>
</tr>
<tr>
<td>Alarming</td>
<td>With the capabilities provided by Cloud Monitor, alarms will be triggered in case of message heap or delayed message sending/receiving.</td>
<td>Not supported</td>
</tr>
</tr>
<tr>
<td  rowspan="3">Security management and control</td>
<tr>
<td>Tenant namespace isolation</td>
<td>You can implement this feature in the console in a visual manner.</td>
<td>This feature is not supported. Namespaces cannot be truly isolated due to bugs.</td>
</tr>
<tr>
<td>Root account and sub-account management</td>
<td>Supports authorization between Tencent Cloud CAM root accounts and sub-accounts and between enterprise accounts.</td>
<td>Not supported</td>
</tr>
</tr>
<tr>
<td>Migration tool</td>
<td>Tool for migrating from Apache RocketMQ</td>
<td>You can easily migrate from Apache RocketMQ to TDMQ for RocketMQ by using scripts.</td>
<td>-</td>
</tr>
</table>
</escape>
