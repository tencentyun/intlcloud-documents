This document describes how to quickly run the Tencent Cloud MLVB-API-Example for Android.

## Environment Requirements
- Android 4.1 (SDK API level 16) or above; Android 5.0 (SDK API level 21) or above is recommended.
- Android Studio 3.5 or later
- Device on Android 4.1 or above for the application

## Prerequisites
You have [signed up for a Tencent Cloud account](https://www.tencentcloud.com/document/product/378/17985).

## Directions
[](id:step1)
### Step 1. Download the SDK and MLVB-API-Example source code
1. Download the package [here](https://www.tencentcloud.com/document/product/1071/38150) as needed. Here, the [Professional Edition](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Professional_Android_latest.zip) is used as an example.
2. Decompress the file after download.<br>
>!The source code can also be obtained from [GitHub](https://github.com/LiteAVSDK/Live_Android/tree/main/MLVB-API-Example).

[](id:step2)
### Step 2. Configure the license
1. Log in to the [CSS console](https://console.tencentcloud.com/live/livestat), select **MLVB SDK** > [**License Management**](https://console.tencentcloud.com/live/license) on the left sidebar, and click **Create**. 
![](https://qcloudimg.tencent-cloud.cn/raw/ed8480080cbbd5283d5f8bca8266304b.png) 
2. Enter the `App Name`, `Package Name`, and `Bundle ID` as needed and click **Confirm**. 
  - **Package Name**: Enter the **applicationId** in the **build.gradle** file in the `App` directory.
  - **Bundle ID**: Enter the **Bundle Identifier** of the project in **Xcode**.

3. After the license is created successfully, the page will display the information of the generated license. **You need to pass in two parameters, `Key` and `License URL`, during initial SDK configuration. Store the following information properly.** 
<img src="https://qcloudimg.tencent-cloud.cn/raw/a6b24e8677c514ee1721d38893fd9ca2.png" width=800>
4. Open the `LiteAVSDK_Professional_Android_version number/MLVB-API-Example/Debug/src/main/java/com/tencent/mlvb/debug/GenerateTestUserSig.java` file. Set parameters in `GenerateTestUserSig.java` as follows:
  - `LICENSEURL`: A placeholder by default. Set it to the actual download license URL.
  - LICENSEURLKEY: A placeholder by default. Set it to the actual download license key.

[](id:step3)
### Step 3. Configure stream push/playback capabilities
1. Apply for a domain name in [DNSPod](https://dnspod.cloud.tencent.com/?from=qcloudProductDns) and get an ICP filing for it.
2. Add the stream push/playback domain name in **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** in the **CSS console**. For detailed directions, see [Adding Your Own Domain](https://intl.cloud.tencent.com/document/product/267/35970).
3. Configure the CNAME record for the domain name as instructed in [Configuring CNAME](https://intl.cloud.tencent.com/document/product/267/31057).
4. After configuring the stream push/playback domain name, you can get the `CNAME` information on the **Basic Info** page of the domain name.
<img src="https://qcloudimg.tencent-cloud.cn/raw/3e43f156dce4b4575bdc6f4d6fdd87b6.png" width=500px>
5. Open the `LiteAVSDK_Professional_Android_version number/MLVB-API-Example/Debug/src/main/java/com/tencent/mlvb/debug/GenerateTestUserSig.java` file.
Set parameters in `GenerateTestUserSig.java` as follows:
  - **PUSH_DOMAIN**: Set it to your [stream push domain name](https://console.cloud.tencent.com/live/domainmanage).
  - **PLAY_DOMAIN**: Set it to your [playback domain name](https://console.cloud.tencent.com/live/domainmanage).
  - **LIVE_URL_KEY**: This parameter is optional. It is used to generate authentication information such as `txSecret`. For more information on how to calculate it, see [Publishing/Playback URL](https://cloud.tencent.com/document/product/454/7915). You can query it in **Manage** > **Stream Push Configuration** > **Authentication Configuration** on the [Domain Name](https://console.cloud.tencent.com/live/domainmanage) page.<br>


[](id:push)
#### Configuring stream push parameters
1. Find and open the `LiteAVSDK_Professional_Android version number/MLVB-API-Example/Debug/src/main/java/com/tencent/mlvb/debug/GenerateTestUserSig.java` file.
2. Set parameters in the [GenerateTestUserSig.java](https://github.com/LiteAVSDK/Live_Android/tree/main/MLVB-API-Example/Debug/src/main/java/com/tencent/mlvb/debug/GenerateTestUserSig.java) file based on the above service:
  - SDKAPPID: A placeholder by default. Set it to the actual `SDKAppID`.
  - SECRETKEY: A placeholder by default. Set it to the actual secret key.

[](id:pushurl)
#### Stream push URL field description
You need to concatenate the specific stream push/pull URL string based on the used protocol as instructed in [Publishing/Playback URL](https://www.tencentcloud.com/document/product/1071/39359). A string has been concatenated in the demo, and the stream can be played back after you run the demo.

[](id:step5)

### Step 5. Compile and run
Open the demo project `MLVB-API-Example` with Android Studio 3.5 or later and click **Run**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/70bb721a8cea4c41b697804cad70ed5b.png" width=300px>
