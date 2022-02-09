This document describes how to quickly get started with RUM.


## Step 1. Create a business system[](id:step1)
1. Log in to the [RUM console](https://console.cloud.tencent.com/rum).
2. On the left sidebar, click **Application Management** > **Business System**.
3. On the business system management page, click **Create Business System**. In the pop-up window, enter the business name and indicate your consent to the agreement.

## Step 2. Connect an application[](id:step2)
 1. Log in to the [RUM console](https://console.cloud.tencent.com/rum).
 2. On the left sidebar, click **Data Overview**.
 3. On the data overview page, click **Application Connection** and configure the application information as detailed below:
<table>
<th>
 Configuration Item
</th>
<th>
 Description
</th>
<tr>
<td>
 Application Name
</td>
<td>
 Enter a custom application name, which identifies the application in the RUM console.
</td>
</tr>
<tr>
<td>
 Application Description
</td>
<td>
 Enter an application description such as usage and overview, which helps other users better understand this application.
</td>
</tr>
<tr>
<td>
 Application Type
</td>
<td>
 RUM supports connection to web, mini program (WeChat and QQ), Hippy, Weex, and React Native applications.
</td>
</tr>
<tr>
<td>
 Application Repository Address (optional)
</td>
<td>
 Enter the address of your application repository, which is optional.
</td>
</tr>
<tr>
<td>
 Business System
</td>
<td>
 This feature is used to manage your connected applications by category. For example, you can categorize your applications by conditions such as development team, business logic, and application type. If you have no available teams, click **Create** on the right, enter the relevant information, and click **OK** to create one.
</td>
</tr>
<tr>
<td>
 Enable Auto URL Aggregation
</td>
<td>
 After it is enabled, URLs with the same domain will be aggregated for analysis; for example, <code>app.qq.com/user/123/index.html </code> and <code>app.qq.com/user/456/index.html </code> will be aggregated into <code>app.qq.com/user/*/index.html</code>.
</td>
</tr>
<tr>
<td>
 Sample Rate
</td>
<td>
 It indicates the percentage of user performance data (tested page, API, and static resource speeds) to be reported. 100% indicates that no data will be sampled, and 0% indicates that no performance data will be imported.
</td>
</tr>
</table>

4. After completing the configuration, click **Next** and select a method to install the SDK as detailed below:
- Install the SDK through **npm** (supported for all application types). The followings steps use a web application as an example to describe how to connect to the SDK through npm.
 i. On the connection guide page, copy the first command line to import the npm package.
![](https://qcloudimg.tencent-cloud.cn/raw/daf5b47188e69bcf3a6d77f0231b9848.png)
 ii. On the connection guide page, copy the provided code to initialize the SDK.
![](https://qcloudimg.tencent-cloud.cn/raw/db365dbaa753145e917e7bc1cc955266.png)

- Connect to the SDK by **importing the &lt;script&gt; tag** (supported only for web applications).
 i. On the connection guide page, copy the provided `<script>` tag code.
ii. Import the code below **&lt;script&gt; tag import** into the `<head></head>` tags.
![](https://qcloudimg.tencent-cloud.cn/raw/2a0b0ab2df53d6a3650724e299907913.png)
<dx-alert infotype="explain" title="">
After completing the above steps for connection, you can use the data overview, page performance, exception analysis, page view (PV and UV), API monitoring, and static resource features. If you want to use the log query, offline log, custom speed test, and custom event features, you need to report the data as instructed in the connection guide.
</dx-alert>


## Step 3. View the monitoring data[](id:step3)
After your application is connected successfully and reports a certain amount of data, you can go to the RUM console to view monitoring data such as exception analysis, page performance, and page view.
