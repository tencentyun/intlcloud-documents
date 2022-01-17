## Overview

This document describes how to configure a Unreal Engine project for the GME APIs for Unreal Engine.

## Downloading SDK

1. Download the applicable demo and SDK. For more information, please see [SDK Download Guide](https://intl.cloud.tencent.com/zh/document/product/607/18521).
2. Locate the SDK resources for Unreal Engine on the page.
3. Click **Download**. After decompression, the downloaded SDK resources include the following files:
<table>
<thead>
<tr>
<th>File Name</th>
<th align="center">Description</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>GMESDK.uplugin</td>
<td align="center">Plugin file</td>
<td>Plugin configuration file</td>
</tr>
<tr>
<td>Resources</td>
<td align="center">Plugin resource file</td>
<td>Plugin resource file</td>
</tr>
<tr>
<td>Source</td>
<td align="center">SDK files</td>
<td>SDK library files and code files for various platforms, such as header files</td>
</tr>
</tbody></table>
<dx-alert infotype="explain" title="Platforms supported by SDK for Unreal Engine:">
SDK for Unreal Engine has integrated Windows, macOS, Android, and iOS platform architectures. If you need console platform architectures, [submit a ticket](https://console.intl.cloud.tencent.com/workorder).
</dx-alert>

## Project Configuration

### Step 1: import Plugins files

In the Unreal Engine project directory, open the `Plugins` folder (create it if it does not exist) and copy the SDK into it as shown below:
![](https://main.qcloudimg.com/raw/751894ab16c5262b7a99370cc7efd52c.png)

### Step 2: compile the plugin

After importing, compile the plugin in Unreal Engine.
![](https://main.qcloudimg.com/raw/562882f1d39aa0d4fc77e835290d99df.png)

### Step 3: complete compilation

After compilation is completed, the following directories will appear in VS 2015.
![](https://main.qcloudimg.com/raw/0070a5057c678182ca78c166b9aeaeee.png)

### Step 4: open to view the GME plugin

Open the Unreal Engine again, click **Edit**, and click **Plugins** to view the GME plugin. Make sure that the GME SDK is in **Enabled** status.
![](https://main.qcloudimg.com/raw/60fb6340f6899e2c8fc6f4693193533e.png)

## Adaptations of Different Unreal Engine Versions

### Unreal Engine 4.21 and above

If you are using Unreal Engine 4.21 or higher, you need to add the following code after downloading the GME sample code for Unreal Engine:

```
AUEDemoLevelScriptActor::AUEDemoLevelScriptActor()
{
    PrimaryActorTick.bCanEverTick = true;
}
```

<dx-alert infotype="explain" title="">
Tick is disabled by default and must be enabled manually.
</dx-alert>



### Unreal Engine 4.26

If you are using Unreal Engine 4.26, you need to download the [adaptation file](http://dldir1.qq.com/hudongzhibo/QCloud_TGP/GME/pubilc/UEDemo_4.26Adapter.zip) and import it into the project. The downloaded file contains two folders: `Source` and `Plugins`.

- For a demo project, import both folders into the project in an overwriting manner.
- If you only need the GME SDK, import the `Plugins` folder only.
