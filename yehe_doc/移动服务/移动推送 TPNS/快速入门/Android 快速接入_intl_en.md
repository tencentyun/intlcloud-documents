## Overview

This document describes how to quickly integrate TPNS into your Android application. You can use the TPNS service on your application in just three steps.

## Preparing for Integration

1. Before integrating the SDK, you need to log in to the [TPNS Console](https://console.cloud.tencent.com/tpns) and create the product and Android application. For detailed directions, please see [Creating Products and Applications](https://intl.cloud.tencent.com/document/product/1024/32603).
   ![](https://main.qcloudimg.com/raw/748fd7e885077735bdb631aab2bae2b7.png)
2. Then go to the application's **Configuration Management** page to prepare for the integration.
   ![](https://main.qcloudimg.com/raw/f2047b88c465df6abc36104253241cae.png)

## Step 1: start integration

1. On the **Configuration Management** page, click **Quick Integration**.
![](https://main.qcloudimg.com/raw/c45001ef6396382a83b73105f3a7214e.png)
2. Complete the configuration as instructed in the integration guide and click **Click to verify**.
![](https://main.qcloudimg.com/raw/910f9e03f0c609e847676ee2b62a7a66.png)
3. If the following prompt is displayed, the SDK has been successfully integrated.
![](https://main.qcloudimg.com/raw/20dcdc160613bf6b8552a508891cbda5.png)
	- If the following prompt is displayed, please check whether you have applied for a free trial or purchased the push service for the application.

	You can view the current application service status on the [**Product Management**](https://console.cloud.tencent.com/tpns) page. The service will be activated 30 minutes after you apply for a free trial or purchase the service.
	
	- If the following prompt is displayed, please check whether the application has been successfully registered with the push service as instructed in [verifying integration result](#jierujieguo).
	

<span id="jierujieguo"></span>

## Step 2: verify integration result

1. Run the application, filter logs by the "TPush" keyword, and view the displayed logs.
   ![](https://main.qcloudimg.com/raw/3534e6c05ab9f6959e6e19d4272dc48b.png)
   If a log similar to that shown in the preceding figure is displayed, the TPNS SDK has been successfully integrated as a plugin.
2. The log of a successful registration with the push service is as shown below:
```plaintext
XG register push success with token:6ed8af8d7b18049d9fed116a9db9c71ab4aabb65
```
If the token cannot be found, please check the error code returned by the registration API and troubleshoot as instructed in [Error Code](https://intl.cloud.tencent.com/document/product/1024/30722).

## Step 3: quickly integrate with vendor channel

1. On the **Configuration Management** page, enable the vendor push channel and configure the application information such as `AppId` and `SecretKey`. For more information about how to apply for such information, see the documentation of the vendor channel.
 - Click **View Documentation** to see the vendor channel description.
 - Configure the vendor channel at `AppId`, `AppKey`, and `AppSecret` on the right.
   ![](https://main.qcloudimg.com/raw/a3a2f1cdf2c09f087daded2ecc3e1dad.png)
2. After configuring the vendor channel information, click **Download Configuration Files** at the top of the page to download the vendor channel configuration file and use it to replace the legacy one in the project file.
 ![](https://main.qcloudimg.com/raw/4dfa37ac471c1c3b18cc559d5780a6be.png)

## Troubleshooting 

1. View plugin logs.
 If an exception occurs during integration, set the `debug` field in the `tpns-configs.json` file to `true` and run the following command: 
```
./gradlew --rerun-tasks :app:processReleaseManifest 
```
Then, use the `TpnsPlugin` keyword for analysis.
2. Click **sync projects**.
 ![](https://main.qcloudimg.com/raw/30368ed3cb4a25f3c33be46e3c1f2f5d.png)
3. Check whether there are relevant dependencies in the External Libraries of the project.
 ![](https://main.qcloudimg.com/raw/1de82d05f351939883e1870ae7300c44.png)
4. If the log displays `Execution failed for task ':Paracraft:checkTPNS'`, the TPNS Android SDK can be upgraded to a new version. If you do not want to check for updates, add `"upgrade": false` to the `tpns-configs.json` file, as shown below:
<img src="https://main.qcloudimg.com/raw/9eb6a2e108a7a4d1abdd10ef5c1cffdd.png" width="70%"></img>
