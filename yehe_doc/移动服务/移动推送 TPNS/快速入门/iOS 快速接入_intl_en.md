## Overview

This document describes how to quickly integrate TPNS into your iOS application. You can use the local tool to configure TPNS for your application in just a few clicks with no code integration required.


## Preparing for Integration

### Creating an iOS application

1. Before integrating the SDK, you need to log in to the [TPNS Console](https://console.cloud.tencent.com/tpns) and create the product and iOS application. For detailed directions, please see [Creating Products and Applications](https://intl.cloud.tencent.com/document/product/1024/32603).

2. Upload the push certificate on the **Configuration Management** page. You can get the push certificate as instructed in [Acquisition of Push Certificate](https://intl.cloud.tencent.com/document/product/1024/30728).

3. After completing the above steps, click "Quick Integration" to download the quick integration tool.

4. Decompress the package and double-click TPNS Smart Tool.

5. The message "Unable to open TPNS Smart Tool" will be displayed.

6. Go to **System Preferences** > **Security & Privacy** > **General** and click **Open Anyway**.

7. Enter the system password as prompted to confirm the operation and click **Open Anyway** again after the confirmation. The **Open** button will be displayed. Then, click it.



## Starting Integration

1. After starting the quick integration tool, go to the homepage and click **Start Integration**.

2. Enter the configuration page and configure the following 6 items as detailed below.


### Configuration items 1 and 2: AccessID and AccessKey

Log in to the [TPNS console](https://console.cloud.tencent.com/tpns).

1. On the "Product Management" page, find the product for which to configure the push capability and select configuration management for iOS or macOS.

2. Enter the product configuration management details page, copy `AccessID` and `AccessKey`, and paste them into the corresponding input boxes in the quick integration tool.


### Configuration item 3: project language

- Please select according to the language used by the `AppDelegate` file:
  - For `AppDelegate.m`, please select `Objective-C`
  - For `AppDelegate.swift`, please select `Swift`

### Configuration item 4: project file

Please select the project file with the extension of `.xcodeproj`:
![](https://main.qcloudimg.com/raw/28fdfcc8a2d2af749d54b48880f048c5.jpg)

### Configuration item 5: basic push capability

Basic push capability: normal push notification capability, which does not contain features such as push data reach statistics and rich media push.

### Configuration item 6: notification service extension plugin

Notification service extension plugin is mainly used to calculate the reach rate of pushes and implement features such as rich media push.
- If you select automatic signing for `Xcode`, `Xcode` will generate a provisioning file for your notification service extension plugin on the Apple Developer platform.
- If you select manual signing for `Xcode`, you need to manually generate a provisioning file on the Apple Developer platform. Otherwise, the application cannot be installed on a real device for debugging. The steps are as follows:


1. Go to the [Apple Developer platform](https://developer.apple.com/account/resources/identifiers/list) to apply for a bundle identifier for the notification service extension plugin.
>?Bundle identifier naming rule: (main target Bundle Identifier).TPNSService.
2. Apply for a provisioning file containing the bundle identifier.

3. Specify `Bundle Identifier` and `Provisioning Profile` of the extension plugin as the bundle identifier and provisioning file you applied for respectively.
![](https://main.qcloudimg.com/raw/eb8edae0c798ac9434c930eba3178fa8.png)
> ?
>- If you are **integrating TPNS for the first time**, we recommend you check items 5 and 6 at the same time; otherwise, the push reach data cannot be obtained, and rich media pushes cannot be delivered.
>- You can integrate configuration item 5 or 6 separately or integrate both of them at the same time as needed by your project.




### Integrating TPNS SDK

1. After the above 6 configuration items are set, the **Quick Integration** button will become blue and clickable. Then, click it.

2. After successful integration, the following pop-up window will be displayed.


## Project Structure and Configuration After Successful Integration

- If the integration is successful, the project structure and configuration will be as shown below:
  ![](https://main.qcloudimg.com/raw/e8afaa08424282986e0d0d83b93d5f14.jpg)
  ![](https://main.qcloudimg.com/raw/f830b564e0c6736bb77abff6224c693c.jpg)
- If there are exceptions such as compilation failure, no push notifications, or no reach rate statistics, please check the configuration of your project against the above figure to locate the integration error or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

## Verifying Integration Result

Connect your iPhone to Xcode, install the application, and view the logs in the console. If a log similar to the one below is displayed, the client has properly integrated the SDK.

```plaintext
[TPNS] Current device token is 9298da5605c3b242261b57****376e409f826c2caf87aa0e6112f944
[TPNS] Current TPNS token is 00c30e0aeddff1270d8****dc594606dc184
```

If the token cannot be found, please check the error code returned by the registration API and troubleshoot as instructed in [Error Codes](https://intl.cloud.tencent.com/document/product/1024/30731).

