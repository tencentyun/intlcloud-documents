# APIs

<hr>

## API Overview


The path prefix of all APIs’ package names is: ```com.tencent.android.tpush```. There are several important classes that provide APIs for external use, including:

| Class name | Description |
|-------|-----|
|```XGPushManager```| Push service |
|```XGPushConfig```| Push service configuration item API |
|```XGPushBaseReceiver```| Receiver to receive messages and result feedback, which needs to be statically registered by developers in ```AndroidManifest.xml``` |
## Launch and registration

<hr>

The app can only use the SDK push service after successfully registering for and launching the TPNS. Please ensure that AccessId and AccessKey have already been configured.

The new version of SDK has integrated TPNS launch and app registration into the registration API, which means you can simply call the registration API to complete the launch and registration by default.

After a successful registration, the device token will be returned. The token is used to identify the uniqueness of the device and is also the unique identifier for TPNS to stay connected with the backend. For more information on how to get tokens, see **Getting Tokens**.

The registration API usually provides a compact version and a version with callback. Please choose an appropriate version according to your business needs.


### Registering the device

<hr>

Standard registration only registers the current device, and the backend can send different push messages based on device tokens. There are two versions of the API.

Note: This registration method does not support account push.

***Prototype***

```java
public static void registerPush(Context context)
```

***Parameters***

context: The context object of the current app, which cannot be null

***Sample***

```java
XGPushManager.registerPush(this);
```

To allow you to know if the registration is successful, a version with callback is provided.

***Prototype***

```java
public static void registerPush(Context context,
final XGIOperateCallback callback)
```


***Parameters***

context: The context object of the current app, which cannot be null

callback: Callback functions, including success and failure callbacks and cannot be null

***Sample***

```java
XGPushManager.registerPush(this, new XGIOperateCallback() {
@Override
public void onSuccess(Object data, int flag) {
Log.d("TPush", "The registration is successful, the device token is: " + data);
}
@Override
public void onFail(Object data, int errCode, String msg) {
Log.d("TPush", "The registration failed, error code: " + errCode + ", error message: " + msg);
}
})

```


### Binding an account for registration

<hr>

Binding an account for registration means using a specified account to register for the app in addition to binding a device for registration (one account cannot be logged into multiple devices). This allows the backend to send push messages to specified accounts. This API has two versions.

Note: The account can be email, QQ account number, mobile number, username, etc.

***Prototype***
```java	
Launch and register for the app, and at the same time bind the account. Recommended for apps with an account system. This API will override accounts previously bound to the device, and only the current registered account will take effect
void bindAccount(Context context, String account, XGIOperateCallback callback)

Launch and register for the app, and at the same time bind the account. Recommended for apps with an account system. This API will override accounts previously bound to the device, and only the current registered account will take effect. There is no registration callback	
void bindAccount(Context context, final String account)

Launch and register for the app, and at the same time bind the account. Recommended for apps with an account system. This API will retain the previous account and only perform an addition operation. One token can have a maximum of 10 accounts, otherwise accounts that are bound previously will be automatically replaced. There is registration callback
void appendAccount(Context context, String account, XGIOperateCallback callback)

Launch and register for the app, and at the same time bind the account. Recommended for apps with an account system. This API will retain the previous account and only perform an addition operation. One token can have a maximum of 10 accounts, otherwise accounts that are bound previously will be automatically replaced. There is no registration callback
void appendAccount(Context context, final String account)	
```
***Parameters***

context: The context object of the current app, which cannot be null

account: The account


***Sample***

```java
XGPushManager.bindAccount(getApplicationContext(),"test");
```



### Unbinding Account

<hr>


```java
//Unbind the specified account (there is registration callback)

void delAccount(Context context, final String account, XGIOperateCallback callback)	

//Unbind the specified account (there is no registration callback)

void delAccount(Context context, final String account ）
```

Note

**Account unbinding only removes the association between the token and the app account. If full/tag/token push is used, the notification/message can still be received.**

***Parameters***

context: The context object of the current app, which cannot be null

account: The account

***Sample***

```java
XGPushManager.delAccount(getApplicationContext(),"test");
```



### Getting registration result

<hr>

There are two ways to check if the registration is successful

***(1) Use the callback version of the registration API***

The XGIOperateCallback class provides an API to process registration success or failure. Please see the sample in the registration API.

Definition of XGIOperateCallback:

```java
/**
* Operation callback API
*/
public interface XGIOperateCallback {
/**
* Callback when the operation is successful
* @param data Business data of a successful operation, such as the token information when registration is successful
* @param flag Flag tag
*/
public void onSuccess(Object data, int flag);
/**
* Callback when the operation fails
* @param data Business data of a failed operation
* @param errCode Error code
* @param msg Error message
*/
public void onFail(Object data, int errCode, String msg);
}
```

**(2) Reload XGPushBaseReceiver**

The result can be obtained by reloading the onRegisterResult of XGPushBaseReceiver.

(Note: The reloaded XGPushBaseReceiver needs to be configured in AndroidManifest.xml. For more information, see "Message Configuration")

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
|getToken()|String|""| Device token, i.e., the unique ID of the device |
|getAccessId()|long|0| Get the accessId of the registration |
|getAccount|String|""| Get the account bound for registration |
|getTicket()|String|""| Login state ticket |
|getTicketType()|short|0| Ticket type |


## Unregistration

<hr>

When a user has logged out or the app is closed and it is no longer necessary to receive push messages, the device can be unregistered from the app. (Note: Once the device is unregistered, push messages will no longer be received unless the device is successfully registered again)


***(1) Prototype***

```java
public static void unregisterPush(Context context)
```


*** (2) Parameters***

```java
context: The context object of the app.
```


***(3) Sample***

```java
XGPushManager.unregisterPush(this);
```



***Unregistration result***

The result can be obtained by reloading the onUnregisterResult of XGPushBaseReceiver.

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
</pre>
```

***Note***

Unregistration operation should not be too frequent; otherwise, it may cause delay in backend synchronization.

Switching accounts does not require unregistration. With multiple registrations, the last registration will automatically take effect.

## Notification and Message

<hr>

TPNS mainly provides two push formats:
"Push notification" and "pass-through message command", which are different.

### Push notification (displayed in the notification panel)

This refers to the content displayed in the notification panel of the device. All operations are performed by TPNS SDK. The app can listen to clicks on notifications. In other words, push notifications delivered in the frontend do not need to be processed by the app and will be displayed in the notification panel by default.

After the TPNS service is successfully registered, notifications can be delivered without any configuration.

In general, combined with custom notification styles, standard notifications can meet most business needs, and if you need more flexible pushes, you can consider using messages.

### In-app message command (not displayed in notification panel)

This refers to the content delivered to the app by TPNS. The app needs to inherit the XGPushBaseReceiver API to implement and handle all the operations on its own. In other words, delivered messages are not displayed in the notification panel by default, and TPNS is only responsible for delivering messages from the TPNS server to the app, but not processing the messages, which needs to be done by the app. For more information, see MessageReceiver in the Demo.

Message refers to the text message delivered by the developer through frontend or backend scripts. TPNS is only responsible for delivering the message to the app, while the APP is fully responsible for handling the message body on its own.

Because the message is flexible and highly customizable, it is suitable for apps to handle custom business needs on its own, such as delivering app configuration information, and customizing message retention and display.

For example, if a game needs to provide different notifications for different scenarios (such as reminders for user upgrade, version update, and marketing campaigns), it can encapsulate these scenarios in messages in JSON format and deliver them to the app, and then the app can display different reminders based on these scenarios to meet personalized needs.

  ***Message Configuration***

If you need to listen to messages, see the XGPushBaseReceiver API or the MessageReceiver class in the demo. You can inherit XGPushBaseReceiver and configure the following content in the configuration file:

```xml
    <receiver android:name="Complete class name, such as: com.qq.xgdemo.receiver.MessageReceiver">
        <intent-filter>
        <!-- Receive message passthrough -->
        <action android:name="com.tencent.android.tpush.action.PUSH_MESSAGE" />
        <!-- Listen to results of registration, unregistration, tag setting/deletion, and notification click ->
        <action android:name="com.tencent.android.tpush.action.FEEDBACK" />
        </intent-filter>
    </receiver>
```

***Getting in-app message***

A message delivered by the developer in the frontend can be received by the app if it inherits XGPushBaseReceiver and reloads the onTextMessage. After successfully receiving the message, the app can handle it based on specific business scenarios.

XGPushBaseReceiver also provides other APIs, such as those for returning the results of notification display/click or registration/unregistration. For more information, see the "XGPushBaseReceiver" section or the MessageReceiver class in the demo.

Please make sure that the receiver has been registered in AndroidManifest.xml, i.e., YOUR_PACKAGE.XGPushBaseReceiver is set.


***Prototype***

```java
public void onTextMessage(Context context,
XGPushTextMessage message)
```


***Parameters***

context: The current context of the app

message: The received message structure. Below is the list of methods of XGPushTextMessage:

| Method name | Return value | Default value | Description |
|----|--------|-----|---|
|getContent()|String|""| Message body content, and generally it is sufficient to deliver only this field |
|getCustomContent()|String|""| Custom key-value of the message |
|getTitle()|String|""| Message title (note: The description of the in-app message delivered from the frontend is not a title) |

### Local Notification
  Local notifications are customized by the user and saved locally. When the app is open, the TPNS service will determine whether there is a notification once every five minutes based on the network heartbeat. Local notifications will pop up only if the service is enabled, and there may be a delay of about five minutes. The notification will pop up when the time set is earlier than the current device time.
  
 ***Sample code***
```java
        // Create a local notification
        XGLocalMessage local_msg = new XGLocalMessage();
       
        // Set the local message type; 1: notification, 2: message
        
        local_msg.setType(1);
        
        // Set the message title
        
        local_msg.setTitle("qq");
        
        // Set the message content
        
        local_msg.setContent("ww");
        
        // Set the message date in the format of 20140502, for example
        
        local_msg.setDate("20140930");
        
        // Set the hour when the message is triggered (in 24-hour time), for example: 22 indicates 10 p.m.
        
        local_msg.setHour("19");
        
        // Set the minute when the message is triggered, for example: 05 indicates the 5th minute in the hour
        
        local_msg.setMin("31");
        
        // Set the message style, the default value is 0 or none
        
        local_msg.setBuilderId(0);
          
        // Set the action type: 1 - open the activity or the app itself; 2 - open the browser; 3 - open the Intent; 4 - open the app by the package name
         
        local_msg.setAction_type(1);
        
        // Set the app-pulling page
        
        local_msg.setActivity("com.qq.xgdemo.SettingActivity");
        // Set the URL
        
         local_msg.setUrl("http://www.baidu.com");
         
        // Set the Intent
        
         local_msg.setIntent("intent:10086#Intent;scheme=tel;action=android.intent.action.DIAL;S.key=value;end");
             
        //Whether to overwrite the save settings of the original build_id. 1: Yes; 0: No.
        
         local_msg.setStyle_id(1);
         
        // Set the audio resource
        
         local_msg.setRing_raw("mm");
         
        // Set the key and value
        
         HashMap<String, Object> map = new HashMap<String, Object>();
         
         map.put("key", "v1");
         
          map.put("key2", "v2");
          
        local_msg.setCustomContent(map);
        
        // Set the URL for downloading apps
        
        local_msg.setPackageDownloadUrl("http://softfile.3g.qq.com:8080/msoft/179/1105/10753/MobileQQ1.0(Android)_Build0198.apk");
        
        // Add notification locally     XGPushManager.addLocalNotification(context,local_msg);
```
        

## Getting device token

<hr>

A token is the unique identifier for TPNS to stay connected with the backend. It is the unique ID for the app to receive messages. The token can be obtained only if the device is successfully registered through the following methods. TPNS token may change if the app is uninstalled and reinstalled.

***(1) Obtain through the registration API with callback***

In the onSuccess(Object data, int flag) method of the registration API with XGIOperateCallback, the parameter "data" is the token. For more information, see the relevant sample of the registration API.

***(2) Reload XGPushBaseReceiver***

Reload the onRegisterResult (Context context, int errorCode,XGPushRegisterResult registerMessage) of XGPushBaseReceiver and obtain the token through the getToken API provided by the parameter registerMessage. For more information, see the **Getting registration results** section.

***(3) XGPushConfig.getToken(context)***

Once the device is successfully registered, the token will be stored locally and then can be obtained through the XGPushConfig.getToken(context) API.


## Getting Notification

<hr>

The delivery and display of notifications are completely controlled by the TPNS SDK. To store the displayed notification content locally, developers can reload the onNotificationShowedResult(Context, XGPushShowedResult) of XGPushBaseReceiver. Here, the XGPushShowedResult object provides an API for reading the notification content.


***Prototype***

```java
public abstract void onNotificationShowedResult(Context context,XGPushShowedResult notifiShowedRlt); 
```

***Parameters***

context: Current context of the app, notifiShowedRlt: The displayed notification object


## Getting message click results

<hr>

*** Listening to notification effect and customizing key-value ***

On the built-on activity display page of TPNS, the number of notification/message arrivals and the action of notification clicks/ clearing are counted by default. To listen to these events, you need to embed the code as follows.

Note: If developers want to count the number of app launches caused by TPNS or get the delivered custom key-value, they need to call the following method in onResume() of all (or opened) activities.

***(1) Prototype***

```java
public abstract void onNotificationShowedResult(Context context,XGPushShowedResult notifiShowedRlt); 
```


*** (2) Parameters***

activity: Context of the opened activity

***(3) Return value***

XGPushClickedResult: The opened object of the notification; if the activity is open due to TPNS notification, XGPushClickedResult will be returned; otherwise, null will be returned.

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
public static void onActivityStoped(Activity activity) 
```


*** (2) Parameters***

activity: Context of the current activity


***(3) Sample***

```java
@Override
protected void onPause() {
super.onPause();
XGPushClickedResult clickedResult = XGPushManager.onActivityStarted(this);
String  customContent= clickedResult.getCustomContent();
} 
```


## Tags

<hr>

***Preset tags***

Currently, TPNS provides two types of preset tags:

Geographic location (at the provincial level)

App version number

Preset tags are automatically reported in the SDK.



***Configuring custom tags***

Developers can set tags for different users and then send bulk notifications based on the tags. An app can have a maximum of 10,000 tags, and each token can have a maximum of 100 tags under one app. A tag cannot contain any spaces.



***Function prototype***

```java
public static void setTag(Context context, String tagName) 
```



***Parameters***

context: Context object

tagName: Name of the tag to be set, which cannot be null or empty.



***Processing result***

The result can be obtained by reloading the onSetTagResult of XGPushBaseReceiver.


***Sample***

```java
XGPushManager.setTag(this, "male"); 
```



***Set multiple tags***

Set multiple tags at a time, which will override the tags previously set for this device. If the format of the newly added tags is “test:2", “level:2", all historical tags of the device will be deleted, and “test:2” and “level:2” will be added
If the newly added tag has a part without the punctuation mark `:`, such as [“test:2”, “level”], then all historical tags of this device will be deleted, and then “test:2” and “level” tags will be added

*Note*:
 1. In newly added tags, `:` is the backend keyword. Use it according to your business scenarios
2. In this API, you must first check the table and clear historical tags before you can set new tags. When calling, the interval should not be too tight (we recommend an interval of greater than 5s), otherwise an update may occur



***Function prototype***

```java
public static void setTags(Context context, String operateName, Set<String> tags) 
```



***Parameters***

context: Context object
operateName: The operation name defined by the user. The callback result will be returned as it is for user to distinguish the operation. The tagName parameter of onSetTagResult in XGPushBaseReceiver is returned as it is
tags: A collection of tag names, and each tag is a string. Restrictions: Each tag cannot exceed 40 bytes (otherwise the tag will be discarded) or contain spaces (all spaces will be deleted). Up to 1,000 tags can be set, and excessive ones will be discarded



***Processing result***

The result can be obtained by reloading the onSetTagResult of XGPushBaseReceiver.


***Sample***

```java
String[] tags = "tag1 tag2".split(" ");
Set<String> tagsSet = new HashSet<>(Arrays.asList(tags));
XGPushManager.setTags(getApplicationContext(), "setTags:" + System.currentTimeMillis(), tagsSet); 
```



***Add multiple tags***

Adding multiple tags at a time will not override tags previously set for this device.



***Function prototype***

```java
public static void addTags(Context context, String operateName, Set<String> tags) 
```



***Parameters***

context: Context object
operateName: The operation name defined by the user. The callback result will be returned as it is for user to distinguish the operation. The tagName parameter of onSetTagResult in XGPushBaseReceiver is returned as it is

tags: A collection of tag names, and each tag is a string. Restrictions: Each tag cannot exceed 40 bytes (otherwise the tag will be discarded) or contain spaces (all spaces will be deleted). Up to 1,000 tags can be set, and excessive ones will be discarded



***Processing result***

The result can be obtained by reloading the onSetTagResult of XGPushBaseReceiver.


***Sample***

```java
String[] tags = "tag1 tag2".split(" ");
Set<String> tagsSet = new HashSet<>(Arrays.asList(tags));
XGPushManager.addTags(getApplicationContext(), "addTags:" + System.currentTimeMillis(), tagsSet);
```




***Delete a tag***



This is for developers to delete user tag data.


***Function prototype***


```java
public static void deleteTag(Context context, String tagName) 
```



***Parameters***

context: Context object

tagName: Name of the tag to be set, which cannot be null or empty


***Processing result***

The result can be obtained by reloading the onDeleteTagResult of XGPushBaseReceiver.

***Sample***

```java
XGPushManager.deleteTag (this, "male"); 
```



***Delete multiple tags***

Delete multiple tags at a time.



***Function prototype***

```java
public static void deleteTags(Context context, String operateName, Set<String> tags)
```



***Parameters***

context: Context object
operateName: The operation name defined by the user. The callback result will be returned as it is for user to distinguish the operation. The tagName parameter of onSetTagResult in XGPushBaseReceiver is returned as it is
tags: A collection of tag names, and each tag is a string. Restrictions: Each tag cannot exceed 40 bytes (otherwise the tag will be discarded) or contain spaces (all spaces will be deleted). Up to 1,000 tags can be set, and excessive ones will be discarded



***Processing result***

The result can be obtained by reloading the onSetTagResult of XGPushBaseReceiver.


***Sample***

```java
String[] tags = "tag1 tag2".split(" ");
Set<String> tagsSet = new HashSet<>(Arrays.asList(tags));
XGPushManager.deleteTags(getApplicationContext(), "deleteTags:" + System.currentTimeMillis(), tagsSet);
```



***Clear all tags***

Clear all tags of this device.



***Function prototype***

```java
public static void cleanTags(Context context, String operateName)
```



***Parameters***

context: Context object
operateName: The operation name defined by the user. The callback result will be returned as it is for user to distinguish the operation. The tagName parameter of onSetTagResult in XGPushBaseReceiver is returned as it is



***Processing result***

The result can be obtained by reloading the onSetTagResult of XGPushBaseReceiver.


***Sample***

```java
XGPushManager.cleanTags(getApplicationContext(), "cleanTags:" + System.currentTimeMillis());
```



## Configuration APIs

<hr>

All configuration APIs are in the XGPushConfig class. In order for the configuration to take effect in time, developers need to ensure that configuration APIs are called before launching or registering for TPNS.


### Debug Mode

(Important note: To ensure data security, make sure debug mode is turned off when publishing)


***(1) Function Prototype***

```java
public static void enableDebug(Context context, boolean debugMode)
```


*** (2) Parameters***

context: App context object

debugMode: The default is false. To enable the debug log, set it to true

### Getting Token

Token (also known as mobile ID or MID) is the identity ID of a device. It is randomly generated by the server based on the device property and delivered to the local system. The token obtained by all apps using TPNS or Mobile Tencent Analytics (MTA) on the same device is the same.

One of the benefits of using token is that it eliminates the statistical impact of duplicate device IDs of knockoff mobile phones, increasing accuracy.

If you use the latest version of MTA, the MID obtained through the MTA's StatConfig.getMid() API is the same as that obtained using this API.

Note: A token is generated during the first registration, and will remain in the mobile phone. The token always exists regardless of unregistration. For version 3.0 and above, the token may change when the app is uninstalled and then reinstalled.

***(1) Function prototype***


```java
public static String getToken(Context context)
```



*** (2) Parameters***

context: App context object

***(3) Return value***

A standard token will be returned upon success, and null or "0" upon failure


### Setting AccessID

If it has already been configured in AndroidManifest.xml, it does not need to be called again; if both of them exist, this API will be used.

***(1) Function prototype***

```java
public static boolean setAccessId(Context context, long accessId)
```


*** (2) Parameters***

Context object
accessId: The accessId obtained by registering in the frontend


***(3) Return value***

true: Success

false: Failure

Note: The accessId set through this API will also be stored in the file

### Setting AccessKey
If it has already been configured in AndroidManifest.xml, it does not need to be called again; if both of them exist, this API will be used.

***(1) Function prototype***

```java
public static boolean setAccessId(Context context, String accessKey) 
```


*** (2) Parameters***

Context object

accesskey: The accesskey obtained by registering in the frontend


***(3) Return value***

true: Success

false: Failure

Note: The accessId set through this API will also be stored in the file

