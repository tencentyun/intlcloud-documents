This document describes how to configure a Unity project for the GME APIs for Unity.


## Downloading SDK

1. Download the applicable demo and SDK. For more information, please see [SDK Download Guide](https://intl.cloud.tencent.com/document/product/607/18521).
2. Locate the SDK resources for Unity on the page.
3. Click **Download**. After decompression, the downloaded SDK resources include the following files:
<table>
<thead>
<tr>
<th>File Name</th>
<th align="center">Description</th>
<th>Role</th>
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

Copy the files from the `Plugins` folder in the SDK to the folder under **Plugins** > **Assets** > **Plugins** as shown below:
<img src="https://main.qcloudimg.com/raw/ce80710126e82b2af58090207a3ae077.png"  width="65%" /></img>

>?If you don't need to export executables in the Win32 architecture, delete the `x86` folder under the `Plugins` folder.


### Step 2: import code files

Copy the files in the `Scripts` folder in the SDK to the folder used to store code in your Unity project as shown below:  
<img src="https://main.qcloudimg.com/raw/21e8b967c75ebdd2ea1686cfd434f89c.png"  width="65%" /></img>




## Audio Settings

In the Unity editor, go to **Edit > Project Settings > Audio** and use the default system settings. If you make a change to the settings, Unity playback sound effect will be interrupted due to the hardware buffer set on the iOS device, as shown below:
<img src="https://main.qcloudimg.com/raw/db8975fcaefa3dc71732ede1b5f979db.png"  width="50%" /></img>


<dx-alert infotype="forbid" title="Unity Audio Setting">
Please do not set the **Audio** module in **Project Settings**.
</dx-alert>

If the settings are as follows, Unity playback sound effect will be interrupted due to the hardware buffer set on the iOS device:
![](https://main.qcloudimg.com/raw/0b1c09af7f42e39081cca1718baaede3.png)

## Operations on macOS

If you use Unity to access the GME SDK on macOS 10.15.x, an error shows that the file is corrupted during the execution due to the `com.apple.quarantine` attribute.
![](https://main.qcloudimg.com/raw/29aa9b69f32c13ffe3c6db4559c9ff17.png)
The most direct solution is to delete the `com.apple.quarantine` attribute, as shown below:
1. Run the `cd` command in terminal to go to the `Unity_OpenSDK_Audio/Assets/Plugins/` folder in the project.
2. Run the following command.
```
$ xattr -d com.apple.quarantine gmesdk.bundle
```

>?This operation is risky. It is recommended to use a lower version of macOS for access.
>

