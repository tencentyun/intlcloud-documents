
This document describes how to view monitoring information such as server fleets, game server queues, and instances.
## Prerequisites

You have [created a server fleet](https://intl.cloud.tencent.com/document/product/1055/36675).

## Directions

1. Log in to the [GSE console](https://console.cloud.tencent.com/gse/asset) and click **Fleet** on the left sidebar.
2. Click the server fleet ID to enter the server fleet details page.
![](https://main.qcloudimg.com/raw/42c96a345b41ae2545c10534cf8aee1e.png)
3. On the server fleet details page, click **View Monitoring** in the top-right corner to enter the monitoring panel.
![](https://main.qcloudimg.com/raw/99e7932d115505db65079bd78ad71335.png)
4. Click **Dashboard** > **Dashboard List** > **Create Dashboard** > **Create Chart** to create a monitoring chart.
5. Select the namespace and metrics in the **Metric** to define data to be displayed on the monitoring chart. You can select **Fleet**, **GameServerSessionQueue** or **Instance** as the namespace as needed.
![](https://main.qcloudimg.com/raw/40bfdf27116e1b8ebf6a16a33f840116.png)


 - Description of monitoring metrics available for **Game Server Elastic-scaling - Fleet**:

<table>
<thead>
<tr>
<th width="30%">Monitoring Metric</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Activating Game Server Sessions (Count)</td>
<td>Number of game server sessions in ACTIVATING status (a session in this status is being launched)</td>
</tr>
<tr>
<td>Active Game Server Sessions (Count)</td>
<td>Number of game server sessions in ACTIVE status (a session in this status can host players and is hosting zero to multiple players)</td>
</tr>
<tr>
<td>Active Instances (Count)</td>
<td>Number of instances in ACTIVE status (an instance in this status is running active server processes)</td>
</tr>
<tr>
<td>Idle Instances (Count)</td>
<td>Number of active instances that are not hosting any game server sessions</td>
</tr>
<tr>
<td>Percent Idle Instances (%)</td>
<td>Percentage of active instances in idle status</td>
</tr>
<tr>
<td>Max Instances (Count)</td>
<td>Maximum number of instances allowed by the server fleet</td>
</tr>
<tr>
<td>Min Instances (Count)</td>
<td>Minimum number of instances allowed by the server fleet</td>
</tr>
<tr>
<td>Desired Instances (Count)</td>
<td>Target number of active instances that can be maintained by the server fleet</td>
</tr>
<tr>
<td>Healthy Server Processes (Count)</td>
<td>Number of active server processes that are running normally</td>
</tr>
<tr>
<td>Server Process Abnormal Terminations (Count)</td>
<td>Number of server processes that have been closed due to exceptions since the last report</td>
</tr>
<tr>
<td>Server Process Activations (Count)</td>
<td>Number of server processes that have successfully switched from the ACTIVATING status to ACTIVE status since the last report</td>
</tr>
<tr>
<td>Server Process Terminations (Count)</td>
<td>Number of server processes that have been closed since the last report</td>
</tr>
<tr>
<td>Active Server Process (Count)</td>
<td>Number of server processes in ACTIVE status (a process in this status is running and can host game server sessions)</td>
</tr>
<tr>
<td>Percent Healthy Server Processes (%)</td>
<td>Percentage of all active server processes that are running normally</td>
</tr>
<tr>
<td>Available Game Server Sessions (Count)</td>
<td>Number of idle game server session slots in the active server processes that are running normally</td>
</tr>
<tr>
<td>Percent Available Game Server Session (%)</td>
<td>Percentage of idle game server session slots in all active server processes (no matter whether they are running normally or not)</td>
</tr>
<tr>
<td>Active Player Sessions (Count)</td>
<td>Player sessions in ACTIVE (the players have connected to active game server sessions) or RESERVED status (the players have been assigned with slots in the game server session but have not connected)</td>
</tr>
<tr>
<td>Player Session Activations (Count)</td>
<td>Number of player sessions that have switched from the RESERVED status to ACTIVE status since the last report (within a certain period of time)</td>
</tr>
<tr>
<td>No Instances (Count)</td>
<td>Number of instances that fail to be purchased</td>
</tr>
</tbody></table>

![](https://main.qcloudimg.com/raw/610777f8db2c951e732fc3ac0b181633.png)

 - Description of available monitoring metrics for **Game Server Elastic-scaling - GameServerSessionQueue**:

<table>
<thead>
<tr>
<th width="25%">Monitoring Metric</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Average Wait Time (s)</td>
<td>Average execution wait time for game server session placement requests in PENDING status in game server queue</td>
</tr>
<tr>
<td>First Choice Not Viable (Count)</td>
<td>Number of game server sessions that are placed in to a fleet other than the preferred one as the preferred one is nonviable (for example, it is a Spot fleet with a high interruption rate)</td>
</tr>
<tr>
<td>First Choice Out of Capacity (Count)</td>
<td>Number of game server sessions that are placed in to a fleet other than the preferred one as the preferred fleet does not have available resources</td>
</tr>
<tr>
<td>Lowest Latency Placement (Count)</td>
<td>Number of game server sessions that are placed into the region with the lowest latency for players</td>
</tr>
<tr>
<td>Placements Canceled (Count)</td>
<td>Number of game server session placement requests that have been canceled before timeout since the last report</td>
</tr>
<tr>
<td>Placements Failed (Count)</td>
<td>Number of failed game server session placement requests since the last report</td>
</tr>
<tr>
<td>Placements Started (Count)</td>
<td>Number of new game server session placement requests that have been added to the queue since the last report</td>
</tr>
<tr>
<td>Placements Succeeded (Count)</td>
<td>Number of successful game server session placement requests since the last report</td>
</tr>
<tr>
<td>Placements Timed Out (Count)</td>
<td>Number of game server session placement requests that are not executed due to the queue timeout since the last report</td>
</tr>
<tr>
<td>Queue Depth (Count)</td>
<td>Number of game server session placement requests in PENDING status in queue</td>
</tr>
<tr>
<td>Placement In ap-shanghai (Count)</td>
<td>Number of game server sessions that have been successfully placed in a server fleet in Shanghai since the last report</td>
</tr>
<tr>
<td>Placement In na-siliconvalley (Count)</td>
<td>Number of game server sessions that have been successfully placed in a server fleet in Silicon Valley since the last report</td>
</tr>
<tr>
<td>Placement In na-ashburn (Count)</td>
<td>Number of game server sessions that have been successfully placed in a server fleet in Virginia since the last report</td>
</tr>
<tr>
<td>Placement In ap-beijing (Count)</td>
<td>Number of game server sessions that have been successfully placed in a server fleet in Beijing since the last report</td>
</tr>
<tr>
<td>Placement In ap-guangzhou (Count)</td>
<td>Number of game server sessions that have been successfully placed in a server fleet in Guangzhou since the last report</td>
</tr>
<tr>
<td>Placement In ap-hongkong (Count)</td>
<td>Number of game server sessions that have been successfully placed in a server fleet in Hong Kong since the last report</td>
</tr>
<tr>
<td>Placement In ap-mumbai (Count)</td>
<td>Number of game server sessions that have been successfully placed in a server fleet in Mumbai since the last report</td>
</tr>
<tr>
<td>Placement In ap-seoul (Count)</td>
<td>Number of game server sessions that have been successfully placed in a server fleet in Seoul since the last report</td>
</tr>
<tr>
<td>Placement In ap-tokyo (Count)</td>
<td>Number of game server sessions that have been successfully placed in a server fleet in Tokyo since the last report</td>
</tr>
<tr>
<td>Placement In eu-frankfurt (Count)</td>
<td>Number of game server sessions that have been successfully placed in a server fleet in Frankfurt since the last report</td>
</tr>
<tr>
<td>Placement In ap-singapore (Count)</td>
<td>Number of game server sessions that have been successfully placed in a server fleet in Singapore since the last report</td>
</tr>
<tr>
<td>Placement In ap-bangkok (Count)</td>
<td>Number of game server sessions that have been successfully placed in a server fleet in Bangkok since the last report</td>
</tr>
</tbody></table>

![](https://main.qcloudimg.com/raw/036fef271e25a599a9d50ad769f10614.png)



 - Description of available monitoring metrics for **Game Server Elastic-scaling - Instance**:

<table>
<thead>
<tr>
<th width="20%">Monitoring Metric</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Public Outbound Traffic (MBytes)</td>
<td>Average outbound traffic per second of public ENI</td>
</tr>
<tr>
<td>Private Inbound Packets (Count/s)</td>
<td>Average number of inbound packets per second of private ENI</td>
</tr>
<tr>
<td>Private Inbound Bandwidth (MBit/s)</td>
<td>Average inbound traffic per second of private ENI</td>
</tr>
<tr>
<td>Private Outbound Packets (Count/s)</td>
<td>Average number of outbound packets per second of private ENI</td>
</tr>
<tr>
<td>Private Outbound Packets (Count/s)</td>
<td>Average outbound traffic per second of private ENI</td>
</tr>
<tr>
<td>Memory Utilization (%)</td>
<td>Percentage of the memory actually used, excluding the memory used by buffers and system caches</td>
</tr>
<tr>
<td>Memory Usage (MBytes)</td>
<td>Amount of the memory actually used, excluding the memory used by buffers and system caches</td>
</tr>
<tr>
<td>CPU Utilization</td>
<td>Real time CPU utilization during instance execution</td>
</tr>
<tr>
<td>TCP Connections (Count)</td>
<td>Number of TCP connections in ESTABLISHED status</td>
</tr>
<tr>
<td>Public Inbound Packets (Count/s)</td>
<td>Average number of inbound packets per second of public ENI</td>
</tr>
<tr>
<td>Public Outbound Packets (Count/s)</td>
<td>Average number of outbound packets per second of public ENI</td>
</tr>
<tr>
<td>Public Inbound Bandwidth (MiBit/s)</td>
<td>Average inbound traffic per second of public ENI</td>
</tr>
<tr>
<td>Public Outbound Bandwidth (MiBit/s)</td>
<td>Average outbound traffic per second of public ENI</td>
</tr>
<tr>
<td>CPU Average Load</td>
<td>Average number of tasks that are using and waiting to use the CPU per minute</td>
</tr>
</tbody></table>

![](https://main.qcloudimg.com/raw/08cae6d15fca6e92cf20ec14c567eb75.png)

6. Select the region of the object to be monitored in **Region** on the right, and the list of monitoring object names will be displayed for you to select.
![](https://main.qcloudimg.com/raw/ee27d25d7e8e91e2713b1cd475aa0149.png)
7. You can click **Chart Name** to rename the chart and click **OK** to create a monitoring chart as needed.
![](https://main.qcloudimg.com/raw/d486150aca8a7ae1afb716748628a4ca.png)
8. You can also copy, edit, export and delete the chart later when needed.
![](https://main.qcloudimg.com/raw/59b55a60695cd9652db14a9fd016f6f3.png)

