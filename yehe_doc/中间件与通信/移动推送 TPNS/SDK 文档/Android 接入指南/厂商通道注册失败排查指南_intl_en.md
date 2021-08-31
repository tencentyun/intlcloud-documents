## Problem Description

If your application is connected to a vendor channel, but a log similar to the following one is found in the application operation logs: 

```
[OtherPushClient] handleUpdateToken other push token is :  other push type: huawei
```

Then it means that your application failed to register with the vendor channel. You can locate and troubleshoot the problem by getting the return code for vendor channel registration failure.

## Troubleshooting Directions

### Getting the return code for vendor channel registration

TPNS SDK for Android provides the following ways to get the return code for vendor channel registration:

Filter application operation logs by the keyword `OtherPush` to find logs similar to the following ones and locate the return code for vendor channel registration:

```
// Huawei channel
// If filtering by the keyword `OtherPush` cannot find the return code, you can try the keyword `HMSSDK` and find the return code after `onResult` or `onConnect`
[OtherPushHuaWeiImpl] other push huawei onConnect code:907135702

n// Mi channel
[OtherPush_XG_MI] register failed, errorCode: 22022, reason: Invalid package name: com.xxx.xxx

// Meizu channel
[OtherPush_XG_MZ] onRegisterStatus BasicPushStatus{code='110000', message='Invalid appId'}

// OPPO channel
[OtherPushOppoImpl] OppoPush Register failed, code=14, msg=INVALID_APP_KEY

// vivo channel
[OtherPushVivoImpl] vivoPush Register or UnRegister fail, code = 10003
```

### Troubleshooting by return code

You can refer to the official push documentation of each vendor to get the specific descriptions of return codes and troubleshoot accordingly. The table below lists some common error codes:

<table>
 <tbody><tr>
 <th>Vendor Channel </th>
 <th>Return Code </th>
 <th>Description </th>
 <th>Suggested Solution </th>
 <th>Link </th>
 </tr>
 <tr>
 <td rowspan="5">Huawei </td>
 <td>1001 </td>
 <td>Make sure that the "HMS" or "HMS-Core" application is installed in the phone, which is required for Huawei Push </td>
 <td>Go to Huawei AppGallery to download and install the "HMS-Core" application </td>
 <td rowspan="5"><a href="https://developer.huawei.com/consumer/cn/doc/development/HMS-Guides/push-faq-v4#h1-1577153305362-0" target="_blank"> Huawei return codes</a> </td>
 </tr>
 <tr>
 <td>6003 </td>
 <td>The application APK is not signed or contains signing information that doesn't match that registered on the Huawei Developer platform; however, it must be correctly signed for Huawei Push</td>
 <td>Sign the APK file or check whether the signing information is correct<a href="https://intl.cloud.tencent.com/document/product/1024/37176">Configuring the signature certificate fingerprint for the Huawei channel</a> </td>
 </tr>
  <tr>
 <td>907135000 </td>
 <td>The `appId` is invalid</td>
 <td><li>Check whether the value of the `appId` field in the Huawei Push configuration file `agconnect-services.json` matches the application package name
      <li>Check whether the configuration file is in the root directory of the project's `app` module (at the same level as the `build.gradle` file of the application) </td>
 </tr>
  <tr>
 <td>907135702 </td>
 <td>The SHA256 value of the signature file is different from that configured on the Huawei Push platform </td>
 <td>Check whether the entered SHA256 value of the signature file is the same as the one configured on the Huawei Push platform (multiple ones can be added)</td>
 </tr>
 <tr>
 <td>907135003 </td>
 <td>The `apiclient` object is invalid </td>
 <td> <li> Check whether the phone can access the internet normally or reconnect it to the network
       <li> This problem is most probably caused by version incompatibility of the HMS-Core application on Huawei phones. You can try searching for HMS-Core or Huawei Mobile Service in Huawei AppGallery, check whether the latest version is installed, and if not, upgrade it</td>
 </tr>
 <tr>
 <td rowspan="3">Mi </td>
 <td>22006 </td>
 <td>The application ID is invalid</td>
 <td>Check whether the application package name, `appId`, and `appKey` match each other on the Mi Push platform  </td>
 <td rowspan="3"><a href="https://dev.mi.com/console/doc/detail?pId=1557" target="_blank"> Mi return codes</a> </td>
 </tr>
  <tr>
 <td>22007 </td>
 <td>The application key is invalid </td>
 <td>Check whether the application package name, `appId`, and `appKey` match each other on the Mi Push platform </td>
 </tr>
  <tr>
 <td>22022 </td>
 <td>The application package name is invalid</td>
 <td>Check whether the application package name, `appId`, and `appKey` match each other on the Mi Push platform </td>
 </tr>
<tr>
 <td rowspan="2">Meizu </td>
 <td>110000 </td>
 <td>The `appId` is invalid</td>
 <td>Check whether the application package name, `appId`, and `appKey` match each other on the Meizu Push platform. ⚠️Check the application information on the <a href="https://push.meizu.com" target="_blank"> Flyme Push</a> platform </td>
 <td rowspan="2"><a href="http://open-wiki.flyme.cn/doc-wiki/index#id?129" target="_blank"> Meizu return codes</a> </td>
 </tr>
  <tr>
 <td>110001 </td>
 <td>The `appKey` is invalid </td>
 <td>Check whether the application package name, `appId`, and `appKey` match each other on the Meizu Push platform </td>
 </tr>
 <tr>
 <td rowspan="2">OPPO </td>
 <td>14 </td>
 <td>The `AppKey` parameter is invalid</td>
 <td>Please note that OPPO's `AppKey` instead of `AppId` should be entered for `setOppoPushAppId`, while OPPO's `AppSecret` instead of `AppKey` should be entered for `setOppoPushAppKey`  </td>
 <td rowspan="2"><a href="https://open.oppomobile.com/wiki/doc#id=10704" target="_blank"> OPPO return codes</a> </td>
 </tr>
  <tr>
 <td>15 </td>
 <td>The `AppKey` parameter is missing </td>
 <td>Enter the `AppKey` parameter </td>
 </tr>
 <tr>
 <td rowspan="3">vivo </td>
 <td>10003 </td>
 <td>The application package name does not match the configured one</td>
 <td>Check whether the application package name, `appId`, and `appKey` match each other on the vivo Push platform  </td>
 <td rowspan="3"><a href="https://dev.vivo.com.cn/documentCenter/doc/368" target="_blank"> vivo return codes</a> </td>
 </tr>
  <tr>
 <td>10004 </td>
 <td>The `appKey` is incorrect </td>
 <td>Check whether the application package name, `appId`, and `appKey` match each other on the vivo Push platform </td>
 </tr>
  <tr>
 <td>10005 </td>
 <td>The `appId` is incorrect</td>
 <td>Check whether the application package name, `appId`, and `appKey` match each other on the vivo Push platform </td>
 </tr>
<tr>
 </tbody></table>





### Troubleshooting other issues

- **For Huawei Push, the push service needs to be enabled on the Huawei Push platform**
  If you cannot get the Huawei token on your Huawei device, and the return code for vendor push channel registration is 0, then please go to the [Huawei Push platform](https://developer.huawei.com/consumer/cn/), check whether the push service is enabled for the application on the **Development** -> **Push Service** page and whether `Push Kit` and `App Messaging` are enabled on the **Development** -> **Project Settings** -> **API Management** page.

- **For Mi Push, the push service needs to be enabled on the Mi Push platform**
  If you cannot find the return code for Mi channel registration, please check whether the application's message push service is enabled on **[Mi Open Platform](https://dev.mi.com/console/appservice/push.html)** -> **Push Platform**.

- **For OPPO Push, the push feature needs to be enabled first before messages can be pushed**
  On the push service page on [OPPO Open Platform](https://open.oppomobile.com), you can view applications with the service enabled and those not enabled. Among those not enabled, click the one for which you want to apply for push permission to enter the push service page and apply for enablement accordingly.
- **For vivo Push, the push feature needs to be enabled first before messages can be pushed**
  Go to **[vivo Open Platform](https://dev.vivo.com.cn/home)** -> **Push Platform** -> **Message Push** -> **All Applications, click **Application Name** to select the target application among all the created applications, and click **Submit Application**.

 > ?For some vendors, the push service will take effect around 5 minutes after it is enabled. If registration still fails after the push service is enabled, please wait a while and try again.

- **The HMS version is too low**
  Search for the keyword "HMSSDK" in the logs, and if a log similar to the following one is found, that is, `connect versionCode` is lower than `connect minVersion`, then it means that the system application "HMS" or "HMS_Core" is too old. Please retry registering after upgrading the application.
```plaintext
I/HMSSDK_HuaweiApiClientImpl: ====== HMSSDK version: 20601301 ======
I/HMSSDK_HuaweiApiClientImpl: Enter connect, Connection Status: 1
E/HMSSDK_Util: In getHmsVersion, Failed to read meta data for the HMS VERSION.
I/HMSSDK_HuaweiApiClientImpl: connect minVersion:20600000
I/HMSSDK_HuaweiMobileServicesUtil: connect versionCode:20301306
D/HMSAgent: connect end:-1001
```

- **Some vivo models do not support the push service**
  vivo Push is supported only on certain newer models and corresponding OS versions. For more information, please see [here](https://dev.vivo.com.cn/documentCenter/doc/156#w1-08608733).

