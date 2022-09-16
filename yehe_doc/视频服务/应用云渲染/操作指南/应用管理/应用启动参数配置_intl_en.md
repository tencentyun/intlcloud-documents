CAR supports self-service startup parameter configuration. A newly created cloud application can run normally in the CAR environment only after you configure its startup parameters.

## Directions

1. Go to the [CAR console](https://console.cloud.tencent.com/car).
2. Click **Application management** on the left sidebar. On the **Application management** page, click **Startup parameters** of the target application.
![](https://qcloudimg.tencent-cloud.cn/raw/7b168cd24cb530becd116bb87b1a4892.jpg)
3. Enter the configuration information:
![](https://qcloudimg.tencent-cloud.cn/raw/c752b6496ae1730dbc20a485dd9e6656.jpg)

<table>
<thead>
<tr>
<th colspan=2>Configuration Item</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td rowspan=2 width=15%>Application information</td>
<td width=15%>Application ID</td>
<td>It is generated randomly on the backend and doesn't need to be changed.</td>
</tr>
<tr>
<td>Application name</td>
<td>A custom name<strong>It can contain up to 16 letters, digits, or hyphens (-).</strong></td>
</tr>
<tr>
<td rowspan=2>Basic startup parameters</td>
<td>Startup path</td>
<td>If your application has been created, you can directly select the startup path of the .exe file; otherwise, enter a relative startup path, such as <code>EPIC\UE.exe</code></td>
</tr>
<tr>
<td>Process list</td>
<td>The list of processes to be pulled during application operations. You can view the details in the <b>Task Manager</b>, such as `UE.exe`. Make sure that all processes are entered completely to help maintain the application operations in the cloud.</td>
</tr>
<tr>
<td>Advanced startup parameters</td>
<td>Startup parameter</td>
<td>The startup parameter to be passed in during .exe startup<br>Note: <strong>We recommend you make the cloud application get information required by the business through the data channel.</strong></td>
</tr>
<tr>
<td rowspan=2>Capture</td>
<td>Capture the desktop</td>
<td>CAR will capture the cloud system desktop for users to use.</td>
</tr>
<tr>
<td>Capture application window</td>
<td>CAR will capture the window image of the cloud application for users to use. If you need to use an adaptive frontend resolution, we recommend you use this mode. You need to provide the <b>application class name</b> and <b>title</b> (the title is the window title during application startup). If the window title isn't customized during development, the window title after `Demo.exe` starts will be <code>Demo</code>. If your application is a UE application, enter <code>UnrealWindow</code> for the <b>Class name</b>.</td>
</tr>
</tbody></table>


4. After configuration, click **Confirm**.

