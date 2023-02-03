In the CSS console, you can manage domains and streams, configure transcoding, recording, and acceleration, as well as push streams (web) and monitor resources. 

## Prerequisites

- You have activated [CSS](https://cloud.tencent.com/product/css). 
- You have logged in to the [CSS console](https://console.cloud.tencent.com/live/livestat).

## Overview
Click **Overview** on the left sidebar to view data including the current downstream bandwidth, today’s downstream bandwidth, the current number of push channels, the number of concurrent connections, as well as bandwidth usage, traffic usage, and push channels trends in the last 30 days. You can change the granularity of the data. On the same page, you can also change the billing mode or click **Beginner's Guide** in the top-right corner to read instructions to get started with CSS.
![](https://qcloudimg.tencent-cloud.cn/raw/e8946c20fd1a4cad644cfbd4f637bb14.png)

### Today's Data

This section displays the downstream peak bandwidth, downstream traffic usage, the current number of push channels, and the number of concurrent connections of the day.
<table>
<thead><tr><th width="20%">Item</th><th width="80%">Description</th></tr></thead>
<tbody><tr>
<td>Current Downstream Bandwidth</td>
<td>The peak bandwidth consumed for acceleration by all playback domains.</td>
</tr>
<tr>
<td>Today's Downstream Traffic</td>
<td>The total traffic consumed for acceleration by all playback domains on the current day.</td>
</tr>
<tr>
<td>Current Push Channels</td>
<td>The number of current push channels.</td>
</tr>
<tr>
<td>Concurrent connections</td>
<td><li/>If the playback protocol is RTMP or FLV, **Concurrent Connections** indicates the number of online viewers. <li/>If the playback protocol is HLS, **Concurrent Connections** cannot be used as an indication of the number of online viewers.</td>
</tr>
</tbody></table>

### Usage trends

This section displays usage trends (**Bandwidth Trend**, **Traffic Trend**, and **Push Channels**) for today, yesterday, the last 7 days, and the last 30 days.

<table>
<thead><tr><th width="20%">Item</th><th width="80%">Description</th></tr></thead>
<tbody><tr>
<td>Bandwidth Trend</td>
<td>The sum of the peak bandwidth consumed for acceleration by all playback domains in the query period.</td>
</tr>
<tr>
<td>Traffic Trend</td>
<td>The total traffic consumed for acceleration by all playback domains in the query period.</td>
</tr>
<tr>
<td>Push Channels</td>
<td>The number of push channels under the selected domains in the query period.</td>
</tr>
</tbody></table>

#### Changing the granularity

You can click the drop-down list box next to **Granularity** to change the granularity of the usage trend data.
![](https://main.qcloudimg.com/raw/8582c16fca9bd3e4c2f0fcd78625cbb5.png)

### Billing details
- **Billing mode**
  This section shows your billing modes inside and outside the Chinese mainland. If you use the same billing mode for LEB and LEB, you can click **Price calculator** to estimate your cost.
- **Switching the billing mode**
  Click **Switch**, check the information in the pop-up window, and click **Confirm** to change the billing mode. For more information, see [Changing Billing Modes](https://intl.cloud.tencent.com/document/product/267/30411). If you want to use different billing modes for LEB and LVB, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
- **Viewing package usage**
  Click **Details** in the **Packages** area to go to the [Resource Package/Plugin Management](https://console.cloud.tencent.com/live/resources/package?type=traffic) page and view the usage, creation time, expiration time, and status of your traffic and transcoding packages.  
- **Buying packages**
  On the CSS package purchase page, click **Buy** in the **Packages** area to buy a package.
>? For more information, see [Pricing Overview](https://intl.cloud.tencent.com/document/product/267/2819).

### Get Started with LEB

Click **Start Now** in the **Get Started with LEB** area to read the instructions to quickly get started with LEB.