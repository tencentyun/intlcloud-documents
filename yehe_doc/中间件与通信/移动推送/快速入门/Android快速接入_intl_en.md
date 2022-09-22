## Overview
This document describes how to quickly integrate TPNS into your Android application. You can use the TPNS service on your application in just four steps.
## Preparing for Integration
1. Before integrating the SDK, you need to log in to the [TPNS Console](https://console.cloud.tencent.com/tpns) and create the product and Android application. For detailed directions, please see [Creating Products and Applications](https://intl.cloud.tencent.com/document/product/1024/32603).
3. After completing the above steps, enter the application's **Configuration Management** page to prepare for the integration.

## Starting Integration
1. On the **Configuration Management** page, click **Quick Integration**.
2. Complete the configuration as instructed in the integration guide and click "Verify".
3. If the following prompt is displayed, the SDK is successfully integrated.

- If the following prompt is displayed, please check whether the trial has been activated or whether the push service has been purchased for the application.

You can view the current application service status on the [Product Management](https://console.cloud.tencent.com/tpns) page. The service will be activated 30 minutes after you apply for the trial or purchase the service.

- If the following prompt is displayed, please check whether the application has been successfully registered with the push service as instructed in [Verifying Integration Result](#jierujieguo).

<span id="jierujieguo"></span>
## Verifying Integration Result
1. Run the application, filter logs by the "TPush" keyword, and view the displayed logs:
![](https://main.qcloudimg.com/raw/3534e6c05ab9f6959e6e19d4272dc48b.png)
If a log similar to the one above is displayed, the TPNS SDK has been successfully integrated as a plugin.

2. The log of successful registration with the push service is as shown below:
```
XG register push success with token:6ed8af8d7b18049d9fed116a9db9c71ab44d5565
```
If the token cannot be found, please check the error code returned by the registration API and troubleshoot as instructed in [Error Codes](https://intl.cloud.tencent.com/document/product/1024/30722)

## Quickly Integrating with Vendor Channel
1. On the configuration management page, enable the vendor push channel and configure application information such as `AppId` and `SecretKey`. For more information about how to apply for such information, see the documentation of the vendor channel.
 - Click **View Documentation** to see the vendor channel description.
 - Configure the vendor channel at `AppId`, `AppKey`, and `AppSecret` on the right.
2. After configuring the vendor channel information, click **Download Configuration File** at the top to download the vendor channel configuration file and use it to replace the legacy one in the project file.
![](https://main.qcloudimg.com/raw/4dfa37ac471c1c3b18cc559d5780a6be.png)

## Troubleshooting
1. View plugin logs.
If an exception occurs during integration, set the `"debug"` field in the `tpns-configs.json` file to `true` and run the following command: 
```
./gradlew --rerun-tasks :app:processReleaseManifest 
```
Then, use the `"TpnsPlugin"` keyword for analysis.
2. Sync projects.
![](https://main.qcloudimg.com/raw/30368ed3cb4a25f3c33be46e3c1f2f5d.png)
3. Check whether there are relevant dependencies in the External Libraries of the project.
![](https://main.qcloudimg.com/raw/1de82d05f351939883e1870ae7300c44.png)
