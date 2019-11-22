
## Overview
LogListener is a log collection client provided by CLS. You can install and deploy it to easily and quickly access CLS without modifying the run logic of applications. It is a non-intrusive collection method for application services.

The procedures for collecting logs with LogListener are shown in the following figure:

![](https://main.qcloudimg.com/raw/7efda83d58a3eea79377f0ce134bc90a.png)

## Procedure Description

1. Download the latest version of [LogListener](https://main.qcloudimg.com/raw/8656fcadd12ab9689674df09b510b52b/loglistener.2.2.2.tar.gz).
2. [Install and deploy LogListener](https://intl.cloud.tencent.com/document/product/614/17414) on the destination server. Upon successful installation, it automatically launches and maintains a heartbeat connection with the backend of CLS.
3. Go to the [CLS Console](https://console.cloud.tencent.com/cls), create a [server group](https://intl.cloud.tencent.com/document/product/614/17412), and add the server IP.
4. Go to the **Collection Configuration** page of the log topic, enter the log path to determine the data source, and bind the server group. For a detailed operation sample, please see the [Collection of Full Text in a Single Line](https://intl.cloud.tencent.com/document/product/614/32287) document.
5. Go to the **Index Configuration** page of the log topic, configure the full text or key-value index, and enable the index. For a detailed operation sample, please see the [Collection of Full Text in a Single Line](https://intl.cloud.tencent.com/document/product/614/32287) document.

By now, LogListener monitors the log files that meet the rules according to the collection configuration of the log topics. Users may view the collected log data via log search.

