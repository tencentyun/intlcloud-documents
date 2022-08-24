## Feature Overview

CDN speed test uses a scheduled task configured in Cloud Automated Testing (CAT) to access the target resource from globally distributed real terminal nodes. This simulates the access experience of real users to test and monitor the CDN performance. It works in a zero-code non-intrusive manner to help you continuously monitor the accuracy, quality, and stability of CDN resource download in all regions.

## Use Cases

### CDN performance prediction

Before CDN service selection or migration, you can quickly predict the performance in all or specified regions after connection to CDN without modifying the production network environment. Then, you can design CDN optimization or migration plans and policies accordingly.
	

### CDN performance monitoring

Based on regular testing and alarming, CDN speed test monitors availability problems caused by the unavailability of the origin or CDN service. In addition, it also collects detailed end-to-end phase-specific time statistics to help you continuously monitor the CDN service performance, such as time taken for DNS, TCP connection establishment, CDN server response, first packet arrival, and entire file loading.
	

### Resource update verification

After a CDN resource is updated, CDN speed test can actively test and compare the resource MD5 value to check whether the resource cached at each access point is updated promptly. This prevents resource update failures and avoids a poor user experience and business losses.
		
		

## Configuration Guide

### Step 1. Enable the CDN speed test feature

Log in to the [CDN console](https://console.cloud.tencent.com/cdn/plugins) and find the CDN speed test feature section. When activating the service for the first time, you need to create a preset service role and grant CDN relevant permissions. After successful authorization, toggle on **CDN Speed Test**.
![](https://qcloudimg.tencent-cloud.cn/raw/8d3a2bb9f278aa7e35cb65a33079de8d.png)

### Step 2. Create a monitoring task

1. Go to the task list page and click **Create Task**.
2. From all available URLs, select the URLs for which to simulate user access requests (up to five URLs can be monitored at the same time), select the test points of ISPs in the regions where you want to simulate access requests, and enable the test task.

![]()

### Step 3. Analyze the performance in various dimensions

After 10–20 minutes, the test data will be returned from test points around the world. You can view various core metrics of each resource on the performance dashboard. In the middle of the page, you can analyze specified metrics and lines and view the performance differences between regions, ISPs, and lines.
![]()

### Step 4. Analyze details and troubleshoot failures

Click a task to view complete task logs, including time taken in each phase, hop path at the network layer, and file MD5 values. For element download and network problems, you can create dedicated page performance or network quality tasks to get more specific metric data.
![]()


