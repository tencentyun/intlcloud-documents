Thank you for using Tencent Cloud Game Multimedia Engine (GME) SDK. This document provides the information on Unity SDK project configuration to make it easy for Unity developers to debug and integrate the APIs for GME.

## SDK Preparation

You can obtain the SDK by the following steps:

### Download SDK

Go to the [Download Instructions](https://cloud.tencent.com/document/product/607/18521) page.

Locate SDK resource for Unity on the interface.

Click **Download**. The SDK resource contains following items after decompression:

![](https://main.qcloudimg.com/raw/55494d9bb9145938f0594416f73b29f7.png)

Description:

| File Name | Description           
| ------------- |:-------------:|
| Plugins | SDK library file |
| Scripts | SDK code file |

## Preparations

### 1. Import Plugins
Copy the files from the Plugins folder in the development kit into the Plugins folder under Assets of the Unity project, as shown below:  
![](https://main.qcloudimg.com/raw/1221a25f62cedd3831cf2bb27bb1ea45.png)

### 2. Import code file
Copy the files in the Scripts folder in the SDK to the folder used to store code in the Unity project, as shown below:  
![](https://main.qcloudimg.com/raw/8904a83c6173fa7c5b04ddb0e48138ca.png)

### 3. Audio settings
In the Unity editor, go to **Edit** -> **Project Setting** -> **Audio** and use the default system settings. If you make a change to the settings, Unity playback sound effect will be interrupted due to the iobuffer set on the iOS device.
![](https://main.qcloudimg.com/raw/df14517cac7fc29383c90720627572c7.png)

If the settings are as follows, Unity playback sound effect will be interrupted due to the iobuffer set on the iOS device.
![](https://main.qcloudimg.com/raw/69857f53bdc2ee7c7ad5e48777620df1.png)


## Exporting to Different Platforms

Project configuration is required before you can export executable files from the Unity engine to different platforms:

| Platform | Project Configuration           
| ------------- |:-------------:|
| Android | [Project Configuration for Android](https://cloud.tencent.com/document/product/607/15203) |
| iOS | [Project Configuration for iOS](https://cloud.tencent.com/document/product/607/15219) |
| Mac | [Project Configuration for Mac](https://cloud.tencent.com/document/product/607/18617) |
