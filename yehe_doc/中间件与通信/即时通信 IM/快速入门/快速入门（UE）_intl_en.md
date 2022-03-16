This document describes how to quickly run the IM demo for Unreal Engine.

>? Currently, the demo can be run on Windows, macOS, iOS, and Android.

## Environment Requirements
Unreal Engine 4.27.1 or later.
<table>
   <tr>
      <th width="0px" style="text-align:center">Platform</td>
      <th width="0px" style="text-align:center">Environment</td>
   </tr>
   <tr>
      <td>Android</td>
      <td><li>Android Studio 4.0 or later. </li><li>Visual Studio 2017 15.6 or later. </li><li>A real device for testing.                    </li></td>
   </tr>
   <tr>
      <td>iOS & macOS</td>
      <td><li>Xcode 11.0 or later.                   </li><li>OSX 10.11 or later.       </li><li>Ensure your project has a valid developer signature.  </li></td>
   </tr>
   <tr>
      <td>Windows</td>
      <td><li>OS: Windows 7 SP1 or later (64-bit based on x86-64).                    </li><li>Disk capacity: at least 1.64 GB of space after the IDE and required tools are installed.                            </li><li>Install <a href="https://visualstudio.microsoft.com/zh-hans/downloads/">Visual Studio 2019</a>.        </li></td>
   </tr>
</table>

## Prerequisites
You have [signed up](https://intl.cloud.tencent.com/document/product/378/17985) for a Tencent Cloud account and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions
[](id:step1)
### Step 1. Create an app
1. Log in to the [IM console](https://console.cloud.tencent.com/im).
>? If you already have an app, record its SDKAppID and [obtain key information](#step2).
>A Tencent Cloud account can create a maximum of 300 IM apps. If you want to create a new app, [disable and delete](https://intl.cloud.tencent.com/document/product/1047/34540) an unwanted app first. **Once an app (along with its SDKAppID) is deleted, the service it provides and all its data are lost. Proceed with caution**.
>
2. Click **Create Application**, enter your app name, and click **Confirm**.
![](https://main.qcloudimg.com/raw/15e61a874a0640d517eeb67e922a14bc.png)
3. After creation, you can see the status, service version, SDKAppID, creation time, tag, and expiry time of the new app on the overview page of the console. Record the SDKAppID.
![](https://main.qcloudimg.com/raw/7954cc2882d050f68cd5d1df2ee776a6.png)

[](id:step2)

### Step 2. Obtain key information
1. Click the target app card to go to the basic configuration page of the app.
![](https://qcloudimg.tencent-cloud.cn/raw/8d469e975f1ca5a2f3dbc9c6fe8774f5.png)
2. In the **Basic Information** area, click **Display key**, and then copy and save the key information.
>! Please store the key information properly to prevent disclosure.

[](id:step3)
### Step 3. Configure the demo project file
1. Download the IM demo project from [Download the Demo](https://github.com/tencentyun/IMUnrealEngine).
2. Find and open `/IM_Demo/Source/debug/include/DebugDefs.h`.
3. Set parameters in `DebugDefs.h` as follows:
<ul><li/>SDKAPPID: `0` by default. Set it to the actual `SDKAppID`.
	<li/>SECRETKEY: left empty by default. Set it to the actual key.</ul>
	<img src="https://imgcache.qq.com/operation/dianshi/other/UE4.6a419c2e7f7085671529d3694cb99458527c2970.png"/>

>?
>- In this document, the method to obtain UserSig is to configure a SECRETKEY in the client code. In this method, the SECRETKEY is vulnerable to decompilation and reverse engineering. Once your SECRETKEY is disclosed, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for locally running a demo project and feature debugging**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How to Calculate UserSig on the Server](https://intl.cloud.tencent.com/document/product/1047/34385).

[](id:step4)
### Step 4. Compile, package, and run the project
1. Double-click to open `/IM_Demo/IM_Demo.uproject`.
2. Compile, run, and test the project.
<dx-tabs>
::: macOS\s
**File** -> **Package Project** -> **Mac**
:::
::: Windows\s
**File** -> **Package Project** -> **Windows** -> **Windows(64-bit)**
![](https://imgcache.qq.com/operation/dianshi/other/win.ba79ccce59ae58718e6c35c16cdef55531456a70.png)
:::
::: iOS\s
Package Project
**File** -> **Package Project** -> **Mac**
:::
::: Android\s
1. For development and testing, see [Android Quick Start](https://docs.unrealengine.com/4.27/en/SharingAndReleasing/Mobile/Android/GettingStarted/).
2. For packaging, see [Packaging Android Projects](https://docs.unrealengine.com/4.27/en/SharingAndReleasing/Mobile/Android/PackagingAndroidProject/).
:::
</dx-tabs>

## API Documentation of IM Unreal Engine
For more information on APIs, see [API Overview](https://im.sdk.qcloud.com/doc/en/md_introduction_CPP%E6%A6%82%E8%A7%88.html).

## FAQs

### What should I do if the error "Attempt to construct staged filesystem reference from absolute path" occurs on Android?
Close the project in UE4, open CMD, and run the following commands:

<dx-codeblock>
:::  cmd
adb shell

cd sdcard

ls (you should see the UE4Game directory listed)

rm -r UE4Game
:::
</dx-codeblock>

Compile your project again.
