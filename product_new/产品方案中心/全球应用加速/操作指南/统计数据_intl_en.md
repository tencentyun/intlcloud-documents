You can view the statistics of a connection under a specified project and its corresponding listener’s statistics on the “Overview” and “Monitor” pages.
## Overview
### Selecting a connection
Log into the [Global Application Acceleration Console](https://console.cloud.tencent.com/gaap). Click **Statistics**>**Overview**. On the **Overview** page, you can select the connection of any project to view the statistics.
![](https://main.qcloudimg.com/raw/ee8855b279a91831d35c09f12633b4c0.png)
<span id ="Selecting a Statistical Period">
### Selecting a statistical period</span>
Five common statistical periods are available: Today, Yesterday, Last 7 days, Last 15 days, and Last 30 days. You can also customize a specific start and end date, as shown in the following figure:
![](https://main.qcloudimg.com/raw/33c0e700386d4080509118db2cbc6b6a.png)
<span id="Selecting a Data Type"></span>
### Selecting a data type
Supported connection data types are: bandwidth (outbound bandwidth and inbound bandwidth), packet volume (outbound packet volume and inbound packet volume), delay, packet loss rate, and concurrent connections.
**Outbound bandwidth** refers to the bandwidth from the origin server to the client. **Inbound bandwidth** refers to the bandwidth from the client to the origin server.

### Data Comparison
You can select a data type and check different connections for comparison.
![](https://main.qcloudimg.com/raw/6adaaa7336bbc7479b8c5df7c21c3782.png)

## Monitoring Connection
### Selecting a connection
Log into the [Global Application Acceleration Console](https://console.cloud.tencent.com/gaap). Click **Statistics**>**Monitor**. On the **Monitor** page, select the project, a single connection or a connection group, and the connection name. By default, the given statistics are combined statistics on all the listeners under the specified connection. You can select different connections as shown by the red box in the following figure:
![](https://main.qcloudimg.com/raw/b957ff2db257f55cc4369d7c9f08f88f.png)

### Selecting a listener
On the **Statistics** page, select a listener under the specified connection of the specified project to view its statistics. You can select different listeners as shown by the red box in the following figure:
![](https://main.qcloudimg.com/raw/849c21e874f488c623acc245c928a6c4.png)

### Selecting a statistical period
See the previous [Selecting a statistical period](#Selecting a statistical period) section.

### Supported Items
See the previous [Selecting a data type](#Selecting a data type) section.

### Data Comparison
You can select historical data to compare it to current data. The historical data must have the same statistical period as the current data.
![](https://main.qcloudimg.com/raw/a68dcaf4e4735f48304fffb1e045ab67.png)
