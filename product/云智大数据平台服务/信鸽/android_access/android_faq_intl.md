## Pushes cannot be received

Use the token obtained to push at [TPNS' official website](http://ixg.qq.com/). Please troubleshoot according to conditions described below if pushes cannot be received. Make sure you have the latest  SDK version, because issues in the old version may have been fixed in the latest version. Try refreshing the webpage if error occurs in website push.

### Registration succeeded but pushes cannot be received

* Please check whether the current app package name is the same as that entered when TPNS is registered. If not, it is recommended to enable multi-package name push when pushing.
* Check whether the network is exceptional on the phone and switch to 4G network for testing.
* TPNS push is divided into "notification bar message" and "in-app message" (passthrough message). A notification bar message can be displayed in the notification bar, while an in-app message cannot.
* Confirm that the phone is in normal mode. Some phones may have restrictions on network and activity of the backend TPNS process when in Low Power or Do Not Disturb mode.
* Check whether the notification bar permission is granted on the phone. On some OPPO and Vivo phones, the notification bar permission has to be granted manually.

### Registration failed and pushes cannot be received

* A newly created app will have a data synchronization process of about one minute. During this period, the registration may return error code 20. You can simply retry later.

**\[Parameters are incorrectly entered\]**

* Check whether the access id and access key are correctly configured. Common errors are the secret key is misused or the access key contains spaces.

**\[Registration returned an error\]**

* If the console returns an error code such as "10004", "10002", or "20", please see [Android SDK Error Codes](https://intl.cloud.tencent.com/document/product/1024/30722).

**\[Registration had no callback\]**

* Check whether 
**wup package** is added.
* Check whether the current 
**network condition**
 is good. It is recommended to use 4G network for testing. Wi-Fi may cause insufficient network bandwidth due to excessive users.
* **Nubia phones**
  Models that were released in the second half of 2015 and 2016 cannot be registered, including "Nubia Z11 series", "Nubia Z11S series", and "Nubia Z9S series". Models that can be registered are all previous ones, including "Z7 series" and "My Prague series" (this issue is found in TPNS v2.47 and 3.X).

### After the app is closed, pushes cannot be received

* At present, third-party push services cannot guarantee that the pushes can be received after the app is closed. This is due to the limitation of the mobile phone's custom ROM on the TPNS service. All activities of TPNS are on the basis that the TPNS service can connect to the internet and run properly. After the service is terminated, whether it can be restarted depends on the system settings, security programs, and user operations.
* QQ and WeChat are in the system-level app whitelist, and the relevant service will not exit after the app is closed, so the user can still receive messages after closing the app, and in fact, the relevant service survives in the backend.
* On Android, after the app is closed and the TPNS service is disconnected from the TPNS server, the message delivered to the device will become an offline message, which can be retained for up to 72 hours. If there are multiple offline messages, up to two of them can be retained. If messages pushed after the app is closed cannot be received after the app is opened again, please check whether the unregistration API is called: XGPushManager.unregisterPush\(this\).

### Account pushes cannot be received

Account, also known as alias, refers to the user account of an app with account login function. This is not only for QQ or WeChat, and all accounts of the user are supported. For example, the account of Mobile QQ is QQ account number, the account of Gmail is the email address, and the account of China Mobile is the mobile number.

For users to whom pushes are to be made based on the account, you need to bind the account to the token first; otherwise, pushes will fail. On Android, account binding is performed upon registration, namely through the registerPush\(context,account\) API. On iOS, it is configured through setAccount.

* When selecting account push, if the system prompts "Token not found, check registration", it means that the account is not associated with the token. There are two possible reasons for this:

(1) The account or alias is unregistered. It is not necessarily due to app call, in some cases, the unregistration may be triggered automatically.

(2) The device is registered with another account or alias, which will automatically unbind the original one. (One device can only correspond to one alias. If there is no device under the current alias, there will certainly be a "not found" error.)

* After the account is bound, you can deliver a notification by specifying the alias (account). Normally, all devices that have recently logged in to this account can receive the notification. When the user account is logged out, call registerPush\(context,"\*"\) to unbind the current account.
* Account (alias) cannot contain only one single character. One account can be bound to up to 100 devices. Only the last bound device can receive pushes.

### Tag pushes cannot be received

Please check whether the tag is successfully bound. An app can have up to 10,000 tags, each token can have up to 100 tags in one app, and no spaces are allowed in the tag.

* **Use the server push SDK to query the tag and token binding**

```php
/**
     * Query the token tag
     */
public function QueryTokenTags($deviceToken)
    {
        $ret = array('ret_code' => -1);
        if (!is_string($deviceToken)) {
            $ret['err_msg'] = 'deviceToken is not valid';
            return $ret;
        }
        $params = array();
        $params['access_id'] = $this->accessId;
        $params['device_token'] = $deviceToken;
        $params['timestamp'] = time();

        return $this->callRestful(self::RESTAPI_QUERYTOKENTAGS, $params);
    }
```
## Issues with push data

**\[Push is paused\]**

* Full push limitations (V2, V3):
  1. You can create up to 30 pushes per hour for full push, and excessive ones will fail.
  2. Full push of the same content can be performed only once per hour, and excessive ones will fail.

* Tag push limitations (V3):
  1. The same app can create up to 30 tag pushes per hour, and excessive ones will fail.
  2. Push of the same content with the same tag can be performed only once per hour, and excessive ones will fail.


**\[Effect statistics\]**

* Next day: The push data can be viewed the next day after pushed
* Real-time: The push data can be viewed immediately after pushed. Currently, up to 14 times of real-time statistics collection are supported per week.

**\[Actually delivered pushes\]**

* During the offline retention period of the message, there will be successful connections to the TPNS server and normally delivered pushes. (For example, if the message is retained offline for 3 days, the actually delivered data will stabilize on the fourth day, and the data will increase as more devices are turned on and connected to the TPNS server.)

**\[Historical details\]**

* Historical details only show full pushes, tag pushes, and number package pushes at the official website. (Currently, push details cannot be displayed for batch accounts or batch devices.)

**\[Data overview\]**

* It shows the data of the day. The data of a specific day is the total amount of pushes by various push actions on that day. (There are four types of pushes: unicast, broadcast (i.e., batch push and full push), notification bar message, and in-app message.)

## Message tap event and page redirection method

---

Since tapping a message generates a tap event by default in the current SDK, the default tap event is to open the main interface. Therefore, if a redirection action is set in the onNotifactionClickedResult method of the device message tap callback, the custom redirection will conflict with the default tap event. The result is that after tapping, the user will be redirected to the specified interface and then returned to the main interface. As a result, you cannot set redirection in onNotifactionClickedResult.

**Below lists the solutions \(the first one is recommended\):**

**\[1\] Use Intent to redirect to the specified page (this method is for Android 3.2.3 and higher)**

* You need to configure the page to redirect to on the client app's manifest, for example, if you want to redirect to AboutActivity, specify the following page:

```
<activity
android:name="com.qq.xg.AboutActivity"
android:theme="@android:style/Theme.NoTitleBar.Fullscreen" >
<intent-filter >
<action android:name="android.intent.action.VIEW" />
<category android:name="android.intent.category.DEFAULT"/>
<data android:scheme="xgscheme"
android:host="com.xg.push"
android:path="/notify_detail" />
</intent-filter>
</activity>
```
* If you use the TPNS console to set the intent for redirection, enter in the following way:

![](https://main.qcloudimg.com/raw/91801529d911bc58f7aff2956af1d3f6.png)

* If you use the server SDK to set the intent for redirection, you can set the intent to the following (with the Java SDK as an example):
```
action.setIntent("xgscheme://com.xg.push/notify_detail");
```
* If you want to bring parameters such as param1 and param2, you can set as below:
```
action.setIntent("xgscheme://com.xg.push/notify_detail?param1=aa&param2=bb");
```

* Get the parameters on the device:
1. In the onCreate method of the page you specify for redirection to:
```
Uri uri = getIntent().getData();
    if (uri != null) {                
String url = uri.toString();
String p1= uri.getQueryParameter("param1");
String p2= uri.getQueryParameter("param2");
 }
```
2. If the passed parameters contain special characters such as # and &,
they can be parsed by using the following method:
```
Uri uri = getIntent().getData();
    if (uri != null) {                
 String url = uri.toString();
 UrlQuerySanitizer sanitizer = new UrlQuerySanitizer();
 sanitizer.setUnregisteredParameterValueSanitizer(UrlQuerySanitizer.getAllButNulLegal());
   sanitizer.parseUrl(url);
   String value1 = sanitizer.getValue("key1");
   String value2 = sanitizer.getValue("key2");
   Log.i("XG" , "value1 = " + value1 + " value2 = " + value2);
}
```

**\[2\] Set the page to redirect to upon message tap when delivering the message**

(a) You can set the deeplink (package name + class name) directly in the web-based advanced functions;

(b) Set the SetActivity method (package name + class name) of the Action field in the Message class in the backend, and get the relevant content of the message through XGPushClickedResult: title, content, and additional parameters.

* The method of setting the page to redirect to in the backend is as follows (with the Java SDK as an example):

```js
......
XingeApp android = new XingeApp(accessID,secretkey);
Message message_android =new Message();
message_android.setExpireTime(86400);
message_android.setTitle("TPNS");
message_android.setType(1);
message_android.setContent("android test2");
ClickAction action =new ClickAction();
action.setActivity("com.qq.xgdemo.activity.SettingActivity");
message_android.setAction(action);
JSONObject ret1 = android.pushSingleDevice("token",message_android);
......
```

* The method of getting the Message parameter on the device is as follows:

```
// this must be the context of the page to redirect to upon tap.
XGPushClickedResult clickedResult = XGPushManager.onActivityStarted(this);
// Get the parameters near the message
String ster = clickedResult.getCustomContent();
// Get the message title
String set = clickedResult.getTitle();
// Get the message content
String s = clickedResult.getContent();

```
**\[3\] Send in-app message to the device; the user-defined notification bar uses local notification pop-up to set the page to redirect to**



## FAQs for TPNS Android SDK integration with vendor-specific channels

### Functions supported by vendor-specific channels

- Mi channel supports arrival callback and passthrough, but not tap callback.
- Huawei channel supports tap callback (requiring custom parameters) and passthrough (ignoring custom parameters), but not arrival callback.
- Meizu channel supports arrival callback and tap callback, but not passthrough.

**Note: If you need to get parameters through tap callback or redirect to a custom page, you can use the Intent to do so. Click [here](https://intl.cloud.tencent.com/document/product/1024/30720) to view the tutorials.**

### The problem of otherpushToken = null that may be encountered during debugging
* For 4.X otherpush version, check whether the vendor-specific channel initialization code is enabled, and add the following to your app's attachBaseContext function:

 ```
 StubAppUtils.attachBaseContext(context);
 ```
* For 4.X otherpush version, after the cloud controller successfully downloads the vendor's dex package for the corresponding device, you need to kill the app process and restart the app to complete the registration. The downloaded log is as follows:
  ```xml
10-25 15:16:31.067 16551-16551/? D/XINGE: [DownloadService] onCreate()
10-25 15:16:31.073 16551-16757/? D/XINGE: [DownloadService] action:onHandleIntent
10-25 15:16:31.083 16551-16757/? V/XINGE: [CloudCtrDownload] Create downloadControl
10-25 15:16:31.089 16551-16757/? I/XINGE: [CloudCtrDownload] action:download - url:https://pingjs.qq.com/xg/Xg-Xm-plug-1.0.2.pack, saveFilePath:/data/user/0/com.qq.xgdemo1122/app_dex/XG/5/, fileName:Xg-Xm-plug-1.0.2.pack
10-25 15:16:31.097 16551-16757/? V/XINGE: [CloudCtrDownload] Download file: Xg-Xm-plug-1.0.2.pack
10-25 15:16:31.641 16551-16757/? D/XINGE: [DownloadService] download file Succeed
10-25 15:16:31.650 16551-16757/? D/XINGE: [CloudCtrDownload] Download succeed.
10-25 15:16:31.653 16551-16551/? D/XINGE: [CloudControlDownloadReceiver] onReceive
10-25 15:16:31.673 16551-16738/? I/test: Download file SuccessXg-Xm-plug-1.0.2.pack to /data/user/0/com.qq.xgdemo1122/app_dex/XG/5/
  ```
```
* If the dex configuration package cannot be downloaded at all, you can use the non-dynamic loading method to integrate it. In this case, you need to use the TPNS v4.X jar without the vendor-specific channels and then integrate the jars of each vendor-specific channel. For more information about how to integrate, see the relevant document.


**\[Troubleshooting for Mi channel\]**

* Check whether the TPNS SDK is v3.2.0 or higher.
* Check the manifest file configuration according to the development documentation, especially the places where the package name needs to be modified.

```
<permission android:name="com.example.mipushtest.permission.MIPUSH_RECEIVE" android:protectionLevel="signature" />
<!-- Here, change com.example.mipushtest to the app package name -->
<uses-permission android:name="com.example.mipushtest.permission.MIPUSH_RECEIVE" />
<!-- Here, change com.example.mipushtest to the app package name -->
```

* Check whether you have set the APPID and APPKEY of Mi before the registration and whether the third-party push has been started.

```
// Enable the third-party push
XGPushConfig.enableOtherPush(this,true);
// Set the Appid and Appkey of Mi
XGPushConfig.setMiPushAppId(this,MIPUSH_APPID);
XGPushConfig.setMiPushAppKey(this,MIPUSH_APPKEY);
```

* Check whether the app package name is the same as that registered with Mi open push platform and TPNS console.


* Listen to the registration result of Mi by implementing the custom broadcast that inherits PushMessageReceiver and check the registration return code.
* Start logcat, observe the log with the tag of PushService to see what error message is present.

**\[Troubleshooting for Huawei channel\]**

* Check whether the TPNS SDK is v3.2.0 or higher and whether the version in **Settings** -> **Application Management** -> **Huawei Mobile Service** on the Huawei phone is higher than 2.5.3.
* Check the manifest file configuration according to the Huawei channel access guide in the development documentation.
* Check whether the third-party push has been started before the TPNS registration and whether the Huawei APPID is configured correctly.
* Check whether the app package name is the same as that registered with Huawei Push's official website and TPNS console.
* Call XGPushConfig.setHuaweiDebug\(true\) before registering the code, manually confirm that the storage permission is granted to the app, check the reason of error of Huawei registration failure outputted in the huawei.txt file in the SD card directory, and then find the cause corresponding to the error code in Huawei development documentation.
* In cmd, run adb shell setprop log.tag.hwpush VERBOSE and
  adb shell logcat -v time &gt; D:/log.txt to start to capture the log, test, and then close the cmd window. Send the log to technical support.

**\[Troubleshooting for Meizu channel\]**

* Similar to the troubleshooting method for Mi channel. For more information, see troubleshooting for Mi channel.






```