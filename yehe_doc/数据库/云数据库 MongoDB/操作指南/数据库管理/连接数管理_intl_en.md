You can view the client connection information of the current database in the TencentDB for MongoDB console, including the IPs and number of connections. In this way, you can adjust its configuration in real time to meet your growing business needs. 

## Background
TencentDB for MongoDB records the IPs of clients connected to the current instance and the number of connections. When there is a large number of concurrent application requests, if the configured upper limit of connections is insufficient, the current database specification cannot sustain such requests. In this case, you can directly increase the upper limit in the console.

## Version Description
Currently, TencentDB for MongoDB 4.2, 4.0, 3.6, and 3.2 support connection management.

## Notes
- The system records the IPs of clients connected to the current instance and the number of connections. You can choose to manually release connection requests.
- If the number of connections reaches or exceeds 80% of the upper limit and affects the establishment of new connections, you can click **Increase Connections** in the console to increase the maximum number of connections to 150% of the original limit for the next 6 hours.
- If the problem persists, contact the aftersales service or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

## Prerequisites
- You have [applied for a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551).
- The TencentDB for MongoDB replica set or sharded instance is in **Running** status.

## Directions
### Viewing the number of connections
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. Click the target instance ID to enter the **Instance Details** page.
6. Select the **Database Management** > **Manage Connection** tab.
7. View all client connection statistics of the current database.
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Real-Time connections</td><td>Number of all connections to the current database.</td></tr>
<tr>
<td>Connection percentage</td><td>Percentage of all client connections to the current database to the maximum number of connections.</td></tr>
<tr>
<td>Maximum connections</td><td>Upper limit of the number of connections.</td></tr>
<tr>
<td>Remaining</td><td>The remaining usage duration of the increased upper limit.</td></tr>
<tr>
<td>Client IP</td><td>IP of a client connected to the database.</td></tr>
<tr>
<td>Connections</td><td>Number of connections.</td></tr>
</tbody></table>

### Increasing upper limit
1. On the **Manage Connection** tab, click **Increase Connections**.
2. In the **Note** window, confirm the notes and click **OK**.
> ?After the number of connections is increased, the connection limit will be raised to 20,000. If the service is affected, please check it out as soon as possible during that time. Click OK to start execution.

## Related APIs
| API                   | Description                                                      |
| ------------------------- | ------------------------------------------------------------ |
| DescribeClientConnections | [Queries the client connection information of instance](https://intl.cloud.tencent.com/document/product/240/34703) |

