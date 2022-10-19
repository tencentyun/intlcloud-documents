This document describes how to configure a Unity project for the GME APIs for Unity.


## Downloading SDK

1. Download the applicable demo and SDK. For more information, please see [SDK Download Guide](https://intl.cloud.tencent.com/zh/document/product/607/18521).
2. Locate the SDK resources for Unity on the page.
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
<td>Plugins</td>
<td align="center">SDK library files</td>
<td>Stores library files for each platform</td>
</tr>
<tr>
<td>GMESDK</td>
<td align="center">SDK code files</td>
<td>Provides APIs</td>
</tr>
</tbody></table>


<dx-alert infotype="explain" title="Platforms supported by SDK for Unity">
SDK for Unity has integrated Windows, Mac, Android, and iOS platform architectures at the same time.
</dx-alert>



## Project Configuration

### Step 1: import Plugins files

Copy the files from the `Plugins` folder in the SDK to the folder under **Unity project** > **Assets** > **Plugins** as shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/ce8ba3561d43148971f1cbe9076be3a3.png"  width="100%" /></img>



<dx-alert infotype="explain" title="">
If you don't need to export executables in the Win32 architecture, delete the `x86` folder under the `Plugins` folder.
</dx-alert>




### Step 2: import code files

Copy the files in the `Scripts` folder in the SDK to the folder used to store code in your Unity project as shown below:  
<img src="https://qcloudimg.tencent-cloud.cn/raw/5ab4509590a5effa9e8aadeee2456492.png"  width="100%" /></img>



## Unity 2021 Configuration
If you use Unity Editor 2021 or higher, you need to cut the `lib` folder under `Plugins` > `Android` > `Opensdk.plugin` and paste it in the `Android` directory of the `Plugins` file in the project, at the same level as `Opensdk.plugin`.

<img src="https://qcloudimg.tencent-cloud.cn/raw/bc7156db71faf994654c824787bfb1a9.png"  width="65%" /></img>


## Audio Settings

In the Unity editor, go to **Edit > Project Settings > Audio** and use the default system settings. If you make a change to the settings, Unity playback sound effect will be affected due to the hardware buffer set on the iOS device, as shown below:
<img src="https://main.qcloudimg.com/raw/db8975fcaefa3dc71732ede1b5f979db.png"  width="50%" /></img>


<dx-alert infotype="forbid" title="Unity Audio Setting">
Please do not set the **Audio** module in **Project Settings**.
</dx-alert>

If the settings are as follows, Unity playback sound effect will be interrupted due to the hardware buffer set on the iOS device:
![](https://qcloudimg.tencent-cloud.cn/raw/6eb910221b8a24289dcffe0a39d60573.png)

## Operations on macOS

If you use Unity to access the GME SDK on macOS 10.15.x, an error shows that the file is corrupted during the execution due to the `com.apple.quarantine` attribute.
The most direct solution is to delete the `com.apple.quarantine` attribute, as shown below:
1. Run the `cd` command in terminal to go to the `Unity_OpenSDK_Audio/Assets/Plugins/` folder in the project.
2. Run the following command.
```
$ xattr -d com.apple.quarantine gmesdk.bundle
```



<dx-alert infotype="explain" title="">
This operation is risky. It is recommended to use a lower version of macOS for access.
</dx-alert>

