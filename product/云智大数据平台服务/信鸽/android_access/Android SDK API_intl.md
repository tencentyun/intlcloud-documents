# APIs

<hr>

## API Overview



The package name path prefix for all APIs is: ```com.tencent.android.tpush```. There are several important classes that provide APIs, including:

| Class name | Description |
|-------|-----|
|```XGPushManager```| Push service push |
|```XGPushConfig```| Push service configuration item API |
|```XGPushBaseReceiver```| Receiver to receive messages and result feedback, which needs to be statically registered in ```AndroidManifest.xml``` by yourself |

### XGPushManager Function Class

```XGPushManager``` provides a list of APIs of TPNS. The default method is ```public static``` type.

| Prototype | Function |
|:----------|:--------|
|```void registerPush(Context context)```| Start and register (no registration callback) |
|```void registerPush (```<br>```Context context,``` <br>```final XGIOperateCallback callback```<br>```)```| Start and register (with registration callback) |
|```void registerPush(``` <br> ```Context context,``` <br> ``` String account, ``` <br> ```XGIOperateCallback callback``` <br> ```)``` | Start and register the app, and bind the account at the same time. <br>Recommended for apps with an account system <br>(Used for versions below 3.2.2; there is registration callback) |
|```void bindAccount(``` <br> ```Context context, ``` <br> ```String account, ``` <br> ```XGIOperateCallback callback``` <br> ```)``` | Start and register the app, and bind the account at the same time. <br>Recommended for apps with an account system <br>(Used for version 3.2.2 and higher; <br>this API will override the account previously bound to the device; and only the currently registered account will take effect) |
|```void bindAccount(``` <br> ```Context context,``` <br> ``` final String account``` <br> ```)``` | Start and register the app, and bind the account at the same time. <br>Recommended for apps with an account system <br>(Used for version 3.2.2 and higher; this API will override the account previously bound to the device; <br>and only the currently registered account will take effect. There is no registration callback) |
| ```void appendAccount(``` <br> ```Context context,``` <br> ``` String account, ``` <br> ```XGIOperateCallback callback``` <br> ```)``` | Start and register the app, and bind the account at the same time. <br>Recommended for apps with an account system <br>(Used for version 3.2.2 and higher; this API will retain the previous account and only perform an addition operation. <br>A maximum of 10 accounts is allowed for one token; if this limit is exceeded, the previously bound account will be automatically replaced. There is registration callback) |
| ```void appendAccount(``` <br> ```Context context,``` <br> ``` final String account``` <br> ```)``` | Start and register the app, and bind the account at the same time. <br>Recommended for apps with an account system <br>(Used for version 3.2.2 and higher; <br>this API will retain the previous account and only perform an addition operation. <br>A maximum of 10 accounts is allowed for one token; if this limit is exceeded, the previously bound account will be automatically replaced. There is no registration callback) |
| ```void delAccount(``` <br> ```Context context,``` <br> ``` final String account, ``` <br> ```XGIOperateCallback callback``` <br> ```)```  | Unbind the specified account (used for version 3.2.2 and higher; there is registration callback) |
| ```void delAccount(``` <br> ```Context context,``` <br> ``` final String account``` <br> ```)``` | Unbind the specified account (used for version 3.2.2 and higher; there is no registration callback) |
|```void registerPush(``` <br> ```Context context,``` <br> ```String account, ``` <br> ```String ticket, ``` <br> ```int ticketType,``` <br> ``` String qua, ``` <br> ```final XGIOperateCallback callback``` <br> ```)```| Same as above, only for use by businesses containing an login state |
|```void unregisterPush(Context context)```| Unregister; it is recommended to call when there is no need to receive pushes |
|```void setTag(``` <br> ```Context context,``` <br> ```String tagName``` <br> ```)```| Set a tag |
|```void setTags(```<br>```Context context, ```<br>```String operateName, ```<br>```Set<String> tags```<br>```) ```| Set multiple tags, which will override the tags previously set for this device (used for version 4.0.3 and higher) |
|```void addTags(```<br>```Context context, ```<br>```String operateName, ```<br>```Set<String> tags```<br>```)```| Add multiple tags (used for version 4.0.3 and higher)|
|```void deleteTag(``` <br> ```Context context,``` <br> ```String tagName``` <br> ```)```| Delete a tag |
|```void deleteTags(``` <br> ```Context context, ``` <br> ```String operateName, ``` <br> ```Set<String> tags``` <br> ```)```| Delete multiple tags (used for version 4.0.3 and higher) |
|```void cleanTags(``` <br> ```Context context, ``` <br> ```String operateName``` <br> ```)```| Clear all tags (used for version 4.0.3 and higher) |
|```XGPushClickedResult onActivityStarted(Activity activity)```| Statistics of effects when Activity is opened; get the delivered custom key-value |
|```void onActivityStoped(``` <br> ```Activity activity``` <br> ```)```| Statistics of effects when Activity is opened |
|```void setPushNotificationBuilder(``` <br> ```Context context, ``` <br> ```int notificationBulderId, ``` <br> ```XGPushNotificationBuilder notifiBuilder``` <br> ```)```| Customize local notification style |
|```long addLocalNotification(``` <br> ```Context context, ``` <br> ```XGLocalMessage msg``` <br> ```)```| Local notification |
|```boolean isNotificationOpened(``` <br> ```Context context``` <br> ```)```| Check whether the notification bar is closed |
|```void cancelNotifaction(Context context, int id)```| Clear a single notification |
|```void cancelAllNotifaction(Context context)```| Clear all notifications in the notification bar |

### XGPushConfig Configuration Class

```XGPushConfig``` provides a list of configuration APIs of TPNS. The default method is ```public static``` type. The ```set``` and ```enable``` methods provided for this class can take effect only if called before the ```XGPushManager`` API.

| Prototype | Function |
|-----|-----|
|```void enableDebug(```<br> ```Context context,``` <br> ```boolean debugMode``` <br> ```)```| Whether to enable debugging mode, i.e. outputting the logcat log; important note: in order to ensure data security, it must be set to false before publishing |
|boolean setAccessId(Context context,long accessId)| Configure accessId |
|boolean setAccessKey(Context context,String accessKey)| Configure accessKey |
|String getToken(Context context)| Get token of the device; a normal result can be obtained only if the registration is successful |
|void setReportNotificationStatusEnable(final Context context,final boolean debugMode)| Set whether to report the notification bar status; enabled by default |
|void setReportApplistEnable(final Context context,final boolean debugMode)| Set the whether to report the app list for smart push; enabled by default |
|void enableOtherPush(Context context, boolean flag)| Set whether to support third-party vendor push |
|void setMiPushAppId(Context context, String appid)| Set Mi push APPID |
|void setMiPushAppKey(Context context, String appkey)| Set Mi push APPKEY |
|void setMzPushAppId(Context context, String appid)| Set Meizu push APPID |
|void setMzPushAppKey(Context context, String appkey)| Set Meizu push APPKEY |
|void setHuaweiDebug(boolean isHuaweiDebug)| Set Huawei log mode for troubleshooting |




### XGPushBaseReceiver Broadcast Class

The XGPushBaseReceiver class enables receipt of passthrough messages and feedback on operation results. You must inherit this class and overload related methods.

In addition, you need to register it statically in AndroidManifest.xml (please note that if it is dynamically registered in the code, the current app can receive the messages only when it is running).

| Prototype | Function |
|-----|----|
|void onTextMessage(Context context,XGPushTextMessage message)| Callback of the in-app message |
|void onRegisterResult(Context context,int errorCode,XGPushRegisterResult registerMessage)| Register the callback |
|void onUnregisterResult(Context context, int errorCode)| Unregister the callback | 
|void onSetTagResult(Context context,int errorCode,String tagName)| Set tag callback |
|void onDeleteTagResult(Context context, int errorCode,String tagName)| Delete tag callback |
|void onNotifactionShowedResult(Context context, XGPushShowedResult notifiShowedRlt)| Callback triggered by the display of the notification, where the notification received by the app can be retained |
|void onNotifactionClickedResult(Context context, XGPushClickedResult message)| Callback triggered by the tap on the notification |




## Starting and Registering

<hr>

The app can only use the TPNS service after completing the registration and startup of TPNS. Please ensure that the AccessId and AccessKey are configured before this.

The new version of the SDK has integrated TPNS startup and app registration into the registration API, that is, the startup and registration operations are completed by default by simply calling the registration API.

After successful registration, the device token will be returned. The token is used to identify the uniqueness of the device and is also the unique identifier of the connection between TPNS and the backend. For more information about how to get the token, see the "Getting Token" section.

The registration API usually provides a compact version and a version with callback. Please choose an appropriate version according to your business needs.


### Binding Device Registration

<hr>

Ordinary registration only registers the current device, and the backend can send push messages to different device tokens. There are two versions of the API.

Note: This registration method does not support push to account.

***(1) Prototype***

```java
public static void registerPush(Context context)```

*** (2) Parameters***

context: The context object of the current app, which cannot be null

***(3) Sample***

```java
XGPushManager.registerPush(this);```

In addition, in order to make it easier for you to know whether the registration succeeds, a version with callback is provided.

***(1) Prototype***

```java
public static void registerPush(Context context,
final XGIOperateCallback callback)```


*** (2) Parameters***

context: The context object of the current app, which cannot be null

callback: The callback of the operation, which include callbacks for success and failure and cannot be null

***(3) Sample***

```java
XGPushManager.registerPush(this, new XGIOperateCallback() {
@Override
public void onSuccess(Object data, int flag) {
Log.d("TPush", "The registration succeeded, and the device token is: " + data);
}
@Override
public void onFail(Object data, int errCode, String msg) {
Log.d("TPush", "The registration failed; error code: " + errCode + ", error message: " + msg);
}
})```



### Binding Account Registration

<hr>

Binding account registration is using specified account to register app on the basis of binding device registration. One account cannot be logged into multiple devices. In this way, backend can send push messages to specified accounts. This API has two versions.

Note: Accounts can be email, QQ account number, mobile number, username, etc.

***(1) Prototype***

```java
public static void registerPush(Context context, String account)```

*** (2) Parameters***

context: The context object of the current app, which cannot be null

account: This is the bound account. Push messages can be sent to the account after bound. The account cannot be a single character such as "2" or "a".

If you want to push by alias, you need to set the alias in the account field of the registration request when calling the registration API. Only one account alias is allowed for one device.

***(3) Sample***

```java
XGPushManager.registerPush(this, "UserAccount")
```
In addition, in order to make it easier for you to know whether the registration succeeds, a version with callback is provided.

***(1) Prototype***

```java
public static void registerPush(Context context, String account,
final XGIOperateCallback callback) ```


*** (2) Parameters***

context: The context object of the current app, which cannot be null

account: This is the bound account. Push messages can be sent to the account after bound.

If you want to push by alias, you need to set the alias in the account field of the registration request when calling the registration API. Only one account alias is allowed for one device. If multiple devices log in to the same account, only the last bound device is valid. This cannot be null

callback: The callback of the operation, which include callbacks for success and failure and cannot be null

Note:
Up to 10 accounts are allowed for one token, and up to 100 tokens are allowed for one account.

To bind an account in TPNS v3.2.2 beta and higher, you need to call the new API.

```java

Start and register the app, and bind the account at the same time. Recommended for apps with an account system (used for versions below 3.2.2; there is registration callback).
void registerPush(Context context, String account, XGIOperateCallback callback)
	
Start and register the app, and bind the account at the same time. Recommended for apps with an account system. (Used for version 3.2.2 and higher; this API will override the account previously bound to the device; and only the currently registered account will take effect.)
void bindAccount(Context context, String account, XGIOperateCallback callback)

Start and register the app, and bind the account at the same time. Recommended for apps with an account system. (Used for version 3.2.2 and higher; this API will override the account previously bound to the device; and only the currently registered account will take effect. There is no registration callback.)	
void bindAccount(Context context, final String account)

Start and register the app, and bind the account at the same time. Recommended for apps with an account system. (Used for version 3.2.2 and higher; this API will retain the previous account and only perform an addition operation. A maximum of 10 accounts is allowed for one token; if this limit is exceeded, the previously bound account will be automatically replaced. There is registration callback.)
void appendAccount(Context context, String account, XGIOperateCallback callback)

Start and register the app, and bind the account at the same time. Recommended for apps with an account system. (Used for version 3.2.2 and higher; this API will retain the previous account and only perform an addition operation. A maximum of 10 accounts is allowed for one token; if this limit is exceeded, the previously bound account will be automatically replaced. There is no registration callback.)
void appendAccount(Context context, final String account)	
```


***(3) Sample***

```java
XGPushManager.registerPush(this, "UserAccount",
new XGIOperateCallback() {
@Override
public void onSuccess(Object data, int flag) {
Log.d("TPush", "The registration succeeded, and the device token is: " + data);
}

@Override
public void onFail(Object data, int errCode, String msg) {
Log.d("TPush", "The registration failed; error code: " + errCode + ", error message: " + msg);
}
});```





### Unbinding Account

<hr>

If the app was bound to an account by calling registerPush(context, account) and now needs to be unbound (such as when the user exits), the following method can be called.

Call

```java
registerPush(context, "*") or registerPush(context, "*", xGIOperateCallback )```

That is, setting account="*" means unbinding the previous account.

To unbind an account in TPNS v3.2.2 beta and higher, you need to call the new API:

```java
// Unbind the specified account (used for version 3.2.2 and higher; there is registration callback)

void delAccount(Context context, final String account, XGIOperateCallback callback)	

// Unbind the specified account (used for version 3.2.2 and higher; there is no registration callback)

void delAccount(Context context, final String account ）	

```

Note

Account unbinding just removes the association between the token and the app account. If full/tag/token push is used, the notification/message can still be received.

#### Registration with Login State

<hr>

Taking into account the user's login state, such as in Mobile QQ or Qzone scenarios, we provide a registration API with login state, making it easier for use in such scenarios.

***(1) Prototype***

```java
public static void registerPush(Context context, String account,
String ticket, int ticketType, String qua,
final XGIOperateCallback callback)



*** (2) Parameters***


context: The context object of the current app, which cannot be null

callback: The callback of the operation, which include callbacks for success and failure and cannot be null

account: This is the bound account. Push messages can be sent to the account after bound.

If you want to push by alias, you need to set the alias in the account field of the registration request when calling the registration API. Only one account alias is allowed for one device, and up to 15 devices are allowed for one alias. This cannot be null

ticket: Login state ticket, which cannot be null

ticketType: Ticket type

qua: A field dedicated to Qzone, which can be null if not needed

***(3) Sample**

```java
XGPushManager.registerPush(this, "UserAccount", "ticket", 1, null,
new XGIOperateCallback() {
@Override
public void onSuccess(Object data, int flag) {
Log.d("TPush", "The registration succeeded, and the device token is: " + data);
}

@Override
public void onFail(Object data, int errCode, String msg) {
Log.d("TPush", "The registration failed; error code: " + errCode + ", error message: " + msg);
}
});
```

### Getting Registration Result

<hr>

There are two ways to check whether the registration succeeds.

***(1) Use the callback version of the registration API***

The XGIOperateCallback class provides an API to process registration success/failure. Please see the sample in the registration API.

Definition of XGIOperateCallback:

```java
/**
* Operation callback API
*/
public interface XGIOperateCallback {
/**
* Callback when the operation succeeds
* @param data The business data of successful operation, such as the token information when the registration succeeds
* @param flag Flag tag
*/
public void onSuccess(Object data, int flag);
/**
* Callback when the operation fails
* @param data Business data of failed operation
* @param errCode Error code
* @param msg Error message
*/
public void onFail(Object data, int errCode, String msg);
}
```

**(2) Overload XGPushBaseReceiver**

The result can be obtained by overloading the onRegisterResult method of XGPushBaseReceiver.

(Note: The overloaded XGPushBaseReceiver needs to be configured in AndroidManifest.xml. For more information, see the "Message Configuration" section)

***Sample***

```java
/**
* Registration result
*
* @param context
* App context object
* @param errorCode
* Error code; {@link XGPushBaseReceiver#SUCCESS} indicates success, while others indicate failure
* @param registerMessage
* Registration result return
*/
```


Below is the list of methods provided by XGPushRegisterResult:

| Method name | Return value | Default value | Description |
|---|---|----|----|
|getToken()|String|""| Token of the device, i.e., the unique ID of the device |
|getAccessId()|long|0| Get the accessId of the registration |
|getAccount|String|""| Get the account bound to the registration |
|getTicket()|String|""| Login state ticket |
|getTicketType()|short|0| Ticket type |


## Unregistration

<hr>

When the user has exited or the app is closed and pushes are no longer needed to be received, the app can be unregistered. (Note: Once the device is unregistered, the device will not receive pushed messages before it is re-registered successfully)


***(1) Prototype***

```java
public static void unregisterPush(Context context)```


*** (2) Parameters***

```java
context: The context object of the app.
```

***(3) Sample***

```java
XGPushManager.unregisterPush(this);```



***Unregistration result***

The result can be obtained by overloading the onUnregisterResult method of XGPushBaseReceiver.

***Sample***

```java
<pre class="brush:cpp;">/**
* Unregistration result
*
* @param context
* App context object
* @param errorCode
* Error code; {@link XGPushBaseReceiver#SUCCESS} indicates success, while others indicate failure
*/
@Override
public void onUnregisterResult(Context context, int errorCode) {

}
</pre>```

***Note***

The unregistration operation should not be too frequent; otherwise, it may cause backend synchronization delay.

Switching accounts does not require unregistration, and for multiple registrations, the last registration will take effect.

## Notification and Message

<hr>

TPNS mainly provides two push formats:
"Push notification" and "passthrough message command", which have certain differences.

### Push Notification (Displayed in the Notification Bar)

This refers to the content displayed in the notification bar of the device. All operations are performed by the TPNS SDK. The app can listen to taps on notifications, which is to say, the notifications delivered in the frontend do not need to be processed by the app and will be displayed in the notification bar by default.

After the TPNS service is successfully registered, notifications generally can be delivered without any settings made.

In general, combined with custom notification styles, regular notifications can satisfy most business needs, and if you need more flexible pushes, you can consider using messages.

### In-app Message Command (Not Displayed in Notification Bar)

This refers to the content delivered to the app by TPNS. The app needs to inherit the XGPushBaseReceiver API implementation and handle all the operations on its own, which is to say, the messages delivered are not displayed in the notification bar by default, and TPNS is only responsible for delivering messages from the  TPNS server to the app, but not the processing logic of the messages, which should be implemented by the app itself. For details, see MessageReceiver in Demo.

Message refers to the text message delivered by the developer through frontend or backend scripts. TPNS is only responsible for delivering the message to the app, while the APP itself is completely responsible for the handling of the message body.

Message is flexible and highly customizable, making it more suitable for scenarios where the app prefers to handle personalized business needs by itself, such as delivering app configuration information and customizing message retention and display.

For example, if a game operator needs to provide different notifications for different scenarios (such as reminders for user upgrade, version update, and marketing campaigns), they can encapsulate such scenarios in messages in JSON format and deliver them to the app, and then the app can display different reminders based on the scenarios to meet personalized needs.

  ***Message Configuration***

To make a message receivable, you need to configure the message receiver by configuring the following information in AndroidManifest.xml, where the value of android:name needs to be changed to the receiver implemented by the app itself.

```xml
<!-- Receiver implemented by the app, which is used to receive the message and result feedback -->
<!-- com.tencent.android.xgpushdemo. CustomPushReceiver needs to be changed to the actual receiver -->
<receiver android:name="com.tencent.android.xgpushdemo.CustomPushReceiver" >
<intent-filter>
<!-- Receive message passthrough -->
<action android:name="com.tencent.android.tpush.action.PUSH_MESSAGE" />
<!-- Listen to handling results such as registration, unregistration, tag setting/deletion, and notification tap ->
<action android:name="com.tencent.android.tpush.action.FEEDBACK" />
</intent-filter>
</receiver>```

***Getting In-app Message***

A message delivered by the developer in the frontend can be received by the app by inheriting XGPushBaseReceiver and overloading the onTextMessage method. After successful receipt, the app can handle it according to the specific business scenario.

In addition, XGPushBaseReceiver provides other relevant APIs, such as those for feeding back the results of notification display/tap or registration/unregistration. For details, see the "XGPushBaseReceiver" section or the MessageReceiver class in Demo.

Please make sure that the receiver has been registered in AndroidManifest.xml, i.e., YOUR_PACKAGE.XGPushBaseReceiver is set.


***Prototype***

```java
public void onTextMessage(Context context,
XGPushTextMessage message)
```


***Parameters***

context: The current context of the app

message: The message structure received. Below is the list of methods of XGPushTextMessage:

| Method name | Return value | Default value | Description |
|----|--------|-----|---|
|getContent()|String|""| Message body content; generally, it is sufficient to deliver only this field |
|getCustomContent()|String|""| Custom key-value of the message |
|getTitle()|String|""| Message title (Note: The description of the in-app message delivered from the frontend is not a title) |

### Local Notification
  Local notification is customized by the user and retained locally. When the app is launched, the TPNS service will judge whether there is a notification once every five minutes based on the network heartbeat. The local notification can pop up only if the service is enabled, and there may be a delay of around five minutes. (When the set time is smaller than the current device time, the notification will pop up.)
  
        ```java
        // Create a local notification
        XGLocalMessage local_msg = new XGLocalMessage();
       
        // Set the local message type; 1: notification, 2: message
        
        local_msg.setType(1);
        
        // Set the message title
        
        local_msg.setTitle("qq");
        
        // Set the message content
        
        local_msg.setContent("ww");
        
        // Set the message date in format of 20140502, for example
        
        local_msg.setDate("20140930");
        
        // Set the hour when the message is triggered  (in 24-hour time), for example: 22 for 10 pm
        
        local_msg.setHour("19");
        
        // Set the minute when the message is triggered, for example: 05 for the 5th minute in the hour
        
        local_msg.setMin("31");
        
        // Set the message style; the default value is 0 or not set
        
        local_msg.setBuilderId(0);
          
        // Set the action type: 1 - open the activity or the app itself; 2 - open the browser; 3 - open the Intent; 4 - open the app by the package name
         
        local_msg.setAction_type(1);
        
        // Set the app-pulling page
        
        local_msg.setActivity("com.qq.xgdemo.SettingActivity");
        // Set the URL
        
         local_msg.setUrl("http://www.baidu.com");
         
        // Set the Intent
        
         local_msg.setIntent("intent:10086#Intent;scheme=tel;action=android.intent.action.DIAL;S.key=value;end");
             
        // Set whether to override the retention setting of the original build_id. 1 - override; 0 - do not override
        
         local_msg.setStyle_id(1);
         
        // Set the audio resource
        
         local_msg.setRing_raw("mm");
         
        // Set the key and value
        
         HashMap<String, Object> map = new HashMap<String, Object>();
         
         map.put("key", "v1");
         
          map.put("key2", "v2");
          
        local_msg.setCustomContent(map);
        
        // Set the app download URL
        
        local_msg.setPackageDownloadUrl("http://softfile.3g.qq.com:8080/msoft/179/1105/10753/MobileQQ1.0(Android)_Build0198.apk");
        
        // Add the notification to the local system
        XGPushManager.addLocalNotification(context,local_msg);
        ```
        

## Getting Device Token

<hr>

Token is the unique identifier that maintains the persistent connection between TPNS and the backend. It is the unique ID for the app to receive messages. The token can be obtained only after the device is successfully registered in the following methods. (The token of TPNS may change after the app is uninstalled and then reinstalled.)

***(1) Obtain through the registration API with callback***

In the onSuccess(Object data, int flag) method of the registration API with XGIOperateCallback, the parameter "data" is the token. For details, see the relevant sample of the registration API.

***(2) Overload XGPushBaseReceiver***

Overload the onRegisterResult (Context context, int errorCode,	XGPushRegisterResult registerMessage) method of XGPushBaseReceiver and obtain through the getToken API provided by the parameter registerMessage. For details, see the "Getting Registration Result" section.

***(3) XGPushConfig.getToken(context)***

Once the device is successfully registered, the token will be stored locally and then can be obtained through the XGPushConfig.getToken(context) API.


## Getting Notification

<hr>

The delivery and display of notifications are completely controlled by the TPNS SDK, but some developers need to retain the displayed notification content locally, which can be achieved by overloading the onNotificationShowedResult(Context, XGPushShowedResult) method of XGPushBaseReceiver. Here, the XGPushShowedResult object provides an API for reading the notification content.


***Prototype***

```java
public abstract void onNotificationShowedResult(Context context,XGPushShowedResult notifiShowedRlt); ```

***Parameters***

context: Current context of the app      notifiShowedRlt: The notification object displayed


## Getting Message Tap Result

<hr>

***(v2.30 and higher) Notification effect listening and custom key-value***

The activity display page built in the TPNS SDK can be used. Statistics of notification/message arrivals, notification taps and dismissals are collected by default. However, if you want to listen to these events, you need to embed the code as follows.

Note: If you want to count the app launches caused by TPNS or get the custom key-value delivered, you need to call the following method in onResume() of all (or opened) activities.

***(1) Prototype***

```java
public abstract void onNotificationShowedResult(Context context,XGPushShowedResult notifiShowedRlt); ```


*** (2) Parameters***

activity: Context of the opened activity

***(3) Return value***

XGPushClickedResult: The opened object of the notification; if the activity is opened due to the notification of TPNS, XGPushClickedResult will be returned; otherwise, null will be returned.

List of methods of the XGPushClickedResult class:

| Method name | Return value | Default value | Description |
|----|--------|-----|---|
|getMsgId()|long|0| Message id |
|getTitle()|String|""| Notification title |
|getContent()|String|""| Notification body content |
|getActivityName()|String|""| Name of the page opened |
|getCustomContent()|String|""| Custom key-value, which is a JSON string; at the same time, call the following method in onPause() of Activity |


***(1) Prototype***

```java
public static void onActivityStoped(Activity activity) ```


*** (2) Parameters***

activity: Context of the current activity


***(3) Sample***

```java
@Override
protected void onPause() {
super.onPause();
XGPushClickedResult clickedResult = XGPushManager.onActivityStarted(this);
String  customContent= clickedResult.getCustomContent();
} ```


## Tags

<hr>

***Preset tags***

Currently, TPNS provides two types of preset tags:

Geographic location (at the provincial level)

App version number

Preset tags are automatically reported inside the SDK.

Push method: TPNS console - Push target - Specific users - Device properties


***Set a tag***

You can set tags for different users and then send mass notifications based on tag names in the frontend. An app can have up to 10,000 tags, each token can have up to 100 tags in one app, and no spaces are allowed in the tag.



***Function prototype***

```java
public static void setTag(Context context, String tagName) ```



***Parameters***

context: Context object

tagName: Name of the tag to be set, which cannot be null or empty.



***Handling result***

The result can be obtained by overloading the onSetTagResult method of XGPushBaseReceiver.


***Sample***

```java
XGPushManager.setTag(this, "male"); ```



***Set multiple tags***

**(v4.0.3 and higher)** This is to set multiple tags at a time, which will override the tags previously set for this device.



***Function prototype***

```java
public static void setTags(Context context, String operateName, Set<String> tags) ```



***Parameters***

context: Context object
operateName: User-defined operation name. The callback result will return it as-is, which is used to distinguish the operation. The tagName parameter of onSetTagResult of XGPushBaseReceiver is returned as-is.
tags: A collection of tag names, where each tag is a string. Restrictions: Each tag cannot exceed 40 bytes (if this limit is exceeded, the tag will be discarded) or contain spaces (the included spaces will be deleted). Up to 1,000 tags can be set, and excessive ones will be discarded



***Handling result***

The result can be obtained by overloading the onSetTagResult method of XGPushBaseReceiver.


***Sample***

```java
String[] tags = "tag1 tag2".split(" ");
Set<String> tagsSet = new HashSet<>(Arrays.asList(tags));
XGPushManager.setTags(getApplicationContext(), "setTags:" + System.currentTimeMillis(), tagsSet); 
```



***Add multiple tags***

**(v4.0.3 and higher)** This is to add multiple tags at a time, which will not override the tags previously set for this device.



***Function prototype***

```java
public static void addTags(Context context, String operateName, Set<String> tags) 
```



***Parameters***

context: Context object
operateName: User-defined operation name. The callback result will return it as-is, which is used to distinguish the operation. The tagName parameter of onSetTagResult of XGPushBaseReceiver is returned as-is.
tags: A collection of tag names, where each tag is a string. Restrictions: Each tag cannot exceed 40 bytes (if this limit is exceeded, the tag will be discarded) or contain spaces (the included spaces will be deleted). Up to 1,000 tags can be set, and excessive ones will be discarded



***Handling result***

The result can be obtained by overloading the onSetTagResult method of XGPushBaseReceiver.


***Sample***

```java
String[] tags = "tag1 tag2".split(" ");
Set<String> tagsSet = new HashSet<>(Arrays.asList(tags));
XGPushManager.addTags(getApplicationContext(), "addTags:" + System.currentTimeMillis(), tagsSet);
```




***Delete a tag***



This is to delete user tag data.


***Function prototype***


```java
public static void deleteTag(Context context, String tagName) ```



***Parameters***

context: Context object

tagName: Name of the tag to be set, which cannot be null or empty


***Handling result***

The result can be obtained by overloading the onDeleteTagResult method of XGPushBaseReceiver.

***Sample***

```java
XGPushManager.deleteTag (this, "male"); ```



***Delete multiple tags***

**(v4.0.3 and higher)** This is to delete multiple tags at a time.



***Function prototype***

```java
public static void deleteTags(Context context, String operateName, Set<String> tags)
```



***Parameters***

context: Context object
operateName: User-defined operation name. The callback result will return it as-is, which is used to distinguish the operation. The tagName parameter of onSetTagResult of XGPushBaseReceiver is returned as-is.
tags: A collection of tag names, where each tag is a string. Restrictions: Each tag cannot exceed 40 bytes (if this limit is exceeded, the tag will be discarded) or contain spaces (the included spaces will be deleted). Up to 1,000 tags can be set, and excessive ones will be discarded



***Handling result***

The result can be obtained by overloading the onSetTagResult method of XGPushBaseReceiver.


***Sample***

```java
String[] tags = "tag1 tag2".split(" ");
Set<String> tagsSet = new HashSet<>(Arrays.asList(tags));
XGPushManager.deleteTags(getApplicationContext(), "deleteTags:" + System.currentTimeMillis(), tagsSet);
```



***Clear all tags***

**(v4.0.3 and higher)** This is to clear all tags of this device.



***Function prototype***

```java
public static void cleanTags(Context context, String operateName)
```



***Parameters***

context: Context object
operateName: User-defined operation name. The callback result will return it as-is, which is used to distinguish the operation. The tagName parameter of onSetTagResult of XGPushBaseReceiver is returned as-is.



***Handling result***

The result can be obtained by overloading the onSetTagResult method of XGPushBaseReceiver.


***Sample***

```java
XGPushManager.cleanTags(getApplicationContext(), "cleanTags:" + System.currentTimeMillis());
```



## Configuration APIs

<hr>

All configuration-related APIs are in the XGPushConfig class. In order for the configuration to take effect in time, you need to ensure that the configuration APIs are called before starting or registering TPNS.


### Debugging Mode

(Important note: To ensure data security, please make sure that debugging mode is turned off at the time of publishing!)


***(1) Function prototype***

```java
public static void enableDebug(Context context, boolean debugMode) ```


*** (2) Parameters***

context: App context object

debugMode: false by default. Set it to true if you want to turn on the debugging log

### Getting Token

Token (also known as mobile ID or MID) is the identity ID of a device. It is randomly generated by the server based on the device properties and delivered to the local system. The tokens obtained by all apps using TPNS or Mobile Tencent Analytics (MTA) on the same device are the same.

One of the benefits of using tokens is that it eliminates the statistical impact of duplicate device IDs of knockoff mobile phones and increases accuracy.

If you happen to be using the latest version of MTA, the MID obtained through the MTA's StatConfig.getMid() API is the same as that obtained by this API.

Note: The first registration will generate a token, which will be retained in the phone and will always exist regardless of subsequent logout or unregistration. In v3.0 and higher, the token may change if the app is uninstalled and then reinstalled.

***(1) Function prototype***


```java
public static String getToken(Context context) ```



*** (2) Parameters***

context: App context object

***(3) Return value***

A normal token will be returned upon success, while null or "0" upon failure


### Setting AccessID

If it has already been configured in AndroidManifest.xml, it does not need to be called again; if both of them exist, this API will prevail.

***(1) Function prototype***

```java
public static boolean setAccessId(Context context, long accessId) ```


*** (2) Parameters***

Context object
accessId: The accessId obtained by the registration in the frontend


***(3) Return value***

true: Success

false: Failure

Note: The accessId set through this API will also be stored in the file

### Setting AccessKey
If it has already been configured in AndroidManifest.xml, it does not need to be called again; if both of them exist, this API will prevail.

***(1) Function prototype***

```java
public static boolean setAccessId(Context context, String accessKey) ```


*** (2) Parameters***

Context object

accesskey: The accesskey obtained by the registration in the frontend


***(3) Return value***

true: Success

false: Failure

Note: The accessId set through this API will also be stored in the file
