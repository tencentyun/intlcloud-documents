
## Overview

TKE Serverless provides out-of-the-box event dashboards and can automatically configure the event overview dashboard and aggregated exception search dashboard for the cluster with event storage enabled. With user-defined filters and built-in CLS global event search, TKE Serverless makes it convenient for you to comprehensively observe, find, analyze, and locate problems in the TKE console.


## Feature Description

Three dashboards are configured in **Event Search**, namely **Event Overview**, **Aggregated Exception Search**, and **Global Search**. Follow the steps below to enter the **Event Search** page and use the features:
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. Enable **Event Storage**. For more information, see [Event Storage](https://intl.cloud.tencent.com/document/product/457/39121).
3. On the left sidebar, select **Log Management** > **Event Search**.


### Event overview

On the **Event Overview** tab, you can filter events based on dimensions such as time, namespace, level, reason, resource type, and resource object, view the aggregated statistics of the core event, and display data comparison within a period. Specifically, you can view dashboards of the total number of events and distribution, node exceptions, Pod OOM errors, and important event trends as well as the top exception list.


You can view more statistics on this page as shown below:
- The total number of events, level distribution, causes of exceptions, and object distribution are as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/23dc6c35e6351ea6128ec2d5a1e65f01.png)
- The aggregated information of common events is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/4160f9cc3e97fb116cb3ece3c7630270.png)
- Event trends and the top exception list are as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/b2ab56ba5943c2f1c88ab9c5179f06a0.png)



### Aggregated exception search
On the **Aggregated Exception Search** tab, you can set filters to view the cause and object distribution trends of exceptions over a specified period of time. You can also search for exceptions in the list below the trend diagrams to quickly locate problems as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/eb27a74576206f3adcd843b3af1e5965.png)

### Global search
The global search dashboard with the built-in CLS search and analysis page makes it convenient for you to quickly search for all events in the TKE console as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/73f7cd0a5ceee847a970d19edecdbba3.png)

### Configuring alarm by dashboard
You can configure alarms based on the preset dashboards as instructed below, so that alarms will be triggered when the configured conditions are reached:


1. Click **<img src="https://main.qcloudimg.com/raw/77e0007d25c9724e5b2f05ab3ff8f95a.png" width="2.5%">** on the right of the target dashboard and select **Quickly Add Alarm** from the drop-down list as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/8414be6f130252255d43bdc3dc2facfe.png)
2. For more information on how to configure alarm policies, see [Configuring Alarm Policies](https://intl.cloud.tencent.com/document/product/614/39574).


