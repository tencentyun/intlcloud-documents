This document shows you how to quickly run TRTC-API-Example (Android).

## Environment Requirements
- Android 4.1 (SDK API level 16) or later; Android 5.0 (SDK API level 21) or later is recommended.
- Android Studio 3.5 or later
- Devices with Android 4.1 or later

## Prerequisites
You have [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985).

## Directions

### Step 1. Create an application

1. Log in to the TRTC console and select [Application Management](https://console.cloud.tencent.com/trtc/app) on the left sidebar.

2. Click **Create application**, enter an application name such as `APIExample`. If you already have an application, select **Existing** and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/6704c9f7eb9e18e422c513cb9a2a3926.png)


### Step 2. Download the sample code

1. Select **No UI** and go to GitHub to download the sample code for your platform.
2. Click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/d28964ad85dddd85833a28310a62d514.png)


### Step 3. Configure the project
1. If you are running a demo project, select **Testing**. Note the `SDKAppID` and secret key.
![](https://qcloudimg.tencent-cloud.cn/raw/82a45972f2d12763a6dc80eee6c952c0.png)
2. Open the file downloaded previously. Follow the instructions in the console to modify the `SDKAppID` and secret key, and click **Next**.

>?
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in the client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is disclosed, attackers can steal your Tencent Cloud traffic. Therefore, **this method is suitable only for the local execution and debugging of TRTC-API-Example**.
>- The best practice is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to your server for a dynamic `UserSig`. For more information, see [How do I calculate `UserSig` during production?](https://www.tencentcloud.com/document/product/647/35166).

### Step 4. Compile and run the demo
Open the demo project `TRTC-API-Example` with Android Studio (v3.5 or later) and run the project.


## FAQs

### 1. The app is running on two mobile phones, but why can't they display the images of each other?
Make sure that the two mobile phones use different `UserID`. With TRTC, you cannot use the same `UserID` on two devices simultaneously unless the `SDKAppID` is different.

### 2. What are the restrictions of the firewall?
The SDK uses the UDP protocol for audio/video transmission and therefore cannot be used in office networks that block UDP. If you encounter such a problem, you can refer to [Firewall Restrictions](https://intl.cloud.tencent.com/document/product/647/35164) to troubleshoot the issue.
