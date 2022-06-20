Log in to the [GAAP console](https://console.cloud.tencent.com/gaap). Enter the **Statistics** page.

This page provides the following dimensions: Connection, connection group, listener, origin server, and domain name.

[](id:m1)
## Connection

You can view the connection statistics, as shown below:
- **Connection Type**: It defaults to single connection. You can also select a connection group that has been created before.
- **Connection**: Select a connection of the **Access Management** or of the connection group.
- **Data Type**: Select one or all data types (bandwidth, traffic, packet volume, concurrent connections, HTTP QPS, HTTPS QPS, latency, and packet loss rate).
- **Time Period**: Select a time period.
- **Time Granularity**: Select a time granularity. Supported options: 1 minute, 5 minutes, 1 hour, and 1 day.
  [ The maximum query time is 1 day if you select a 1-minute granularity, 3 days for a 5-minute granularity, 15 days for a 1-hour granularity and 186 days for a 1-day granularity. ]

![](https://qcloudimg.tencent-cloud.cn/raw/4d3f9eaea3e2ca9442ec8cfabf0ad73f.jpg)

[](id:m2)
## Connection Group

You can view the connection group statistics, as shown below:
- **Connection Group**: Select one or more connection groups.
- **Data Type**: Select one or all data types (bandwidth and traffic).
- **Time Period**: Select a time period.
- **Time Granularity**: Select a time granularity. Supported options: 1 minute, 5 minutes, 1 hour, and 1 day.
  [ The maximum query time is 1 day if you select a 1-minute granularity, 3 days for a 5-minute granularity, 15 days for a 1-hour granularity and 186 days for a 1-day granularity. ]

![](https://qcloudimg.tencent-cloud.cn/raw/fce7e20b2dcaa474095a117380f41e85.jpg)

[](id:m3)
## Listener

You can view the listener statistics, as shown below:
- **Connection/Connection Group**: Select a connection or connection group for the listener.
- **Listener**: Select a listener.
- **Data Type**: Select one or all data types (bandwidth, packet volume, concurrent connections).
- **Time Period**: Select a time period.
- **Time Granularity**: Select a time granularity. Supported options: 1 minute, 5 minutes, 1 hour, and 1 day.
  [ The maximum query time is 1 day if you select a 1-minute granularity, 3 days for a 5-minute granularity, 15 days for a 1-hour granularity and 186 days for a 1-day granularity. ]

![](https://qcloudimg.tencent-cloud.cn/raw/b1975214d1f82e89dcded5c4280d0bb9.jpg)

[](id:m4)
## Origin Server

You can view the statistics of the bound origin server when it is healthy.
- **Connection/Connection Group**: Select a connection or connection group for the origin server.
- **Listener**: Select a listener for the origin server.
- **Origin**: Select an origin server.
- **Time Period**: Select a time period.
- **Time Granularity**: Select a time granularity. Supported options: 1 minute and 5 minutes.
  [ The maximum query time is 1 day if you select a 1-minute granularity, and 31 days for a 5-minute granularity. ]

![](https://qcloudimg.tencent-cloud.cn/raw/75ce6339c8d51048a066fd3df481a642.jpg)

[](id:m5)
## Domain Name

You can view the statistics of the domain names in the HTTP/HTTPS listener configuration, as shown below:

- **Region**: Select Chinese mainland or Outside the Chinese mainland.
- **Domains**: Select one or multiple domain names.
- **HTTP Protocol**: Select one or all HTTP protocols.
- **Data Type**: Select one or all data types (requests, status code and top 10 URLs).
- **Time Period**: Select a time period.
- **Time Granularity**: Select a time granularity. Supported options: 1 minute, 5 minutes, 1 hour, and 1 day.
  [ The maximum query time is 1 day if you select a 1-minute granularity, 3 days for a 5-minute granularity, 15 days for a 1-hour granularity and 186 days for a 1-day granularity. ]

![](https://qcloudimg.tencent-cloud.cn/raw/6b58ba9c9a60b3cb5e72ceac3bd0b67f.png)



## Exporting Data

Enter the **Statistics** page, and click the download icon to export data.
![](https://qcloudimg.tencent-cloud.cn/raw/7646c6fb333f613b5dc1059de73b9847.jpg)



## Configuring an Alarm Policy

Enter the [Statistics](https://console.cloud.tencent.com/gaap/data) page, and click **Configure Alarm** in the top right corner to configure an alarm policy. For more details, see [Access Cloud Monitoring](https://intl.cloud.tencent.com/document/product/608/17541).

![]()
