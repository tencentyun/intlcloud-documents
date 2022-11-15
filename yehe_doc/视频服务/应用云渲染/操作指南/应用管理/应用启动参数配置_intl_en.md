In CAR, you can configure your own startup parameters for your applications. A newly created cloud application can run normally in the CAR environment only after you configure its startup parameters.

## Directions

1. Enter the [CAR console](https://console.cloud.tencent.com/car).
2. Click **Application management** on the left sidebar, and click **Startup parameters** of the target application.
![](https://qcloudimg.tencent-cloud.cn/raw/7b168cd24cb530becd116bb87b1a4892.jpg)
3. Complete the required information:
![](https://qcloudimg.tencent-cloud.cn/raw/c752b6496ae1730dbc20a485dd9e6656.jpg)
   For example, for the following application package:
	![](https://qcloudimg.tencent-cloud.cn/raw/dfccf8ee97854b5ac916618bd3dc49b9.png)
	
	The basic startup parameters should be configured as follows:
	![](https://qcloudimg.tencent-cloud.cn/raw/dfcab2df84c97dbebd4c46dc169a81dd.png)

* **Startup path** is the full relative path to your startup application (.exe). If your application has already been created, click **Browse** to select the startup path of the .exe file. **Do not select** the startup path of processes that are not required to start the application, such as `UnityCrashHandler64.exe`.
	
* For stability of your applications in the cloud, we recommend you completely enter all processes to be run by the application, such as `demo.exe|Win64-Shipping.exe`. You can run the application on your local PC and open Windows Task Manager to check which processes are required.
	

For more information, see the table below:

<table>
<thead>
<tr>
<th colspan=2>Configuration item</th>
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
<td>A custom name. <strong>It can contain up to 16 letters, digits, or hyphens (-).</strong></td>
</tr>
<tr>
<td rowspan=2>Basic startup parameters</td>
<td>Startup path</td>
<td>If your application has already been created, you can directly select the startup path of the .exe file; otherwise, enter a relative startup path, such as <code>EPIC\UE.exe</code></td>
</tr>
<tr>
<td>Processes</td>
<td>The processes to be run during application operations, such as `UE.exe`. You can view the details of the processes run by your application by opening the <b>Task Manager</b>. Make sure that all processes are entered completely to help maintain the application operations in the cloud.</td>
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
<td>CAR will capture the window image of the cloud application for users to use. If you need to use an adaptive frontend resolution, we recommend you use this mode. You need to provide the <b>application class name</b> and <b>title</b> (the title is the window title during application startup). If the window title isn't customized during development, the window title after `Demo.exe` starts will be <code>Demo</code>. If your application is a UE application, enter <code>UnrealWindow</code> for the **Class name**. For detailed instructions, see [Using Window Capturing Mode](https://www.tencentcloud.com/document/product/1158/50549).</td> 
</tr>
</tbody></table>


4. After the configuration is complete, click **Confirm**.
