Log in to the [GAAP console](https://console.cloud.tencent.com/gaap), and select **Statistics** on the left sidebar. The **Statistics** page displays data in the following four dimensions: connection, connection group, listener, and origin server.

## Connection

You can view the connection statistics, as shown below:

- **Connection Type**: defaults to Single Connection. You can also select a connection group that has been created before.
- **Connection**: Select a connection of the **Access Management** or the connection group.
- **Data Type**: Select one or all data types (bandwidth, traffic, packet volume, concurrent connections, HTTP QPS, HTTPS QPS, latency, and packet loss rate).
- **Time Period**: Select a time period.
- **Time Granularity**: Select a time granularity. The maximum query time is 15 days if you select a 1-minute granularity, 31 days for a 5-minute granularity, 93 days for a 1-hour granularity and 186 days for a 1-day granularity.

![](https://qcloudimg.tencent-cloud.cn/raw/4d3f9eaea3e2ca9442ec8cfabf0ad73f.jpg)

## Connection Group

You can view the connection group statistics, as shown below:

- **Connection Group**: Select one or more connection groups.
- **Data Type**: Select one or all data types (bandwidth and traffic).
- **Time Period**: Select a time period.
- **Time Granularity**: Select a time granularity. The maximum query time is 15 days if you select a 1-minute granularity, 31 days for a 5-minute granularity, 93 days for a 1-hour granularity and 186 days for a 1-day granularity.

![](https://qcloudimg.tencent-cloud.cn/raw/fce7e20b2dcaa474095a117380f41e85.jpg)

## Listener

You can view the listener statistics, as shown below:

- **Connection/Connection Group**: Select a connection or connection group for the listener.
- **Listener**: Select a listener.
- **Data Type**: Select one or all data types (bandwidth, traffic, packet volume and concurrent connections).
- **Time Period**: Select a time period.
- **Time Granularity**: Select a time granularity. The maximum query time is 15 days if you select a 1-minute granularity, 31 days for a 5-minute granularity, 93 days for a 1-hour granularity and 186 days for a 1-day granularity.

![](https://qcloudimg.tencent-cloud.cn/raw/b1975214d1f82e89dcded5c4280d0bb9.jpg)

## Origin Server

You can view the statistics of the origin server’s health status, as shown below:

- **Connection/Connection Group**: Select a connection or connection group for the origin server.
- **Listener**: Select a listener for the origin server.
- **Origin**: Select an origin server.
- **Time Period**: Select a time period.
- **Time Granularity**: Select a time granularity. The maximum query time is 15 days if you select a 1-minute granularity, and 31 days for a 5-minute granularity.

![](https://qcloudimg.tencent-cloud.cn/raw/75ce6339c8d51048a066fd3df481a642.jpg)

## Exporting Data

Enter the **Statistics** page, and click the download icon to export data.
![](https://qcloudimg.tencent-cloud.cn/raw/7646c6fb333f613b5dc1059de73b9847.jpg)

## Configuring an Alarm Policy
Enter the [Statistics](https://console.cloud.tencent.com/gaap/data) page, and click **Configure Alarm** in the top right corner to configure an alarm policy. For more details, see [Access Cloud Monitoring](https://intl.cloud.tencent.com/document/product/608/17541).
