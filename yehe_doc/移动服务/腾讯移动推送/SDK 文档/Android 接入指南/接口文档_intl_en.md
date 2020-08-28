The path prefix of all APIs' package names is ```com.tencent.android.tpush```. There are several important classes that provide APIs for external use, including:

| Class Name | Description |
| ----------------- | ------------------------------------------------------------ |
| XGPushManager     | Push service                                            |
| XGPushConfig      | Push service configuration item API |
| XGPushBaseReceive | Receiver to receive messages and result feedback, which needs to be statically registered by yourself in `AndroidManifest.xml` |

## Launch and Registration

- The application can only use the SDK push service after successfully registering for and launching the TPNS. Please ensure that `AccessId` and `AccessKey` have already been configured.
- The new version of SDK has integrated TPNS launch and application registration into the registration API, which means you can simply call the registration API to complete the launch and registration by default.
- After a successful registration, the device token will be returned. The token is used to identify the uniqueness of the device and is also the unique ID for TPNS to stay connected with the backend. For more information on how to get tokens, please see [Getting token](#Getting token).

The registration API usually provides a compact version and a version with callback. Please choose an appropriate version according to your business needs.

### Registering device

#### API description

Standard registration only registers the current device, and the backend can send different push messages based on device tokens. There are two versions of the API.

```java
public static void registerPush(Context context)
```

>This registration method does not support account push.

#### Parameter description

context: context object of the current application, which cannot be null.

#### Sample code

```java
XGPushManager.registerPush(getApplicationContext());
```

#### API description

To allow you to know if the registration is successful, a version with callback is provided.

```java
public static void registerPush(Context context,final XGIOperateCallback callback)
```

#### Parameter description

- context: context object of current application, which cannot be null.
- callback: callback functions, including success and failure callbacks and cannot be null.

#### Sample code

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

### Binding an account

#### API description

This API is used to register an application with a specified account. This allows the backend to send push messages to the specified account. This API has two versions.

```java	
Recommended for applications with an account system. This API will override accounts previously bound to the device, and only the current registered account will take effect.
void bindAccount(Context context, String account, XGIOperateCallback callback)

Recommended for applications with an account system. This API will override accounts previously bound to the device, and only the current registered account will take effect. There is no registration callback.	
void bindAccount(Context context, final String account)

Recommended for applications with an account system. This API will retain the previous account and only perform an addition operation. One token can have a maximum of 10 accounts; otherwise, accounts that are bound previously will be automatically replaced. There is registration callback.
void appendAccount(Context context, String account, XGIOperateCallback callback)

Recommended for applications with an account system. This API will retain the previous account and only perform an addition operation. One token can have a maximum of 10 accounts; otherwise, accounts that are bound previously will be automatically replaced. There is no registration callback.
void appendAccount(Context context, final String account)	
```

>
- The account can be email, QQ account number, mobile number, username, etc.
- If multiple devices are bound to the same account, the backend will push the message to the last bound device by default. If you want to push to all the bound devices, you can view the `account_push_type` parameter settings in [REST API](https://tpns.gitbook.io/tpns/pushapi#push-api-ke-xuan-can-shu).



#### Parameter description

- context: context object of current application, which cannot be null.
- account: account.

#### Sample code

```java
XGPushManager.bindAccount(getApplicationContext(),"test");
```

#### Obtaining the account binding result

This API is used to obtain the result of the "XGIOperateCallback" account binding API. For more information about the account binding API, see its API description stated earlier.

Sample code
```java
public interface XGIOperateCallback {

    /**
     * Success callback.
     * @param data  Data of a successful operation, including token of a successful registration.
     * @param flag Tag code
     */
    public void onSuccess(Object data, int flag);
    
    
    /**
     * Failure callback.
     * @param data Data of a failed operation.
     * @param errCode Error code.
     * @param msg Error message.
     */
    public void onFail(Object data, int errCode, String msg);
}
```

### Unbinding account

#### API description

This API is used to unbind a bound account.

```java
// Unbind the specified account (there is registration callback)

void delAccount(Context context, final String account, XGIOperateCallback callback)	

// Unbind the specified account (there is no registration callback)

void delAccount(Context context, final String account )
```

>Account unbinding just removes the association between the token and the application account. If full/tag/token push is used, the notification/message can still be received.

#### Parameter description

- context: context object of current application, which cannot be null.
- account: account.

#### Sample code

```java
XGPushManager.delAccount(getApplicationContext(),"test");
```



### Getting registration result

There are two ways to check if the registration is successful

**Use the Callback version of the registration API**
The `XGIOperateCallback` class provides an API to process registration success or failure. Please see the sample in the registration API.

#### Sample code

```java
/**
* Operation callback API
*/
public interface XGIOperateCallback {
/**
* Callback when the operation is successful
* @param data Business data of a successful operation, such as the token information when registration is successful
* @param flag   Flag tag
*/
public void onSuccess(Object data, int flag);
/**
* Callback when the operation fails
* @param data   Business data of a failed operation
* @param errCode   Error code
* @param msg   Error message
*/
public void onFail(Object data, int errCode, String msg);
}
```

**Reload XGPushBaseReceiver**
The result can be obtained by reloading the `onRegisterResult` method of `XGPushBaseReceiver`.

>The reloaded `XGPushBaseReceiver` needs to be configured in `AndroidManifest.xml`. For more information, please see [Message configuration](#Message configuration) below.

#### Sample code

```java
/**
* Registration result
*
* @param context
* Application context object
* @param errorCode
* Error code; {@link XGPushBaseReceiver#SUCCESS} indicates success, while others indicate failure
* @param registerMessage
* Registration result return
*/
```

#### Class method list

| Method Name | Returned Value | Default Value | Description |
| --------------- | ------ | ------ | ------------------------------- |
| getToken()      | String | None     | Device token, i.e., unique device ID |
| getAccessId()   | long   | 0      | Gets `AccessId` for registration            |
| getAccount      | String | None     | Gets account bound for registration |
| getTicket()     | String | No     | Login state ticket                      |
| getTicketType() | short  | 0      | Ticket type                        |

### Unregistration

#### API description

When a user has logged out or the application is closed and it is no longer necessary to receive push messages, the device can be unregistered from the application. (Once the device is unregistered, push messages will no longer be received unless the device is successfully registered again).

```java
public static void unregisterPush(Context context)
```

#### Parameter description

context: application's context object.



#### Sample code

```java
XGPushManager.unregisterPush(this);
```



### Unregistration result

The result can be obtained by reloading the `onUnregisterResult` method of `XGPushBaseReceiver`.

>
- Unregistration operation should not be too frequent; otherwise, it may cause delay in backend sync.
- Switching accounts does not require unregistration. With multiple registrations, the last registration will automatically take effect.

#### Sample code

```java
<pre class="brush:cpp;">/**
* Unregistration result
*
* @param context
* Application context object
* @param errorCode
* Error code; {@link XGPushBaseReceiver#SUCCESS} indicates success, while others indicate failure
*/
@Override
public void onUnregisterResult(Context context, int errorCode) {

}
</pre>
```



## Notification and Message

TPNS mainly provides two push formats: "push notification" and "in-app message command", which are different.

### Push notification (displayed in notification bar)

This refers to the content displayed in the notification bar of the device. All operations are performed by TPNS SDK. The application can listen to clicks on notifications. In other words, push notifications delivered on the frontend do not need to be processed by the application and will be displayed in the notification bar by default.

>
- After the TPNS service is successfully registered, notifications can be delivered without any configuration.
- In general, combined with custom notification styles, standard notifications can meet most business needs, and if you need more flexible pushes, you can consider using messages.

### In-app message command (not displayed in notification bar)

This refers to the content delivered to the application by TPNS. The application needs to inherit the `XGPushBaseReceiver` API to implement and handle all the operations on its own. In other words, delivered messages are not displayed in the notification bar by default, and TPNS is only responsible for delivering messages from the TPNS server to the application, but not processing the messages, which needs to be done by the application.

- Message refers to the text message delivered by you through frontend or backend scripts. TPNS is only responsible for delivering the message to the application, while the APPLICATION is fully responsible for handling the message body on its own.
- Because the message is flexible and highly customizable, it is suitable for applications to handle custom business needs on its own, such as delivering application configuration information, and customizing message retention and display.

<span id="Message configuration"></span>

### Message configuration

Inherit `XGPushBaseReceiver` and configure the following in the configuration file:

#### Sample code

```xml
<receiver android:name="com.tencent.android.xg.cloud.demo.MessageReceiver">
            <intent-filter>
                <!-- Receive message passthrough -->
                <action android:name="com.tencent.android.xg.vip.action.PUSH_MESSAGE" />
                <!-- Listen to results of registration, unregistration, tag setting/deletion, and notification clicks ->
                <action android:name="com.tencent.android.xg.vip.action.FEEDBACK" />
            </intent-filter>
        </receiver>
```

### Getting in-app message

A message delivered by you on the frontend can be received by the application if it inherits `XGPushBaseReceiver` and reloads the `onTextMessage` method. After successfully receiving the message, the application can handle it based on specific business scenarios.

>Please make sure that the receiver has been registered in AndroidManifest.xml, i.e., YOUR_PACKAGE.XGPushBaseReceiver is set.

```java
public void onTextMessage(Context context,XGPushTextMessage message)
```

#### Parameter description

- context: current context of application.
- message: received message structure.

#### Class method list

| Method Name | Returned Value | Default Value | Description |
| ------------------ | ------ | ------ | ---------------------------------------------------- |
| getContent()       | String | None     | Message body content, and generally it is sufficient to deliver only this field |
| getCustomContent() | String | None     | Customer `key-value` of message                                 |
| getTitle()         | String | None | Message title (the description of the in-app message delivered from the frontend is not a title) |

### Local notification

Local notifications are customized by the user and saved locally. When the application is open, the TPNS service will determine whether there is a notification once every five minutes based on the network heartbeat. Local notifications will pop up only if the service is enabled, and there may be a delay of about five minutes. The notification will pop up when the time set is earlier than the current device time.

#### Sample code

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

// Set the hour when the message is triggered (in 24-hour time); for example: 22 indicates 10 p.m.

local_msg.setHour("19");

// Set the minute when the message is triggered, for example: 05 indicates the 5th minute in the hour

local_msg.setMin("31");

// Set the message style, the default value is 0 or none

local_msg.setBuilderId(0);

// Set the action type: 1 - open the activity or the application itself; 2 - open the browser; 3 - open the Intent; 4 - open the application by the package name

local_msg.setAction_type(1);

// Set the app-pulling page

local_msg.setActivity("com.qq.xgdemo.SettingActivity");
// Set the URL

local_msg.setUrl("http://www.baidu.com");

// Set the Intent

local_msg.setIntent("intent:10086#Intent;scheme=tel;action=android.intent.action.DIAL;S.key=value;end");

// Whether to overwrite the save settings of the original build_id. 1: yes; 0: no.

local_msg.setStyle_id(1);

// Set the audio resource

local_msg.setRing_raw("mm");

// Set the key and value

HashMap<String, Object> map = new HashMap<String, Object>();

map.put("key", "v1");

map.put("key2", "v2");

local_msg.setCustomContent(map);

// Add the notification to the local system     

XGPushManager.addLocalNotification(context,local_msg);
```

### Getting device token

A token is the unique ID for TPNS to stay connected with the backend. It is the unique ID for the application to receive messages. The token can be obtained only if the device is successfully registered through the following methods. TPNS token may change if the application is uninstalled and reinstalled.

#### Getting through registration API with callback

In the `onSuccess(Object data, int flag)` method of the registration API with `XGIOperateCallback`, the `data` parameter is the token. For more information, please see the relevant sample of the registration API.

#### Reloading XGPushBaseReceiver

Reload the `onRegisterResult (Context context, int errorCode,XGPushRegisterResult registerMessage)` method of `XGPushBaseReceiver` and get the token through the `getToken` API provided by the parameter `registerMessage`. For more information, please see the **Getting registration results** section.

#### XGPushConfig.getToken(context)

Once the device is successfully registered, the token will be stored locally and then can be obtained through the `XGPushConfig.getToken(context)` API.

### Getting notification

#### API description

The delivery and display of notifications are completely controlled by the TPNS SDK. To store the displayed notification content locally, you can reload the `onNotificationShowedResult(Context, XGPushShowedResult)` method of `XGPushBaseReceiver`. Here, the `XGPushShowedResult` object provides an API for reading the notification content.

```java
public abstract void onNotificationShowedResult(Context context,XGPushShowedResult notifiShowedRlt); 

```

#### Parameter description

- context: context object of current application.
- notifiShowedRlt: displayed notification object.

### Getting message click results

### Listening on notification effect and customizing key-value

On the built-on activity display page of TPNS, the number of notification/message arrivals and the action of notification clicks/ clearing are counted by default. To listen to these events, you need to embed the code as follows.

>If you want to count the number of application launches caused by TPNS or get the delivered custom `key-value`, you need to call the following method in `onResume()` of all (or opened) activities.

#### API description

```java
onNotificationClickedResult(Context context, XGPushClickedResult notifiClickedRlt); 

```


#### Sample code
```
// If `actionType` of the notification click callback is 1, the message was dismissed; if it is 0, the message was clicked
@Override
public void onNotificationClickedResult(Context context,XGPushClickedResult message) {
if (context == null || message == null) {
return;
}
String text = "";
if (message.getActionType() == NotificationAction.clicked.getType()) {
// The notification is clicked on the notification bar
// The application handles actions related to the click
text = "notification opened:" + message;
} else if (message.getActionType() == NotificationAction.delete.getType()) {
// Notification is dismissed
// The application handles related actions after the notification is dismissed
text = "notification dismissed:" + message;
}
Toast.makeText(context, "broadcast that the received notification is clicked:" + message.toString(),
Toast.LENGTH_SHORT).show();
// Get the custom `key-value`
String customContent = message.getCustomContent();
if (customContent != null && customContent.length() != 0) {
try {
JSONObject obj = new JSONObject(customContent);
// key1 is the key configured by the frontend
if (!obj.isNull("key")) {
String value = obj.getString("key");
Log.d(LogTag, "get custom value:" + value);
}
// ...
} catch (JSONException e) {
e.printStackTrace();
}
}
// Handling process of the application.
Log.d(LogTag, text);
show(context, text);
}
```


#### Parameter description

activity: context of opened activity.

#### Returned values

XGPushClickedResult: the opened object of the notification; if the activity is open due to TPNS notification, `XGPushClickedResult` will be returned; otherwise, null will be returned.

#### Class method list

| Method Name | Returned Value | Default Value | Description |
| ------------------ | ------ | ------ | ------------------------------------------------------------ |
| getMsgId()         | long   | 0      | Message ID                                                      |
| getTitle()         | String | None     | Notification title                                                    |
| getContent()       | String | None     | Notification body content                                                 |
| getActivityName()  | String | None     |  Name of the page opened                                             |
| getCustomContent() | String | None     | Custom `key-value`, which is a JSON string. At the same time, call the following method in `onPause()` of Activity |


### Creating notification channel
#### API description
This API is used to create a notification channel.
```java
public static void createNotificationChannel(Context context, String channelId, String channelName, boolean enableVibration, boolean enableLights, boolean enableSound, Uri soundUri)
```

>This API is applicable to v1.1.5.4 and above.

#### Parameter description

- context: context object of current application.
- channelId: notification channel ID.
- channelName: notification channel name.
- enableVibration: whether to enable vibration.
- enableLights: whether to enable LED indicator.
- enableSound: whether to enable sound.
- soundUri: ringtone resource URI, which is valid if `enableSound` is `true`. To use the system-default ringtone, set this parameter to `null`.

#### Sample code
```java
XGPushManager.createNotificationChannel(this.getApplicationContext(),"default_message", "Default notification",true, true, true, null);
```
### Deleting one notification
#### API description

This API is used to dismiss a notification with a specified ID on the notification bar.
```java
public static void cancelNotifaction(Context context, int id) 
```

#### Parameter description
- context: `Context` object.
- id: ID of the notification to be dismissed.

#### Sample code

```java
XGPushManager.cancelNotifaction(context, 1);
```
	
### Dismissing all notifications
#### API description

This API is used to dismiss all notifications of the current application on the notification bar.

```java
public static void cancelAllNotifaction(Context context) 
```
#### Parameter description

- context: `Context` object.

#### Sample code
```java
XGPushManager.cancelAllNotifaction(context);
```

## Tags
### Preset tag

Currently, TPNS provides two types of preset tags:

- Geographic location (at the provincial level).
- Application version number.
- Preset tags are automatically reported in the SDK.



### Setting custom tag

#### API description

You can set tags for different users and then send mass notifications based on tag names on the frontend. An application can have up to 10,000 tags, and each token can have up to 100 tags in one application. If you want to increase the limits, please submit a ticket for assistance. Each custom tag can be bound to an unlimited number of device tokens, and no spaces are allowed in the tag.

```java
public static void setTag(Context context, String tagName) 
```



#### Parameter description

- context: `Context` object.
- tagName: name of the tag to be set, which cannot be null or empty.



#### Processing result

The result can be obtained by reloading the `onSetTagResult` method of `XGPushBaseReceiver`.

#### Sample code

```java
XGPushManager.setTag(this, "male"); 
```



### Setting multiple tags

#### API description

Setting multiple tags at a time will override tags previously set for this device.

```java
public static void setTags(Context context, String operateName, Set<String> tags) 
```



#### Parameter description

- context: `Context` object.
- operateName: user-defined operation name. The callback result will return it as-is, which is used to identify to which operation the callback belongs.
- tags: a collection of tag names, and each tag is a string. Restrictions: each tag cannot exceed 40 bytes (otherwise, the tag will be discarded) or contain spaces (all spaces will be deleted). Up to 100 tags can be set, and excessive ones will be discarded.



#### Processing result

The result can be obtained by reloading the `onSetTagResult` method of `XGPushBaseReceiver`.

#### Sample code

```java
String[] tags = "tag1 tag2".split(" ");
Set<String> tagsSet = new HashSet<>(Arrays.asList(tags));
XGPushManager.setTags(getApplicationContext(), "setTags:" + System.currentTimeMillis(), tagsSet); 

```



### Adding multiple tags

#### API description
Setting multiple tags at a time will not override tags previously set for this device.
- If the newly added tag is in the format of "test:2  level:2", then all historical tags of this device will be deleted, and then `test:2` and `level` tags will be added.
- If the newly added tag has a part without the punctuation mark `:`, such as "test:2  level", then all historical tags of this device will be deleted, and then `test:2` and `level` tags will be added.


>
-  In newly added tags, `:` is the backend keyword. Use it according to your business scenarios.
- This API should be called at a certain interval (an interval of greater than 5s is recommended); otherwise, update may fail.

```java
public static void addTags(Context context, String operateName, Set<String> tags) 

```



#### Parameter description

- context: `Context` object.
- operateName: user-defined operation name. The callback result will return it as-is, which is used to identify to which operation the callback belongs.
- tags: a collection of tag names, and each tag is a string. Restrictions: each tag cannot exceed 40 bytes (otherwise, the tag will be discarded) or contain spaces (all spaces will be deleted). Up to 100 tags can be set, and excessive ones will be discarded.



#### Processing result

The result can be obtained by reloading the `onSetTagResult` method of `XGPushBaseReceiver`.

#### Sample code

```java
String[] tags = "tag1 tag2".split(" ");
Set<String> tagsSet = new HashSet<>(Arrays.asList(tags));
XGPushManager.addTags(getApplicationContext(), "addTags:" + System.currentTimeMillis(), tagsSet);
```



### Deleting tag

#### API description

This is for you to delete user tag data.

```java
public static void deleteTag(Context context, String tagName) 
```

#### Parameter description

- context: `Context` object.
- tagName: name of the tag to be set, which cannot be null or empty.

#### Processing result

The result can be obtained by reloading the `onDeleteTagResult` method of `XGPushBaseReceiver`.

#### Sample code

```java
XGPushManager.deleteTag (this, "male"); 
```



### Deleting multiple tags

#### API description

Delete multiple tags at a time.

```java
public static void deleteTags(Context context, String operateName, Set<String> tags)
```



#### Parameter description

- context: `Context` object.
- operateName: user-defined operation name. The callback result will return it as-is, which is used to identify to which operation the callback belongs.
- tags: a collection of tag names, and each tag is a string. Restrictions: each tag cannot exceed 40 bytes (otherwise, the tag will be discarded) or contain spaces (all spaces will be deleted). Up to 100 tags can be set, and excessive ones will be discarded.



#### Processing result

The result can be obtained by reloading the `onSetTagResult` method of `XGPushBaseReceiver`.

#### Sample code

```java
String[] tags = "tag1 tag2".split(" ");
Set<String> tagsSet = new HashSet<>(Arrays.asList(tags));
XGPushManager.deleteTags(getApplicationContext(), "deleteTags:" + System.currentTimeMillis(), tagsSet);
```



### Clearing all tags

#### API description

Clear all tags of this device.

```java
public static void cleanTags(Context context, String operateName)
```

#### Parameter description

- context: `Context` object.
- operateName: user-defined operation name. The callback result will return it as-is, which is used to identify to which operation the callback belongs.

#### Processing result

The result can be obtained by reloading the `onSetTagResult` method of `XGPushBaseReceiver`.

#### Sample code

```java
XGPushManager.cleanTags(getApplicationContext(), "cleanTags:" + System.currentTimeMillis());
```



## Configuration APIs

All configuration APIs are in the `XGPushConfig` class. In order for the configuration to take effect in time, you need to ensure that configuration APIs are called before launching or registering for TPNS.

### Disabling session keep-alive (1.1.6.1+)

TPNS enables the session keep-alive feature by default. To disable it, please call the following API in `onCreate` of `Application` or `LauncherActivity` during application initialization and pass in `false`:

```java
XGPushConfig.enablePullUpOtherApp(Context context, boolean pullUp);
```
#### Parameter description
- context: application context
- pullUp: true (enable session keep-alive), false (disable session keep-alive)
>If the following log is printed, the session keep-alive feature has been disabled: `I/TPNS: [ServiceUtil] disable pull up other app`.

### Debug mode

#### API description

To ensure data security, make sure debug mode is turned off when publishing.

```java
public static void enableDebug(Context context, boolean debugMode)
```

#### Parameter description

- context: application context object.
- debugMode: the default value is `false`. To enable the debug log, set it to `true`.

<span id="Getting token"></span>

### Getting token

#### API description

Token is the identity ID of a device. It is randomly generated by the server based on the device property and delivered to the local system. The token of the same application varies by device.

```java
public static String getToken(Context context)
```

>A token is generated during the first application registration and will remain in the mobile phone. The token always exists regardless of unregistration. After the application is completely uninstalled and reinstalled, the token will change. The token varies by application.

#### Parameter description

context: application context object.

#### Returned values

A standard token will be returned upon success, and null or "0" upon failure.

### Getting third-party vendor token
#### API description
A third-party token is the identity ID of a vendor device. It is delivered to the local system by the vendor. The token of the same application varies by device.

``` java 
public static String getOtherPushToken(Context context) 
```

>This API can be called only after successful registration; otherwise, null will be returned.


#### Parameter description
context: application context object.

#### Returned values
A standard token will be returned upon success, and null or "0" upon failure.  



### Setting AccessID

#### API description

If it has already been configured in AndroidManifest.xml, it does not need to be called again; if both of them exist, this API will be used.

```java
public static boolean setAccessId(Context context, long accessId)
```

#### Parameter description

- Context: object.
- accessId: `accessId` obtained by registering on the frontend.

#### Returned values

- true: success.
- false: failure.

>The `accessId` set through this API will also be stored in the file.

### Setting AccessKey

#### API description

If it has already been configured in AndroidManifest.xml, it does not need to be called again; if both of them exist, this API will be used.

```java
public static boolean setAccessKey(Context context, String accessKey) 
```

#### Parameter description

- Context: object.
- accessKey: `accesskey` obtained by registering on the frontend.

#### Returned values

- true: success.
- false: failure.

>The `accessKey` set through this API will also be stored in the file.



### New log reporting APIs

#### API description
If you find exceptions with TPush, you can call this API to trigger reporting of local push logs. When feeding back the problem, please provide the file address for us to troubleshoot.
```
public static void uploadLogFile(Context context, HttpRequestCallback httpRequestCallback)
```

#### Parameter description
- context: `Context` object, which cannot be null.
- httpRequestCallback: log reporting result callback, which include callbacks for success and failure and cannot be null.

#### Sample code
```
    XGPushManager.uploadLogFile(context, new HttpRequestCallback() {
        @Override
        public void onSuccess(String result) {
                 Log.d("TPush", "Upload succeeded. File address:" + result);
        }

        @Override
        public void onFailure(int errCode, String errMsg) {
                 Log.d("TPush", "Upload failed. Error code:" + errCode + ", error message:" + errMsg);
        }
    });
```
 
>You need to enable `XGPushConfig.enableDebug(this, true);` first.


