
## Overview
This document describes how to quickly integrate TPNS into your iOS application. You can use the local tool to configure TPNS for your application in just a few clicks with no code integration required.

## Preparing for Integration
1. Before integrating the SDK, you need to log in to the [TPNS Console](https://console.cloud.tencent.com/tpns) and create the product and iOS application. For detailed directions, please see [Creating Products and Applications](https://intl.cloud.tencent.com/document/product/1024/32603).

2. Once the application is created, you can apply for trial for it as instructed in [Applying for Trial](https://intl.cloud.tencent.com/document/product/1024/32603#.E7.94.B3.E8.AF.B7.E8.AF.95.E7.94.A8) or purchase the TPNS service as instructed in [Purchasing Push Service](https://intl.cloud.tencent.com/document/product/1024/32604).

3. Upload the push certificate on the **Configuration Management** page. You can get the push certificate as instructed in [Getting Certificate](https://intl.cloud.tencent.com/document/product/1024/30728).
 

4. After completing the above steps, click "Quick Integration" to download the quick integration tool.

5. Decompress the package and double-click TPNS Smart Tool.

6. The message "Unable to open TPNS Smart Tool" will be displayed.

7. Go to "System Preferences" > "Security & Privacy" > "General" and click "Open Anyway".

8. Enter the system password as prompted to confirm the operation and click "Open Anyway" again after the confirmation. The "Open" button will be displayed.

## Starting Integration

Install and open "TPNS Smart Tool" and perform the following operations:
1. Click "Start Integration".
2. Enter the `AccessID` and `AccessKey` of the current application (you can get them on the **Configuration Management** page of the application in [Product Management](https://console.cloud.tencent.com/tpns)).

3. Select the programming language (Objective-C or Swift) used by your Xcode project.
4. Upload your Xcode project file (.xcodeproj).
5. Click **Quick Integration** and wait for the integration result.
 - If you select `Objective-C` as the programming language and the following prompt is displayed, the SDK is successfully integrated.
 - If you select `Swift` as the programming language and the following prompt is displayed, the SDK is successfully integrated.

6. Open the application project configuration and check whether the current project certificate supports push; and if not, process the certificate as prompted by Xcode.
![](https://main.qcloudimg.com/raw/6eca69b3e10f2525d87cd3b58c9e59c3.png)

## Verifying Integration Result
Connect your iPhone to Xcode, install the application, and view the logs in the console. If a log similar to the one below is displayed, the client has properly integrated the SDK.
```
[xgpush]Current device token is 80ba1c251161a397692a107f0433d7fd9eb59******85030f1b913625a9dab
[xgpush]Current XG token is 05da87c0ae597******a9e08d884aada5bb2
```
If the token cannot be found, please check the error code returned by the registration API and troubleshoot as instructed in [Error Codes](https://intl.cloud.tencent.com/document/product/1024/30731).

