This document describes how to quickly run Tencent Cloud MLVB-API-Example for iOS.

## Environment Requirements
- Xcode 9.0 or later
- iPhone or iPad with iOS 9.0 or later
- A valid developer signature for your project

## Prerequisites
You have [signed up for a Tencent Cloud account](https://www.tencentcloud.com/document/product/378/17985).

## Directions
[](id:step1)
### Step 1. Download the SDK and MLVB-API-Example source code
1. Download the package [here](https://www.tencentcloud.com/document/product/1071/38150) as needed. Here, the [Professional Edition](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Professional_iOS_latest.zip) is used as an example.
2. Decompress the file after download.<br>
>!The source code can also be obtained from [GitHub](https://github.com/LiteAVSDK/Live_iOS/tree/main/MLVB-API-Example-OC).

[](id:step2)
### Step 2. Configure the license
1. Log in to the [CSS console](https://console.tencentcloud.com/live/livestat), select **MLVB SDK** > [**License Management**](https://console.tencentcloud.com/live/license) on the left sidebar, and click **Create**.
 ![](https://qcloudimg.tencent-cloud.cn/raw/ed8480080cbbd5283d5f8bca8266304b.png) 
2. Enter the `App Name`, `Package Name`, and `Bundle ID` as needed, select the **Live streaming** feature module (**Live Push** + **Video Playback**), and click **Confirm**.
  - **Package Name**: Enter the **applicationId** in the **build.gradle** file in the `App` directory.
  - **Bundle ID**: Enter the **Bundle Identifier** of the project in **Xcode**.

3. After the free trial license is created successfully, the page will display the information of the generated license. **You need to pass in two parameters `Key` and `License URL` during initial SDK configuration. Store the following information properly:**
<img src="https://qcloudimg.tencent-cloud.cn/raw/a6b24e8677c514ee1721d38893fd9ca2.png" width=800>
4. Open the `LiteAVSDK_Professional_iOS_version number/MLVB-API-Example-OC/Debug/GenerateTestUserSig.h` file.
Set parameters in `GenerateTestUserSig.h` as follows:
    - LICENSEURL: Empty by default. Set it to the actual download license URL.
    - LICENSEURLKEY: Empty by default. Set it to the actual download license key.
<img src="https://main.qcloudimg.com/raw/bcf6f24c3f6e480106479d47dd335b93.png" width=600px>


[](id:step3)
### Step 3. Configure stream push/playback capabilities
1. Apply for a domain name in [DNSPod](https://dnspod.cloud.tencent.com/?from=qcloudProductDns) and get an ICP filing for it.
2. Add the stream push/playback domain name in **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** in the **CSS console**. For detailed directions, see [Adding Your Own Domain](https://intl.cloud.tencent.com/document/product/267/35970).
3. Configure the CNAME record for the domain name as instructed in [Configuring CNAME](https://intl.cloud.tencent.com/document/product/267/31057).
4. After configuring the stream push/playback domain name, you can get the `CNAME` information on the **Basic Info** page of the domain name.
<img src="https://qcloudimg.tencent-cloud.cn/raw/3e43f156dce4b4575bdc6f4d6fdd87b6.png
" width=500px>
5. Open the `LiteAVSDK_Professional_iOS_version number/MLVB-API-Example-OC/Debug/GenerateTestUserSig.h` file.
Set parameters in `GenerateTestUserSig.h` as follows:
  - **PUSH_DOMAIN**: Set it to your [stream push domain name](https://console.cloud.tencent.com/live/domainmanage).
  - **PLAY_DOMAIN**: Set it to your [playback domain name](https://console.cloud.tencent.com/live/domainmanage).
  - **LIVE_URL_KEY**: This parameter is optional. It is used to generate authentication information such as `txSecret`. For more information on how to calculate it, see [Publishing/Playback URL](https://www.tencentcloud.com/document/product/1071/39359). You can query it in **Manage** > **Stream Push Configuration** > **Authentication Configuration** on the [Domain Name](https://console.cloud.tencent.com/live/domainmanage) page.<br>


[](id:push)
#### Configuring stream push parameters
1. Find and open the `LiteAVSDK_Professional_iOS_version number/MLVB-API-Example-OC/Debug/GenerateTestUserSig.h` file.
2. Set parameters in the [GenerateTestUserSig.h](https://github.com/LiteAVSDK/Live_iOS/tree/main/MLVB-API-Example-OC/Debug/GenerateTestUserSig.h) file based on the above service:
 - SDKAppID: `0` by default. Set it to the actual `SDKAppID`.
 - SECRETKEY: Empty by default. Set it to the actual secret key.

[](id:pushurl)
#### Stream push URL field description
You need to concatenate the specific stream push/pull URL string based on the used protocol as instructed in [Publishing/Playback URL](https://www.tencentcloud.com/document/product/1071/39359). A string has been concatenated in the demo, and the stream can be played back after you run the demo.

[](id:step5)
### Step 5. Compile and run
Open the demo project `MLVB-API-Example-OC` with Xcode 9.0 or later and click **Run**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/9f99f106e3899046b40f19394ccdb313.png" width=300px>
