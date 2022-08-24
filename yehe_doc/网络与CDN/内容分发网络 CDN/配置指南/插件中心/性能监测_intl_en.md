## Feature Overview

The performance monitoring feature is a one-stop frontend monitoring solution designed for web and mini program monitoring. You only need to install its SDK to your project and complete simple configuration, and then it will take care of the user page quality in an all-around manner, truly enabling cost-effective usage and non-intrusive monitoring. This helps you stay up to date with the page performance and frontend quality.

## Use Cases

- **Page performance analysis**: This feature offers metrics such as above-the-fold render time, TCP connection establishment duration, time to first byte (TTFB), and SSL handshake duration. In addition, it supports latest Web Vitals standards, Google's webpage loading speed and experience metrics, for you to optimize the user experience in an all-around manner.
- **Page exception analysis**: This feature helps you quickly locate page exceptions, including page lag, crash, no response, and inoperability.
- **Page log query**: This feature allows you to search for user logs. Then, you can check the environment when the exception occurred and get enough information to locate problems.
- **User access analysis**: This feature displays the business PV/UV and top access metrics of each page. It analyzes the user access data in various dimensions, including network, browser, and region.
- **API monitoring**: The embedded SDK actively reports the APIs requested by the frontend, and the performance monitoring module will collect key API metrics such as API request time and HTTP code success rates, helping you quickly locate API exceptions.
- **Static resource optimization**: This feature monitors the loading time of static resources like JavaScript scripts, CSS style sheets, and images for you to locate the root causes of problems and optimize the loading of such resources for a better user experience.
- **Custom information reporting**: If the data actively reported by the SDK cannot meet your needs, you can customize the logs, events, and resource speed test metrics to be reported.


## Configuration Process

1. Log in to the [CDN console](https://console.cloud.tencent.com/cdn/plugins), enter the **Plugin Center**, and enable the performance monitoring feature.
2. Select the origin type and connect your application.
3. Analyze the page performance and frontend quality through aggregated analysis and page analysis.
4. You can also configure alarms for key metrics, so that when a metric becomes abnormal, you will receive prompt notifications and can take measures accordingly.


## Configuration Guide

### Step 1. Enable the performance monitoring feature

1. Log in to the [CDN console](https://console.cloud.tencent.com/cdn/plugins) and enter the **Plugin Center**.
2. Find the performance monitoring section and toggle on **Performance Monitoring**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/4fcf3894db0495576f4e7ebc8584059d.png)

### Step 2. Connect your application
After performance monitoring is enabled successfully, you will be redirected to the application list. Click **Create Connection**, select the domain name to be connected to, and connect to the performance monitoring SDK as prompted.

![]()



### Step 3. Analyze the performance
After connecting to the performance monitoring SDK successfully, wait several minutes, and then you can click **Aggregated Analysis** in the performance monitoring section to view the aggregated statistics of static resources. You can also switch to **Page Analysis** at the top to view the loading statistics of static resources on individual pages. ![]()
![]()

### Step 4. Configure an alarm policy
On the performance monitoring page, switch to **Alarm Configuration** at the top and create an alarm policy as instructed in [Creating Alarm](https://intl.cloud.tencent.com/document/product/1131/44515).


