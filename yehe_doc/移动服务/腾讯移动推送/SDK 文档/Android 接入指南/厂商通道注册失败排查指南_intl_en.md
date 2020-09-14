## Problem Description
If your application is connected to a vendor channel, but a log entry similar to the following one is displayed in the application execution log: 
```
[OtherPushClient] handleUpdateToken other push token is :  other push type: huawei
```
It indicates that your application fails to register with the vendor channel. You can get the return code of the registration failure to locate and troubleshoot the problem.

## Troubleshooting Directions
### Getting vendor channel registration return code

The TPNS SDK for Android provides the following two methods to get the vendor channel registration return code:

- Method 1. Filter application execution logs by the keyword `OtherPush` to find the logs similar to the following ones in order to locate the return code for vendor channel registration:
   ```
   // Huawei channel
   // If no return codes can be found with the keyword `OtherPush`, try `HMSSDK`, and see return codes of `onResult ` or `onConnect`.
   [OtherPushHuaWeiImpl] other push huawei onConnect code:907135702
   
   // Mi channel
   [OtherPush_XG_MI] register failed, errorCode: 22022, reason: Invalid package name: com.xxx.xxx
   
   // Meizu channel
   [OtherPush_XG_MZ] onRegisterStatus BasicPushStatus{code='110000', message='Invalid appId'}
   
   // OPPO channel
   [OtherPushOppoImpl] OppoPush Register failed, code=14, msg=INVALID_APP_KEY
   
   // Vivo channel
   [OtherPushVivoImpl] vivoPush Register or UnRegister fail, code = 10003
   ```
   
- Method 2. Call the following API in the callback method of the TPNS registration API `XGPushManager.registerPush` to get the vendor channel registration return code:
   ```java
   /**
        * Get the return code for vendor channel registration failure
        *
        * @param context: application context
        * @return 0   : registration success
        *         Others: vendor channel registration return code
        *         -100: the vendor channel has been enabled, but no dependencies are added
        *         -101: the vendor channel has not been enabled
        * @since v1.1.5.4
        */
   XGPushConfig.getOtherPushErrCode(context);
   ```

    
### Troubleshooting with return code
You can view the specific meaning of return codes in the official documentation of the corresponding channel's push platform for troubleshooting. The following are some common error codes:
<table>
 <tbody><tr>
 <th>Vendor Channel</th>
 <th>Return Code</th>
 <th>Meaning</th>
 <th>Suggested Solution</th>
 <th>Official Return Code Document of Vendor Channel</th>
 </tr>
 <tr>
 <td rowspan="4">Huawei</td>
 <td>1001</td>
 <td>Please confirm that the Huawei Mobile Services or HMS-Core application has been installed on the phone, which is required for Huawei Push</td>
 <td>Download and install HMS-Core in Huawei AppGallery</td>
 <td rowspan="4"><a href="https://developer.huawei.com/consumer/cn/doc/development/HMS-Guides/push-faq-v4#h1-1577153305362-0" target="_blank">Huawei Return Code Description</a></td>
 </tr>
 <tr>
 <td>6003</td>
 <td>The APK file of the application is unsigned. A signature is required for Huawei Push</td>
 <td>Sign the APK file</td>
 </tr>
  <tr>
 <td>907135000</td>
 <td>The `appId` is invalid</td>
 <td>Check whether the application package name matches the `appId` on the Huawei Push platform</td>
 </tr>
  <tr>
 <td>907135702</td>
 <td>The SHA-256 value of the signature file is different from that configured on the Huawei Push platform</td>
 <td>Check whether the entered SHA-256 value of the signature file is the same as that configured on the Huawei Push platform (multiple SHA-256 values can be added)</td>
 </tr>
 <tr>
 <td rowspan="3">Mi</td>
 <td>22006</td>
 <td>The application ID is invalid</td>
 <td>Check whether the application package name, `appId`, and `appKey` match the configuration on the Mi Push platform</td>
 <td rowspan="3"><a href="https://dev.mi.com/console/doc/detail?pId=1557" target="_blank">Mi Return Code Description</a></td>
 </tr>
  <tr>
 <td>22007</td>
 <td>The application `Key` is invalid</td>
 <td>Check whether the application package name, `appId`, and `appKey` match the configuration on the Mi Push platform</td>
 </tr>
  <tr>
 <td>22022</td>
 <td>The application package name is invalid</td>
 <td>Check whether the application package name, `appId`, and `appKey` match the configuration on the Mi Push platform</td>
 </tr>
<tr>
 <td rowspan="2">Meizu</td>
 <td>110000</td>
 <td>The `appId` is invalid</td>
 <td>Check whether the application package name, `appId`, and `appKey` match the configuration in the application information on the <a href="https://push.meizu.com" target="_blank">Flyme Push</a> platform</td>
 <td rowspan="2"><a href="http://open-wiki.flyme.cn/doc-wiki/index#id?129" target="_blank">Meizu Return Code Description</a></td>
 </tr>
  <tr>
 <td>110001</td>
 <td>The `appKey` is invalid</td>
 <td>Check whether the application package name, `appId`, and `appKey` match the configuration on the Meizu Push platform</td>
 </tr>
 <tr>
 <td rowspan="2">OPPO </td>
 <td>14</td>
 <td>The `AppKey` parameter is invalid</td>
 <td>Be sure to enter the OPPO `AppKey` rather than `AppId` in `setOppoPushAppId` and `AppSecret` rather than `AppKey` in `setOppoPushAppKey`</td>
 <td rowspan="2"><a href="https://open.oppomobile.com/wiki/doc#id=10704" target="_blank">OPPO Return Code Description</a></td>
 </tr>
  <tr>
 <td>15</td>
 <td>The `AppKey` parameter is missing</td>
 <td>Add the `AppKey` parameter</td>
 </tr>
 <tr>
 <td rowspan="3">Vivo</td>
 <td>10003</td>
 <td>The application package name is different from that in the configuration</td>
 <td>Check whether the application package name, `appId`, and `appKey` match the configuration on the Vivo Push platform</td>
 <td rowspan="3"><a href="https://dev.vivo.com.cn/documentCenter/doc/368" target="_blank">Vivo Return Code Description</a></td>
 </tr>
  <tr>
 <td>10004</td>
 <td>The `appkey` does not match</td>
 <td>Check whether the application package name, `appId`, and `appKey` match the configuration on the Vivo Push platform</td>
 </tr>
  <tr>
 <td>10005</td>
 <td>The `appid` passed in is incorrect</td>
 <td>Check whether the application package name, `appId`, and `appKey` match the configuration on the Vivo Push platform</td>
 </tr>
<tr>
 </tbody></table>
 
### Other troubleshooting measures
- **Enable the push service on the Huawei Push platform for Huawei Push**
If you cannot get the Huawei token on the Huawei device, but the return code for vendor push channel registration is 0, please go to [Huawei Push](https://developer.huawei.com/consumer/cn/), enter the **Development** > **Push Service** page to check whether the push service for the application is enabled, and enter the **Development** > **Project Settings** > **API Management** page to check whether `Push Kit` and `App Messaging` are enabled.
The push service page is as shown below:

- **Enable the push service on the Mi Push platform for Mi Push**
If you cannot find the return code for Mi channel registration, please go to **[Mi Open Platform](https://dev.mi.com/console/appservice/push.html)** > **Push Operation Platform** and check whether the message push service for the application is enabled.

- **OPPO Push can be enabled officially only after your application is approved for the push service**
The push service page on the [OPPO Open Platform](https://open.oppomobile.com) displays the applications with/without the push service enabled. In the list of applications with the push service not enabled, click the target application to enter its push service page and click "Apply for Activation".

- **Vivo push can be enabled officially only after your application is approved for the push service**
Go to **[Vivo Open Platform](https://dev.vivo.com.cn/home)** > **Push Operation Platform**. In **Message Push** > **All Applications**, the created application is displayed in "Application Name". Click **Application Name**, select the target application, and click **Submit Application**.

>?It takes about 5 minutes for the push service of some vendors to take effect after being enabled. If the registration still fails after the push service is enabled, please wait a while and try again.

- **Huawei Mobile Services version is too old**
Search for log keyword "HMSSDK". If you see the value of `connect versionCod` is lower than that of `connect minVersion`, it indicates that the system uses an earlier "Huawei Mobile Services" or "HMS_Core" version. Please try to register again after upgrading.
```plaintext
I/HMSSDK_HuaweiApiClientImpl: ====== HMSSDK version: 20601301 ======
I/HMSSDK_HuaweiApiClientImpl: Enter connect, Connection Status: 1
E/HMSSDK_Util: In getHmsVersion, Failed to read meta data for the HMS VERSION.
I/HMSSDK_HuaweiApiClientImpl: connect minVersion:20600000
I/HMSSDK_HuaweiMobileServicesUtil: connect versionCode:20301306
D/HMSAgent: connect end:-1001
```


- **Vivo Push is not supported**
Vivo Push is only available in later models and systems. For more information, see [Vivo Push FAQs](https://dev.vivo.com.cn/documentCenter/doc/156#w1-08608733).
