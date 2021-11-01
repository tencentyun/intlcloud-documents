This document describes how to quickly run the TRTC-API-Example for Android.

## Environment Requirements
- Android 4.1 (SDK API level 16) or above (Android 5.0 (SDK API level 21) or above is recommended.)
- Android Studio 3.5 or above
- Devices with Android 4.1 or above

## Prerequisites
You have [signed up](https://intl.cloud.tencent.com/document/product/378/17985) for a Tencent Cloud account and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions
[](id:step1)
### Step 1. Create an application
1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Click **Create Application** and enter the application name such as `TestTRTC`. If you have already created an application, click **Select Existing Application**.
3. Add or edit tags according to your actual business needs and click **Create**.
![](https://main.qcloudimg.com/raw/8dc52b5fa66ec4a5a4317719f9d442b9.png)
>?
>- An application name can contain up to 15 characters. Only digits, letters, Chinese characters, and underscores are allowed.
>- Tags are used to identify and organize your Tencent Cloud resources. For example, an enterprise may have multiple business units, each of which has one or more TRTC applications. In this case, the enterprise can tag TRTC applications to mark out the unit information. Tags are optional and can be added or edited according to your actual business needs.

[](id:step2)
### Step 2. Download the SDK and TRTC-API-Example source code

1. Download the SDK and TRTC-API-Example source code.
2. Click **Next**.

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

[](id:step3)

### Step 3. Configure TRTC-API-Example project files

1. In the **Modify Configuration** step, select the development platform in line with the source package downloaded.
2. Find and open `LiteAVSDK_TRTC_Android version number/TRTC-API-Example/Debug/src/main/java/com/tencent/trtc/debug/GenerateTestUserSig.java`.
3. Set parameters in `GenerateTestUserSig.java` as follows:
	<ul><li/>SDKAPPID: a placeholder by default. Set it to the actual `SDKAppID`.
	<li/>`SECRETKEY`: a placeholder by default. Set it to the actual key.</ul>
	<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">
4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.

>!
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is disclosed, attackers can steal your Tencent Cloud traffic. Therefore, **this method is suitable only for the local execution and debugging of TRTC-API-Example**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, please see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

### Step 4. Compile and run
Open the `TRTC-API-Example` project with Android Studio (3.5 or above) and click **Run**.

## FAQs
### 1. Only public and private keys can be obtained when I try to view the key. How do I get a key?
TRTC SDK 6.6 (August 2019) and later versions use the new signature algorithm HMAC-SHA256. If your application was created before August 2019, you need to upgrade the signature algorithm to get a new key. Without upgrading, you can continue to use the [old algorithm ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166). After upgrading, you can switch between the new and old algorithms as needed.

Upgrade/Switch:
 1. Log in to the [TRTC console](https://console.cloud.tencent.com/trtc).
 2. Click **Application Management** in the left navigation pane, find your application, and click **Application Info**.
 3. Select the **Quick Start** tab and click **Upgrade**, **Asymmetric Encryption**, or **HMAC-SHA256** in **Step 2: obtain the secret key to issue UserSig**.
  - Upgrade.
  - Switch to the old algorithm ECDSA-SHA256:
      ![](https://main.qcloudimg.com/raw/a8737123c1e3cc0f7eb34901ed2629f7.png)
  - Switch to the new algorithm HMAC-SHA256:
      ![](https://main.qcloudimg.com/raw/701fcde1a562bf9fbbb0d426948e311e.png)

### 2. The app is running on two mobile phones, but why can't they display the images of each other?
Make sure that the two mobile phones use different UserIDs. With TRTC, you cannot use the same UserID on two devices simultaneously unless the SDKAppIDs are different.


### 3. What are firewall restrictions does the SDK face?
The SDK uses the UDP protocol for audio/video transmission and therefore cannot be used in office networks that block UDP. If you encounter such a problem, please see [How to Deal with Firewall Restrictions](https://intl.cloud.tencent.com/document/product/647/35164) to troubleshoot the issue.
