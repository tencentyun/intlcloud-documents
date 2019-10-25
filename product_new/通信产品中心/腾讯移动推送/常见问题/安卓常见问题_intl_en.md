# Android FAQs
<hr>

#### Cannot receive notification message?

Use the token you get and push [in the console](https://console.cloud.tencent.com/tpns). If you cannot receive the push, troubleshoot as follows. Make sure the SDK version is the latest version. If the issue occurs in the older version, it may have already been solved in the new version. If you encounter a web-side push error, refresh the page and try again.

#### Why cannot I receive push messages after a successful registration?

* Check whether the current application package name is the same as the application package name entered when registering for TPNS. If not, we recommend you enable push with multi-package names.
* Check whether the mobile network has any exceptions and switch to 4G network for testing.
* TPNS push includes "notification panel message" and "in-app message" (passthrough message). A notification panel message can be displayed in the notification panel, while an in-app message cannot.
* Confirm that the phone is in normal mode. In low power or do not disturb mode, some phones may restrict the network and activity of the backend TPNS process.
* Check whether notification panel message is allowed on the phone. 

#### Why device registration fails?

* Data synchronization for newly created app will take about one minute. During this period, the registration may return the error code 20. You can retry later.

**\[Parameters are incorrectly entered\]**

* Check whether the access id and access key are correctly configured. Common errors are that secret key is misused or access key contains spaces.

**\[Registration returns an error\]**

* If the console returns error codes such as **10004**, **10002**, and **20**, see [Android SDK error codes]

**\[Registration has no callback\]**

* Check the current network condition. We recommend you use 4G network for testing. Wi-Fi used by many users may have insufficient network bandwidth.

#### Why cannot I receive push messages after exiting the app?

* Third-party push services currently cannot guarantee that you can still receive the push after closing the app. This is because the mobile phone customs ROM to limit TPNS service. All activities of TPNS depend on the internet connection and normal operation of TPNS service. After the service is terminated, the system, security programs and user operations determine whether the service can be restarted.
* QQ and WeChat are system-level app whitelist, and the relevant service will not terminate after you exit the app, so the user can still receive messages after exiting the app, and the relevant service can still survive in the backend.
* In Android, after you exit the app and the TPNS service is disconnected from the TPNS server, messages delivered to the device will become offline messages, which can be retained for up to 72 hours. If there are multiple offline messages, only two can be retained in each device. If messages are pushed after the app is closed, please check whether the unregistration API has been called if you cannot receive the message when launching the app: XGPushManager.unregisterPush\(this\).

### How do I configure message clicking event and page redirection methods?

In SDK, a click on a message can trigger a click event, which by default opens the main interface. Therefore, if a redirect action is configured in **onNotificationClickedResult** callback method on the device, there is a conflict between the custom redirect and the default click event. The user will be redirected to the specified page and then  to the main page. Thus, you cannot configure redirect in **onNotificationClickedResult**.

**Solutions are as below \(we recommend the first method\):**

**\[1\] Use Intent to redirect to the specified page**

* You need to configure which page to redirect to on the manifest of the client app, for example, if you want to redirect to AboutActivity, specify the following page:

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
* If you use the TPNS console to set the intent for redirection, enter as follows:

![](https://main.qcloudimg.com/raw/5c7339b703864377ed2bc6463faddce1.png)

* If you use the server SDK to set the intent for redirection, you can set the intent as (take Java SDK as an example):
```
action.setIntent("xgscheme://com.xg.push/notify_detail");
```
* If you want to include parameters such as param1 and param2, you can set as follows:
```
action.setIntent("xgscheme://com.xg.push/notify_detail?param1=aa&param2=bb");
```

* Get the parameters on the device:
1. In the onCreate method of the page that you specify for redirection:
```
Uri uri = getIntent().getData();
    if (uri != null) {                
String url = uri.toString();
String p1= uri.getQueryParameter("param1");
String p2= uri.getQueryParameter("param2");
 }
```
2. If the parameters passed in contain special characters such as # and &:
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

**\[2\] When delivering the message, set the page to redirect to upon message click**

(a) You can set the deeplink (package name + class name) directly in web-based advanced functions;

(b) Set the SetActivity method (package name + class name) of the Action field in the Message class in the backend, and get the message content through XGPushClickedResult, including title, content, and additional parameters.

* The method of setting the page to redirect to in the backend is as follows (take Java SDK as an example):

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
// this must be the context of the page to redirect to upon click.
XGPushClickedResult clickedResult = XGPushManager.onActivityStarted(this);
// Get the parameters near the message
String ster = clickedResult.getCustomContent();
// Get the message title
String set = clickedResult.getTitle();
// Get the message content
String s = clickedResult.getContent();

```
**\[3\] Send in-app message to the device, the user can customize the notification panel, use local notification push, and set the page to redirect to**

