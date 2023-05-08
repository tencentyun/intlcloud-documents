## Overview

This document describes how to quickly integrate the Tencent Push Notification Service SDK into your Android application. You can use the Tencent Push Notification Service on your application after performing the following steps.

>! To avoid your app from being criticized in a circulated notice or removed from the market by regulatory authorities, be sure to add mobile push related instructions in the Privacy Policy according to the Android Compliance Guide before integrating the Tencent Push Notification Service SDK and initialize the SDK after the user agrees to the Privacy Policy. 
>

## Preparing for Integration

### Creating an Android platform application
1. Before integrating the SDK, you need to log in to the [Tencent Push Notification Service console](https://console.cloud.tencent.com/tpns) and create the product and Android application. For detailed directions, please see [Creating Products and Applications](https://www.tencentcloud.com/document/product/1024/32603).
   ![](https://main.qcloudimg.com/raw/748fd7e885077735bdb631aab2bae2b7.png)
2. Go to the **Configuration Management** page of the application to prepare for the integration.
   ![](https://main.qcloudimg.com/raw/f2047b88c465df6abc36104253241cae.png)

## Starting Integration

1. On the **Configuration Management** page, click **Quick Integration**.
![](https://main.qcloudimg.com/raw/c45001ef6396382a83b73105f3a7214e.png)
2. Complete the configuration as instructed and click **Click to verify**.
![](https://main.qcloudimg.com/raw/910f9e03f0c609e847676ee2b62a7a66.png)
3. If the following prompt is displayed, the Tencent Push Notification Service SDK is successfully integrated.
	![](https://main.qcloudimg.com/raw/20dcdc160613bf6b8552a508891cbda5.png)
	If verification failure information as shown in the figure below is reported, check whether the application has been successfully registered with the Tencent Push Notification Service as instructed in [Verifying the Integration Result](#jierujieguo).
>!To increase the offline reach rate, the Tencent Push Notification Service SDK enables the session keep-alive feature by default. To disable the feature, see [here](https://www.tencentcloud.com/document/product/1024/32624#how-do-i-disable-the-keep-alive-feature-of-tpns.3F).



<span id="jierujieguo"></span>

## Verifying the Integration Result

1. Run the application, filter logs by the "TPush" keyword, and view the displayed logs.
   ![](https://main.qcloudimg.com/raw/3534e6c05ab9f6959e6e19d4272dc48b.png)
   If a log similar to that shown in the preceding figure is displayed, the Tencent Push Notification Service SDK has been successfully integrated as a plugin.
2. Check whether the registration with the push service is successful. The following log indicates successful registration.
```plaintext
XG register push success with token:6ed8af8d7b18049d9fed116a9db9c71ab4aabb65
```
If the token cannot be found, please check the error code returned by the registration API and troubleshoot as instructed in [Error Code](https://www.tencentcloud.com/document/product/1024/30722).

## Quickly Integrating with a Vendor Channel

1. On the **Configuration Management** page, enable the vendor push channel and configure the application information such as `AppId` and `SecretKey`. For more information about how to apply for such information, see the documentation of the vendor channel.
 - Click **View Documentation** to see the vendor channel description.
 - Configure `AppId`, `AppKey`, and `AppSecret` for the vendor channel.
   ![](https://main.qcloudimg.com/raw/a3a2f1cdf2c09f087daded2ecc3e1dad.png)
2. After configuring the vendor channel information, click **Download Configuration File** at the top of the page to download the vendor channel configuration file and use it to replace the legacy one in the project file.
 ![](https://main.qcloudimg.com/raw/4dfa37ac471c1c3b18cc559d5780a6be.png)

## Troubleshooting

1. View the Android Gradle plugin logs.
 If an exception occurs during integration, set the `debug` field in the `tpns-configs.json` file to `true` and run the following command: 
```
./gradlew --rerun-tasks :app:processReleaseManifest 
```
Then, use the `TpnsPlugin` keyword for analysis.
2. Click the **sync projects** icon.
 ![](https://main.qcloudimg.com/raw/30368ed3cb4a25f3c33be46e3c1f2f5d.png)
3. Check whether relevant dependencies exist in **External Libraries** of the project.
 ![](https://main.qcloudimg.com/raw/1de82d05f351939883e1870ae7300c44.png)
4. If the log displays `Execution failed for task ':Paracraft:checkTPNS'`, the Tencent Push Notification Service Android SDK can be updated to a later version. If you do not want to check for updates, add `"upgrade": false` to the `tpns-configs.json` file, as shown below:
<img src="https://main.qcloudimg.com/raw/9eb6a2e108a7a4d1abdd10ef5c1cffdd.png" width="70%"></img>
5. If you encounter the version mismatch between the Android Gradle plugin and Gradle version when using the plugin, upgrade the Gradle version by referring to [Android Gradle plugin release notes](https://developer.android.google.cn/studio/releases/gradle-plugin). The table in following figure lists which version of Gradle is required for each version of the Android Gradle plugin.
![](https://main.qcloudimg.com/raw/dcdce69e543adef9d752ef216249da06.png)
