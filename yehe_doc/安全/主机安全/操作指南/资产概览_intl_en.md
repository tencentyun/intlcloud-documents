This document describes how to use Assets Dashboard.

## Overview
Assets Dashboard presents the data of your servers and 15 key asset fingerprint items in a visualized form to give you a picture of your server assets.

## Important Notes
Asset Dashboard is available to all Tencent Cloud users. The collected asset fingerprint items vary with different CWPP editions, so the data displayed in Assets Dashboard varies with the editions, as shown below.

| CWPP Edition | Supported Asset Types |
|---------|---------|
| CWPP Basic (free) | N/A |
| CWPP Pro | 10 items: Resource Monitoring, Accounts, Ports, Processes, Software Applications, Databases, Web Applications, Web Services, Web Frameworks, and Websites |
| CWPP Ultimate | 15 items: Resource Monitoring, Accounts, Ports, Processes, Software Applications, Databases, Web Applications, Web Services, Web Frameworks, Websites, JAR Archive Files, Startup Services, Scheduled Tasks, Environment Variables, and Kernel Modules |

<dx-alert infotype="explain" title="">
Asset fingerprint data is collected automatically every 8 hours (manual collection is supported).
</dx-alert>

## Operation Guide
1. Log in to the [CWPP console](https://console.intl.cloud.tencent.com/cwp).
2. Click **Assets Dashboard** on the left sidebar. The fields and operations related to the feature are described as follows.

### Assets Dashboard
The **Assets Dashboard** section displays the statistics of all assets and asset fingerprints.
![](https://qcloudimg.tencent-cloud.cn/raw/de78acd734a489e31338db2bf3e6580d.png)
### Server Overview and Trending
**Server Trend** shows the changes in the total number of servers, the number of online servers, the number of offline servers, and the number of risky servers in a line graph.
![](https://qcloudimg.tencent-cloud.cn/raw/d3bd77ea1d4fdd5d38097862bfe4aa19.png)
You can view the statistics for the past 7/14/30 days, or a custom period . The data generated 3 months ago is not displayed.
Click **Download** to export the daily data of the server for the selected date range.

### Top 5 Server Tags
The **Top 5 Server Tags** section displays the top 5 most used server tags in CWPP.
![](https://qcloudimg.tencent-cloud.cn/raw/1fa1753eb971f93cb767125af70dbf53.png)

### Resource Monitoring
The **Resource monitoring** section displays the distribution of system load, memory usage, disk usage, and the top 5 servers ranked by these dimensions.
![](https://qcloudimg.tencent-cloud.cn/raw/ef7262f38eada7c9f44247dca224cae3.png)

<dx-alert infotype="explain" title="">
The statistics of system load are only available for Linux servers (Windows servers are not supported).
</dx-alert>

### TOP 5 Asset Fingerprints
**TOP 5 Asset Fingerprints** displays the top 5 accounts, ports, processes, software applications, databases, Web applications, Web services, Web frameworks, and Web sites.
![](https://qcloudimg.tencent-cloud.cn/raw/4c41fc0e0012274de985770e06c250ee.png)



