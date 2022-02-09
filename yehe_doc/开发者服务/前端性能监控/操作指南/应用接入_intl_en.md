RUM can be connected to web, mini program (WeChat and QQ), Hippy, Weex, React Native, and Flutter applications. This document describes how to connect an application.

## Directions
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
 RUM can be connected to web, mini program (WeChat and QQ), Hippy, Weex, React Native, and Flutter applications.
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
</table>

4. After completing the configuration, click **Next** and select a method to install the SDK as detailed below:
- Install the SDK through **npm** (supported for all application types). The followings steps use a web application as an example to describe how to connect to the SDK through npm.
 i. On the connection guide page, copy the first command line to import the npm package.
![](https://qcloudimg.tencent-cloud.cn/raw/daf5b47188e69bcf3a6d77f0231b9848.png)
 ii. On the connection guide page, copy the provided code to initialize the SDK.
![](https://qcloudimg.tencent-cloud.cn/raw/5359b9c4063336e6ac9f477ceb0a27c0.png)
- Connect to the SDK by **importing the &lt;script&gt; tag** (supported only for web applications).
 i. On the connection guide page, copy the provided `<script>` tag code.
ii. Import the code below **&lt;script&gt; tag import** into the `<head></head>` tags.
![](https://qcloudimg.tencent-cloud.cn/raw/038a1cdd1462a9b7fc6581a5da264891.png)
<dx-alert infotype="explain" title="">
After completing the above steps for connection, you can use the data overview, page performance, exception analysis, page view (PV and UV), API monitoring, and static resource features. If you want to use the log query, offline log, custom speed test, and custom event features, you need to report the data as instructed in the connection guide.
</dx-alert>
