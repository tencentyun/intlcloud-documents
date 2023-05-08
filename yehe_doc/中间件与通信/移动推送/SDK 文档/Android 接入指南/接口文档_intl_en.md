## Actions
The account feature and tag deletion feature in this document are available for SDK v1.2.3.0 and later. For versions earlier than v1.2.3.0, see [Accounts and Tags](https://www.tencentcloud.com/document/product/1024/40596).

The package name path prefix of all APIs is `com.tencent.android.tpush`. The following table lists important classes that provide APIs for external use.

| Class | Description |
| ------------------ | ------------------------------------------------------------ |
| XGPushManager     | Push service                                            |
| XGPushConfig      | Push service configuration item API |
| XGPushBaseReceiver | Receiver to receive messages and result feedback, which needs to be statically registered by yourself in `AndroidManifest.xml` |

## Launch and Registration

- The application can use the SDK push service only after successful application registration and Tencent Push Notification Service launch. Before launch and registration, ensure that `AccessId` and `AccessKey` have already been configured.
- The new version of SDK has integrated Tencent Push Notification Service launch and application registration into the registration API, which means you can simply call the registration API to complete the launch and registration by default.
- After a successful registration, the device token will be returned. The token uniquely identifies the device and is also the unique ID for Tencent Push Notification Service to stay connected with the backend. For more information on how to get tokens, see [Getting a device token](#.E8.8E.B7.E5.8F.96.E8.AE.BE.E5.A4.87-token).

The registration API usually provides a compact version and a version with callback. Please choose an appropriate version according to your business needs.

### Registering a device

The following are device registration API methods. For more information on the timing and principle of calls, see [Device registration flow](https://www.tencentcloud.com/document/product/1024/32609#device-registration-flow).

#### API description

Standard registration only registers the current device, and the backend can send different push messages based on device tokens. There are two versions of the API method:

```java
public static void registerPush(Context context)
```

#### Parameter description

`context`: Context object of the current application, which cannot be `null`

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

- `context`: Context object of the current application, which cannot be `null`
- `callback`: Callback functions, including success and failure callbacks and cannot be `null`

#### Sample code

```java
XGPushManager.registerPush(this, new XGIOperateCallback() {
	@Override
	public void onSuccess(Object data, int flag) {
		Log.d("TPush", "Registration succeeded. Device token: " + data);
	}
	@Override
	public void onFail(Object data, int errCode, String msg) {
		Log.d("TPush", "Registration failed. Error code: " + errCode + "; error message: " + msg);
	}
})
```

### Getting the registration result

There are two ways to check if the registration is successful.

**Using the Callback version of the registration API**
The `XGIOperateCallback` class provides an API to process registration success or failure. Please see the sample in the registration API.

#### Sample code

```java
/**
* Operation callback API
*/
public interface XGIOperateCallback {
	/**
	* Callback when the operation is successful
	* @param data //Business data of a successful operation, such as the token information when registration is successful
	* @param flag //Flag tag
	*/
	public void onSuccess(Object data, int flag);
	/**
	* Callback when the operation fails
	* @param data //Business data of a failed operation
	* @param errCode: Error code
	* @param msg //Error message
	*/
	public void onFail(Object data, int errCode, String msg);
}
```

**Inheriting XGPushBaseReceiver**
The registration result can be obtained by rewriting the `onRegisterResult` method of `XGPushBaseReceiver`.

>? The inherited `XGPushBaseReceiver` subclass needs to be configured in `AndroidManifest.xml`. For more information, see [Message configuration](#.E6.B6.88.E6.81.AF.E9.85.8D.E7.BD.AE) below.
>
#### Sample code

```java
/**
*
* @param context //Current context
* @param errorCode //`0` indicates success, while other values are error codes
* @param message //Returned registration result
*/
@Override
public void onRegisterResult(Context context, int errorCode, XGPushRegisterResult message) {
			if (context == null || message == null) {
				return;
			}
			String text = "";
			if (errorCode == XGPushBaseReceiver.SUCCESS) {       // Registration succeeded
				// Get the token here
				String token = message.getToken();
				text = "Registration succeeded. Token:" + token;
			} else {
				text = message + "Registration failed. Error code:" + errorCode;
			}
			Log.d(LogTag, text);
}
```

#### Class method list

| Method | Returned Value | Default Value | Description |
| --------------- | ------ | ------ | ------------------------------- |
| getToken()      | String | None     | Device token, i.e., unique device ID |
| getAccessId()   | long   | 0      | Gets `AccessId` for registration            |
| getAccount      | String | None     | Gets the account bound for registration |
| getTicket()     | String | None     | Login state ticket                      |
| getTicketType() | short  | 0      | Ticket type                        |

### Unregistration

The following are unregistration API methods. For more information on the timing and principle of calls, see device unregistration flow [here](https://www.tencentcloud.com/document/product/1024/32609).

>! After calling the unregistration API, you need to call the registration API again before you can receive pushed messages.
>
#### API description

When a user has logged out or the application is closed and it is no longer necessary to receive push messages, the device can be unregistered from the application. (Once the device is unregistered, push messages will no longer be received unless the device is successfully registered again).

```java
public static void unregisterPush(Context context)
```

#### Parameter description

`context`: Context object of the application


#### Sample code

```java
XGPushManager.unregisterPush(getApplicationContext(), new XGIOperateCallback() {
    @Override
    public void onSuccess(Object data, int i) {
        Log.d("TPush", "Unregistration succeeded");
    }
    @Override
    public void onFail(Object data, int errCode, String msg) {
        Log.d("TPush", "Unregistration failed. Error code: " + errCode + ", error message: " + msg);
    }
});
```


### Getting the unregistration result

The unregistration result can be obtained by rewriting the `onUnregisterResult` method of `XGPushBaseReceiver`.

>?
> - Frequent unregistration is not recommended because it may cause delay in backend sync.
> - Switching accounts does not require unregistration. With multiple registrations, the last registration will automatically take effect.
> 
#### Sample code

```java
/**
* Unregistration result
* @param context //Current context
* @param errorCode //0 indicates success, while other values are error codes
*/
@Override
public void onUnregisterResult(Context context, int errorCode) {
	if (context == null) {
           return;
	 }
	String text = "";
	if (errorCode == XGPushBaseReceiver.SUCCESS) {
		 text = "Unregistration succeeded";
	} else {
		 text = "Unregistration failed" + errorCode;
	}
	Log.d(LogTag, text);
}
```

## Push Notification (Displayed on the Notification Bar)

Push notifications are content displayed on the notification bar of devices. All operations are performed by the Tencent Push Notification Service SDK. Applications can listen for clicks on notifications. In other words, push notifications delivered on the frontend do not need to be processed by applications and will be displayed on the notification bar by default.

>?
> - After the Tencent Push Notification Service is successfully registered, notifications can be delivered without any configuration.
> - In general, combined with custom notification styles, standard notifications can meet most business needs. If you need more flexible pushes, consider using messages.
> 
### Getting notifications

#### API description

The Tencent Push Notification Service SDK provides a callback API for developers to get the content of arrived notifications. Notifications can be obtained by rewriting the `onNotificationShowedResult(Context, XGPushShowedResult)` method of `XGPushBaseReceiver`. Here, the `XGPushShowedResult` object provides an API for reading notification content.

>! Some vendor channel SDKs do not provide a callback method for notification arrival, and vendor channels' arrival callback methods cannot be triggered unless the app process is running. Therefore, the callback API `onNotificationShowedResult` provided in the Tencent Push Notification Service SDK supports listening for the arrival of notifications delivered only through the Tencent Push Notification Service channel, but not through vendor channels.
>
```java
public abstract void onNotificationShowedResult(Context context,XGPushShowedResult notifiShowedRlt); 
```

#### Parameter description

- `context`: Context of current application
- `notifiShowedRlt`: arrived notification object

### Getting notification click results

#### Notification callback listening and custom parameter interpretation

The Tencent Push Notification Service SDK collects statistics on notification/message arrivals and notification clicks and clearances by default. The SDK provides a callback API for developers to listen for notification click events. Notification click events can be obtained by rewriting the `onNotificationClickedResult(Context, XGPushClickedResult)` method of XGPushBaseReceiver.

>?
> - Tencent Push Notification Service SDK v1.2.0.1 or later supports listening for the click events of notifications delivered through the Tencent Push Notification Service channel and various vendor channels.
> - Do not include a redirection action in this callback API. The SDK will automatically perform notification tap-to-redirect based on the redirection action set in the push task. If you want to deliver and get custom push parameters, the Intent mode is recommended. For more information, see [Notification Tap-to-Redirect](https://www.tencentcloud.com/document/product/1024/38354).
> 
#### API description

```java
public abstract void onNotificationClickedResult(Context context, XGPushClickedResult notifiClickedRlt); 
```

#### Sample code

```java
// If `actionType` of the notification click callback is `0`, the message was clicked; if it is `2`, the message was cleared
@Override
public void onNotificationClickedResult(Context context, XGPushClickedResult message) {
    if (context == null || message == null) {
        return;
    }
    String text = "";
    if (message.getActionType() == NotificationAction.clicked.getType()) {
        // The notification is clicked on the notification bar
        // The application handles actions related to the click
        text = "notification opened:" + message;
    } else if (message.getActionType() == NotificationAction.delete.getType()) {
        // Notification is cleared
        // The application handles related actions after the notification is cleared
        text = "notification cleared:" + message;
    }
  
    // Handling process of the application
  
    Log.d(LogTag, "broadcast that the notification is received:" + text);
}
```

#### Parameter description

- `context`: Context of current application
- `XGPushClickedResult`: Opened object of the notification

Methods of `XGPushClickedResult` class are as follows:

| Method | Returned Value | Default Value | Description |
| ---------------- | ------ | ------ | ------------------------------------------------------------ |
| getMsgId()         | long   | 0      | Message ID                                                      |
| getTitle()         | String | None     | Notification title                                                    |
| getContent()       | String | None     | Notification body content                                                 |
| getActionType()  | String | None     | 0: The notification is clicked; 2: The notification is cleared                       |
| getPushChannel() | String | 100    | ID of the channel through which the clicked notification is delivered <li>100: Tencent Push Notification Service channel </li><li>101: FCM channel </li><li>102: Huawei channel </li><li>103: Mi channel </li><li>104: vivo channel </li><li>105: OPPO channel </li><li>106: Meizu channel </li> |


### Clearing all notifications

#### API description

This API is used to clear all notifications of the current application on the notification bar.

```java
public static void cancelAllNotifaction(Context context) 
```

#### Parameter description

`context`: `Context` object

#### Sample code

```java
XGPushManager.cancelAllNotifaction(context);
```

### Creating a notification channel

#### API description

This API is used to create a notification channel.

```java
public static void createNotificationChannel(Context context, String channelId, String channelName, boolean enableVibration, boolean enableLights, boolean enableSound, Uri soundUri)
```

>? This API is applicable only to v1.1.5.4 or later.
>
#### Parameter description

- `context`: Context of current application
- `channelId`: Notification channel ID
- `channelName`: Notification channel name
- `enableVibration`: Whether to enable vibration
- `enableLights`: Whether to enable LED indicator
- `enableSound`: Whether to enable sound
- `soundUri`: Ringtone resource URI, which is valid if `enableSound` is `true`. To use the system-default ringtone, set this parameter to `null`.

#### Sample code

```
// Place the sound file under the Android project resource directory `raw`. Take the file `ring.mp3` as an example.
String uri = "android.resource://" + context.getPackageName() + "/" + R.raw.ring;
Uri soundUri = Uri.parse(uri);
XGPushManager.createNotificationChannel(context, "default_message", "Default notification", true, true, true, soundUri);
```

## Push Message (Not Displayed on the Notification Bar)

Push messages are content delivered to an application by Tencent Push Notification Service. The application needs to inherit the `XGPushBaseReceiver` API to implement and handle all the operations on its own. In other words, delivered messages are not displayed on the notification bar by default, and Tencent Push Notification Service is responsible only for delivering messages from the Tencent Push Notification Service server to the application, but not processing the messages. The messages need to be processed by the application.

Message refers to the text message delivered by you through console or backend scripts. Tencent Push Notification Service is only responsible for delivering the message to the application, while the application is fully responsible for handling the message body on its own.
- Because the message is flexible and highly customizable, it is suitable for applications to handle custom business needs on their own, such as delivering application configuration information and customizing message retention and display.

<span id="Message configuration"></span>

### Message configuration

Inherit `XGPushBaseReceiver` and configure the following in the configuration file:

#### Sample code

```xml
<receiver android:name="com.tencent.android.xg.cloud.demo.MessageReceiver">
	<intent-filter>
		<!-- Receive in-app messages -->
		<action android:name="com.tencent.android.xg.vip.action.PUSH_MESSAGE" />
		<!-- Listen for results of registration, unregistration, tag setting/deletion, and notification clicks -->
		<action android:name="com.tencent.android.xg.vip.action.FEEDBACK" />
	</intent-filter>
</receiver>

```

### Getting in-app messages

A message delivered by a developer in the console can be received by the application if it inherits `XGPushBaseReceiver` and rewrites the `onTextMessage` method. After successfully receiving the message, the application can handle it based on specific business scenarios.

>? Please make sure that the receiver has been registered in `AndroidManifest.xml`, i.e., `YOUR_PACKAGE.XGPushBaseReceiver` is set.
>
```java
public void onTextMessage(Context context,XGPushTextMessage message)
```

#### Parameter description

- `context`: Current context of the application
- `message`: Received message structure

#### Class method list

| Method | Returned Value | Default Value | Description |
| ------------------ | ------ | ------ | ---------------------------------------------------- |
| getContent()       | String | None     | Message body content, and generally it is sufficient to deliver only this field |
| getCustomContent() | String | None     | Customer `key-value` of message                                 |
| getTitle()         | String | None | Message title (the description of the in-app message delivered from the console is not a title) |


## In-App Message Display
Starting with SDK v1.2.7.0, you can set whether to allow the display of in-app message windows. For example, you can enable the display of in-app message windows in one Activity page, while disable it in another Activity page.

>! In-app messages are displayed based on the Android WebView framework. By default, the in-app message display WebView provided by the Tencent Push Notification Service SDK runs in the main process of an app. **Since Android 9, apps can no longer share a single WebView data directory among multiple processes. If your app must use WebView instances in multiple processes, you must first use the `WebView.setDataDirectorySuffix()` method to specify a unique data directory suffix for each process; otherwise, app crash may occur**. The sample configuration code is as follows:
>```java
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.P) {     
    // Starting with Android 9, you need to set different WebView data directories for the WebView instances of apps’ non-main processes.
    String processName = getProcessName()
    if (processName != null 
            && !processName.equals(context.getPackageName())) {
        WebView.setDataDirectorySuffix(processName)
    }
}
```
> Reference document: [Behavior changes: apps targeting API level 28+](https://developer.android.com/about/versions/pie/android-9.0-changes-28?hl=en#web-data-dirs) (Google Developers).
### Setting whether to allow the display of in-app message windows
```java
XGPushConfig.enableShowInMsg(Context context, boolean flag);
```
#### Parameter description

`context`: `Context` object
`flag`: Whether to allow in-app message display. `true`: Allow; `false`: Not allow; default: `false`.

#### Sample code
```java
XGPushConfig.enableShowInMsg(context, true);
```


## Local Notification

### Adding local notifications

Local notifications are customized by users and saved locally. When an application is open, the Tencent Push Notification Service SDK will determine whether there is a notification once every five minutes based on the network heartbeat. Local notifications will pop up only if the service is enabled, and there may be a delay of about five minutes. A notification will pop up when the time set is earlier than the current device time.

#### Sample code

```java	
// Create a local notification
XGLocalMessage local_msg = new XGLocalMessage();
// Set the local message type; 1: Notification, 2: Message
local_msg.setType(1);
// Set the message title
local_msg.setTitle("qq");
// Set the message content
local_msg.setContent("ww");
// Set the message date in the format of 20140502
local_msg.setDate("20140930");
// Set the hour when the message is triggered (in 24-hour clock system); for example: 22 indicates 10 p.m.
local_msg.setHour("19");
// Set the minute when the message is triggered, for example: `05` indicates the 5th minute in the hour
local_msg.setMin("31");
// Set the message style. The default value is 0 or not set
local_msg.setBuilderId(0);
// Set the action type: 1 - open the activity or the app itself; 2 - open the browser; 3 - open the Intent; 4 - open the application by the package name
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
// Add the notification to the local system     
XGPushManager.addLocalNotification(context,local_msg);
```



### Clearing local notifications

#### API description

This API is used to clear local notifications that are created by the application but have not popped up.

```java
public static void clearLocalNotifications(Context context) 
```

#### Parameter description

`context`: `Context` object

#### Sample code

```java
XGPushManager.clearLocalNotifications(context);
```

## Account Management

The following are account management API methods. For more information on the timing and principle of calls, see account flow [here](https://www.tencentcloud.com/document/product/1024/32609).


### Adding an account

#### API description

This API is used to add or update an account. If there is no account of this type, it will add a new one; otherwise, it will overwrite the existing one.

```java
public static void upsertAccounts(Context context, List<AccountInfo> accountInfoList, XGIOperateCallback callback)
```

#### Parameter description

- `context`: `Context` object
- `accountInfoList`: Account list, containing account types and account names
- `callback`: Callback of account binding operation

#### Sample code

```java
XGIOperateCallback xgiOperateCallback = new XGIOperateCallback() {
    @Override
    public void onSuccess(Object data, int flag) {
        Log.i("TPush", "onSuccess, data:" + data + ", flag:" + flag);
    }
    @Override
    public void onFail(Object data, int errCode, String msg) {
        Log.w("TPush", "onFail, data:" + data + ", code:" + errCode + ", msg:" + msg);
    }
};
List<XGPushManager.AccountInfo> accountInfoList = new ArrayList<>();
accountInfoList.add(new XGPushManager.AccountInfo(XGPushManager.AccountType.UNKNOWN.getValue(), "account-test"));
XGPushManager.upsertAccounts(context, accountInfoList, xgiOperateCallback);
```

>?
> - Each account can be bound to up to 100 tokens.
> - The account can be email address, mobile number, username, etc. For account type values, see [Account Type Value Table](https://www.tencentcloud.com/document/product/1024/40598).
> - If multiple devices are bound to the same account, the backend will push the message to the last bound device by default. If you want to push to all the bound devices, you can view the `account_push_type` parameter settings in [Push API](https://www.tencentcloud.com/document/product/1024/33764).
> 
### Adding a mobile number

#### API description

This API is used to add or update a mobile number. If you have bound any mobile number before, it will overwrite the original number; if you haven’t, it will be bound (SDK 1.2.5.0+).

>? The mobile number format is `+[country or area code][subscriber number]`, for example, +8613711112222 (where there is a `+` sign in the front, `86` is the country code, and `13711112222` is the subscriber number). If the entered mobile number does not contain a **country or area code**, Tencent Push Notification Service will automatically add `+86` as the prefix when sending SMS messages. If the mobile number contains a **country or area code**, it will be bound as is. To delete the bound mobile number, call the `delAccountsByKeys` API and set `accountTypeSet` to `1002`.
>
```java
public static void upsertPhoneNumber(Context context, String phoneNumber, XGIOperateCallback callback) 
```

#### Parameter description

- `context`: `Context` object
- `phoneNumber`: An E.164 mobile number in the format of `[+][country code or area code][mobile number]`, for example, +8613711112222
- `callback`: Callback of mobile number binding operation

#### Sample code

```java
XGIOperateCallback xgiOperateCallback = new XGIOperateCallback() {
  @Override
  public void onSuccess(Object data, int flag) {
      Log.i("TPush", "onSuccess, data:" + data + ", flag:" + flag);
  }
   @Override
  public void onFail(Object data, int errCode, String msg) {
      Log.w("TPush", "onFail, data:" + data + ", code:" + errCode + ", msg:" + msg);
  }
};
XGPushManager.upsertPhoneNumber(context, phoneNumber, xgiOperateCallback);
```

### Unbinding an account


#### API description

This API is used to unbind a bound account.

```java
// Unbind the specified account (with registration callback)
void delAccount(Context context, final String account, XGIOperateCallback callback)	
// Unbind the specified account (without registration callback)
void delAccount(Context context, final String account )
```
>? Account unbinding just removes the association between the token and the application account. If full/tag/token push is used, notifications/messages can still be received.
>
#### Parameter description
- `context`: Context object of the current application, which cannot be `null`
- `account`: Account
#### Sample code
```java
XGPushManager.delAccount(getApplicationContext(),"test");
```
### Unbinding by account type
#### API description
This API is used to unbind accounts of one or multiple types. (SDK v1.2.3.0+)
```java
public static void delAccounts(Context context, final Set<Integer> accountTypeSet, XGIOperateCallback callback)
```
#### Parameter description
- `context`: `Context` object
- `accountTypeSet`: Type of the account to be unbound
- `callback`: Callback of account unbinding operation
#### Sample code
```java
XGIOperateCallback xgiOperateCallback = new XGIOperateCallback() {
    @Override
    public void onSuccess(Object data, int flag) {
        Log.i("TPush", "onSuccess, data:" + data + ", flag:" + flag);
    }
    @Override
    public void onFail(Object data, int errCode, String msg) {
        Log.w("TPush", "onFail, data:" + data + ", code:" + errCode + ", msg:" + msg);
    }
};
        
Set<Integer> accountTypeSet = new HashSet<>();
accountTypeSet.add(XGPushManager.AccountType.CUSTOM.getValue());
accountTypeSet.add(XGPushManager.AccountType.IMEI.getValue());
XGPushManager.delAccounts(context, accountTypeSet, xgiOperateCallback);
```
### Clearing all accounts
>? The `delAllAccount` API is disused in SDK v1.2.2.0. The `clearAccounts` API is recommended.
>
#### API description
This API is used to unbind all bound accounts.
```java
// Unbind all accounts (with registration callback)
void clearAccounts(Context context, XGIOperateCallback callback)
// Unbind all accounts (without registration callback)
void clearAccounts(Context context)
```
> ? Account unbinding just removes the association between the token and the application account. If full/tag/token push is used, notifications/messages can still be received.
#### Parameter description
`context`: Context object of the current application, which cannot be `null`
#### Sample code
```java
XGPushManager.clearAccounts(getApplicationContext());
```
## Bucket Tag
The following are tag management API methods. For more information on the timing and principle of calls, see tag flow [here](https://www.tencentcloud.com/document/product/1024/32609).
### Preset tags
Currently, Tencent Push Notification Service preset tags include application version, system version, province, active information, system language, SDK version, country/region, phone brand, and phone model tags. Preset tags are automatically reported in the SDK.
### Overwriting multiple tags
#### API description
Setting multiple tags at a time will overwrite tags previously set for this device.
You can set tags for different users and then send mass notifications based on tag names. An application can have up to 10,000 tags, and each token can have up to 100 tags in one application. If you want to increase the limits, [contact our online customer service](https://cloud.tencent.com/act/event/Online_service). Each custom tag can be bound to an unlimited number of device tokens, and no spaces are allowed in the tag.
```java
public static void clearAndAppendTags(Context context, String operateName, Set<String> tags) 
```
#### Parameter description
- `context`: `Context` object
- `operateName`: User-defined operation name. The callback result will return it as-is, which is used to identify the operation to which the callback belongs.
- tags: A collection of tag names, and each tag is a string. Restrictions: Each tag cannot exceed 50 bytes (otherwise, the tag will be discarded) nor contain spaces (all spaces will be deleted). Up to 100 tags can be set, and excessive ones will be discarded.
#### Processing result
The result can be obtained by rewriting the `onSetTagResult` method of `XGPushBaseReceiver`.
#### Sample code
```java
String[] tags = "tag1 tag2".split(" ");
Set<String> tagsSet = new HashSet<>(Arrays.asList(tags));
XGPushManager.clearAndAppendTags(getApplicationContext(), "clearAndAppendTags :" + System.currentTimeMillis(), tagsSet); 
```
### Adding multiple tags
>? The `addTags` API is disused in SDK v1.2.2.0. The `appendTags` API is recommended.
>
#### API description
- If all tags to be added contain a colon (:), for example, `test:2, level:2`, all `test:*` and `level:*` tags bound with the device will be deleted before the `test:2` and `level:2` tags are added.
- If certain tags to be added do not contain a colon (:), for example, `test:2  level`, all historical tags of the device will be deleted before the `test:2` and `level` tags are added.
>? In newly added tags, a colon (:) is the backend keyword. Use it according to your business scenarios.
>
- This API should be called at a certain interval (an interval longer than 5 seconds is recommended); otherwise, update may fail.
```java
public static void appendTags(Context context, String operateName, Set<String> tags) 
```
#### Parameter description
- `context`: `Context` object
- `operateName`: User-defined operation name. The callback result will return it as-is, which is used to identify the operation to which the callback belongs.
- tags: A collection of tag names, and each tag is a string. Restrictions: Each tag cannot exceed 50 bytes (otherwise, the tag will be discarded) nor contain spaces (all spaces will be deleted). Up to 100 tags can be set, and excessive ones will be discarded.
#### Processing result
The result can be obtained by rewriting the `onSetTagResult` method of `XGPushBaseReceiver`.
#### Sample code
```java
String[] tags = "tag1 tag2".split(" ");
Set<String> tagsSet = new HashSet<>(Arrays.asList(tags));
XGPushManager.appendTags(getApplicationContext(), "appendTags:" + System.currentTimeMillis(), tagsSet);
```
### Deleting multiple tags
>? The `deleteTags` API is disused in SDK v1.2.2.0. The `delTags` API is recommended.
>
#### API description
This API is used to delete multiple tags at a time.
```java
public static void delTags(Context context, String operateName, Set<String> tags, XGIOperateCallback callback) 
```
#### Parameter description
- `context`: `Context` object
- `operateName`: User-defined operation name. The callback result will return it as-is, which is used to identify the operation to which the callback belongs.
- tags: A collection of tag names, and each tag is a string. Restrictions: Each tag cannot exceed 50 bytes (otherwise, the tag will be discarded) nor contain spaces (all spaces will be deleted). Up to 100 tags can be set, and excessive ones will be discarded.
- `callback`: Callback of tag deletion operation
#### Processing result
The result can be obtained by rewriting the `onSetTagResult` method of `XGPushBaseReceiver`.
#### Sample code
```java
XGIOperateCallback xgiOperateCallback = new XGIOperateCallback() {
    @Override
    public void onSuccess(Object data, int flag) {
        Log.i("TPush", "onSuccess, data:" + data + ", flag:" + flag);
    }
    @Override
    public void onFail(Object data, int errCode, String msg) {
        Log.w("TPush", "onFail, data:" + data + ", code:" + errCode + ", msg:" + msg);
    }
};
        
Set<String> tagSet = new HashSet<>();
tagSet.add("tag1");
tagSet.add("tag2");
XGPushManager.delTags(context, "delTags", tagSet, xgiOperateCallback);
```
### Clearing all tags
>? The `cleanTags` API is disused in SDK v1.2.2.0 and later versions. You are advised to use the `clearTags` API.
>
#### API description
This API is used to clear all tags of a device.
```java
public static void clearTags(Context context, String operateName, XGIOperateCallback callback)
```
#### Parameter description
- `context`: `Context` object
- `operateName`: User-defined operation name. The callback result will return it as-is, which is used to identify the operation to which the callback belongs.
- `callback`: Callback of tag clearing operation
#### Processing result
The result can be obtained by rewriting the `onSetTagResult` method of `XGPushBaseReceiver`.
#### Sample code
```java
XGIOperateCallback xgiOperateCallback = new XGIOperateCallback() {
    @Override
    public void onSuccess(Object data, int flag) {
        Log.i("TPush", "onSuccess, data:" + data + ", flag:" + flag);
    }
    @Override
    public void onFail(Object data, int errCode, String msg) {
        Log.w("TPush", "onFail, data:" + data + ", code:" + errCode + ", msg:" + msg);
    }
};
        
XGPushManager.clearTags(context, "clearTags", xgiOperateCallback);
```
### Querying tags
>? This API is used to get the tags bound to a device and available only for v1.2.5.0 and later.
>
#### API description
This API is used to get the tags bound to the device.
```java
    public static void queryTags(final Context context, final String operateName, final int offset, final int limit, final XGIOperateCallback callback)
```
#### Parameter description
- `context`: `Context` object.
- `operateName`: Operation name defined by the user. The callback result will be returned as-is for users to distinguish the operation.
- `offset`: Starting point
- `limit`: Number of tags to get; maximum value: `100`
- `callback`: Callback of tag getting operation
#### Processing result
The result can be obtained by rewriting the `onQueryTagsResult` method of `XGPushBaseReceiver`.
#### Sample code
```java
XGIOperateCallback xgiOperateCallback = new XGIOperateCallback() {
    @Override
    public void onSuccess(Object data, int flag) {
        Log.i("TPush", "onSuccess, data:" + data + ", flag:" + flag);
    }
    @Override
    public void onFail(Object data, int errCode, String msg) {
        Log.w("TPush", "onFail, data:" + data + ", code:" + errCode + ", msg:" + msg);
    }
};
XGPushManager.queryTags(context, 0, 100, xgiOperateCallback);
```
## User Attribute Management
You can set attributes for different users and then perform personalized push in Tencent Push Notification Service. The following are user attribute API methods. For more information on the timing and principle of calls, see user attribute flow [here](https://www.tencentcloud.com/document/product/1024/32609).
### Adding user attributes
#### API description
This API is used to add an attribute (with callback). If there is no attribute, it will add one; otherwise, it will overwrite the existing one.
```java
public static void upsertAttributes(Context context, String operateName, Map<String, String> attributes, XGIOperateCallback callback)
```
#### Parameter description
- `context`: `Context` object
- `operateName`: Operation name defined by the user. The callback result will be returned as-is for users to distinguish the operation.
- `attributes`: Attribute set, where each attribute is identified by `key-value`
- `callback`: Callback of attribute adding operation
> !	
>
> 1. Attributes are transferred through key-value pairs, and only non-empty strings can be accepted.
> 2. There can be up to 50 attributes.
> 3. Both the `key` and `value` of an attribute can contain up to 50 characters.
#### Sample code
```java
XGIOperateCallback xgiOperateCallback = new XGIOperateCallback() {
    @Override
    public void onSuccess(Object data, int flag) {
        log("action - onSuccess, data:" + data + ", flag:" + flag);
    }
    @Override
    public void onFail(Object data, int errCode, String msg) {
        log("action - onFail, data:" + data + ", code:" + errCode + ", msg:" + msg);
    }
};
        
Map<String,String> attr = new HashMap<>();
attr.put("name", "coding-test");
attr.put("gender", "male");
attr.put("age", "100");
XGPushManager.upsertAttributes(context, "addAttributes-test", attr, xgiOperateCallback);
```
### Deleting a user attribute
#### API description
This API is used to delete a specified attribute.
```java
public static void delAttributes(Context context, String operateName, Set<String> attributes, XGIOperateCallback callback)
```
#### Parameter description
- `context`: `Context` object
- `operateName`: Operation name defined by the user. The callback result will be returned as-is for users to distinguish the operation.
- `attributes`: Attribute set, where each attribute is identified by `key-value`
- `callback`: Callback of attribute deleting operation
> !	
>
> 1. Attributes are transferred through key-value pairs, and only non-empty strings can be accepted.
> 2. There can be up to 50 attributes.
> 3. Both the `key` and `value` of an attribute can contain up to 50 characters.
#### Sample code
```java
XGIOperateCallback xgiOperateCallback = new XGIOperateCallback() {
    @Override
    public void onSuccess(Object data, int flag) {
        log("action - onSuccess, data:" + data + ", flag:" + flag);
    }
    @Override
    public void onFail(Object data, int errCode, String msg) {
        log("action - onFail, data:" + data + ", code:" + errCode + ", msg:" + msg);
    }
};
Set<String> stringSet = new HashSet<>();
stringSet.add("name");
stringSet.add("gender");
                
XGPushManager.delAttributes(context, "delAttributes-test", stringSet, xgiOperateCallback);
```
### Clearing all user attributes
#### API description
This API is used to delete all configured attributes.
```java
public static void clearAttributes(Context context, String operateName, XGIOperateCallback callback)
```
#### Parameter description
- `context`: `Context` object
- `operateName`: Operation name defined by the user. The callback result will be returned as-is for users to distinguish the operation.
- `callback`: Callback of attribute clearing operation
#### Sample code
```java
XGIOperateCallback xgiOperateCallback = new XGIOperateCallback() {
    @Override
    public void onSuccess(Object data, int flag) {
        log("action - onSuccess, data:" + data + ", flag:" + flag);
    }
    @Override
    public void onFail(Object data, int errCode, String msg) {
        log("action - onFail, data:" + data + ", code:" + errCode + ", msg:" + msg);
    }
};
        
XGPushManager.clearAttributes(context, "cleanAttributes-test", xgiOperateCallback);
```
### Updating user attributes
#### API description
This API is used to set an attribute (with callback). It will overwrite all the attributes previously set for this device (i.e., clearing and setting).
> !	
>
> 1. Attributes are transferred through key-value pairs, and only non-empty strings can be accepted.
> 2. There can be up to 50 attributes.
> 3. Both the `key` and `value` of an attribute can contain up to 50 characters.
```java
public static void clearAndAppendAttributes(Context context, String operateName, Map<String, String> attributes, XGIOperateCallback callback)
```
#### Parameter description
- `context`: `Context` object
- `operateName`: Operation name defined by the user. The callback result will be returned as-is for users to distinguish the operation.
- `attributes`: Attribute set, where each attribute is identified by `key-value`
- `callback`: Callback of attribute setting operation
#### Sample code
```java
XGIOperateCallback xgiOperateCallback = new XGIOperateCallback() {
    @Override
    public void onSuccess(Object data, int flag) {
        log("action - onSuccess, data:" + data + ", flag:" + flag);
    }
    @Override
    public void onFail(Object data, int errCode, String msg) {
        log("action - onFail, data:" + data + ", code:" + errCode + ", msg:" + msg);
    }
};
        
Map<String,String> attr = new HashMap<>();
attr.put("name", "coding-test");
attr.put("gender", "male");
attr.put("age", "100");
XGPushManager.clearAndAppendAttributes(context, "setAttributes-test", attr, xgiOperateCallback);
```
## Configuration APIs
All configuration APIs are in the `XGPushConfig` class. For configurations to take effect in time, you need to ensure that configuration APIs are called before launching or registering Tencent Push Notification Service.
### Disabling session keep-alive (1.1.6.1+)
Tencent Push Notification Service enables the session keep-alive feature by default. To disable it, please call the following API in `onCreate` of `Application` or `LauncherActivity` during application initialization and pass in `false`:
```java
XGPushConfig.enablePullUpOtherApp(Context context, boolean pullUp);
```
>? Starting from Tencent Push Notification Service SDK v1.2.6.0, the session keep-alive feature is disabled by default, and you do not need to call this API.
>
#### Parameter description
- `context`: Application context
- `pullUp`: `true` (enable session keep-alive); `false` (disable session keep-alive)
>? If the following log is printed, the session keep-alive feature has been disabled: `I/TPNS: [ServiceUtil] disable pull up other app`.
>
#### Sample code
```java
XGPushConfig.enablePullUpOtherApp(context, false); // Default value: true (enable keep-alive)
```
### Debug mode
#### API description
To ensure data security, make sure the debug mode is turned off when publishing.
```java
public static void enableDebug(Context context, boolean debugMode)
```
#### Parameter description
- `context`: Context object of the application
- `debugMode`: The default value is `false`. To enable debug logging, set it to `true`.
#### Sample code
```java
XGPushConfig.enableDebug(context, true); // Default value: false (do not enable)
```
<span id="Getting token"></span>
### Getting a device token
#### API description
A token is the unique ID for Tencent Push Notification Service to stay connected with the backend and the unique ID for an application to receive messages. A device token can be obtained only after the device is successfully registered. The obtaining methods are described as follows. (The Tencent Push Notification Service token may change if the application is uninstalled and reinstalled.)
#### 1. Through the registration API with callback
In the `onSuccess(Object data, int flag)` method of the registration API with `XGIOperateCallback`, the `data` parameter is the token. For more information, see the relevant sample of the registration API.
#### 2. Inheriting XGPushBaseReceiver
Rewrite the `onRegisterResult (Context context, int errorCode,XGPushRegisterResult registerMessage)` method of `XGPushBaseReceiver` and get the token through the `getToken` API provided by the `registerMessage` parameter. For more information, see [Getting registration results](#.E8.8E.B7.E5.8F.96.E6.B3.A8.E5.86.8C.E7.BB.93.E6.9E.9C).
#### 3. Through the XGPushConfig.getToken(context) API
Once the device is successfully registered, the token will be stored locally and then can be obtained through the `XGPushConfig.getToken(context)` API.
Token is the identity ID of a device. It is randomly generated by the server based on the device attributes and delivered to the local system. The token of the same application varies by device.
```java
public static String getToken(Context context)
```
>? A token is generated during the first application registration and will be stored in the mobile phone. The token always exists regardless of whether unregistration is performed subsequently. After the application is uninstalled and reinstalled, the token will change. The token varies by application.
>
#### Parameter description
`context`: Context object of the application
#### Sample code
```java
XGPushConfig.getToken(context);
```
#### Returned values
A standard token will be returned upon success, and `null` or `0` upon failure.
### Getting a third-party vendor token
#### API description
A third-party token is the identity ID of a vendor device. It is delivered to the local system by the vendor. The token of the same application varies by device.
```java 
public static String getOtherPushToken(Context context) 
```
> ? This API can be called only after successful registration; otherwise, `null` will be returned.
#### Parameter description
`context`: Context object of the application
#### Sample code
```java
XGPushConfig.getOtherPushToken(context);
```
#### Returned values
A standard token will be returned upon success, and `null` or `0` upon failure.  
### Getting custom parameters (custom_content) delivered with the notification on the notification click target page
This is a new API in the SDK v1.3.2.0. When a notification is clicked and opened, you can use this API to directly get the custom parameters (custom_content) configured when creating the push task on the target notification setting page.
For usage details, see [Notification Tap-to-Redirect](https://intl.cloud.tencent.com/document/product/1024/38354#rest-api-.E4.BD.BF.E7.94.A8).
``` 
public static String getCustomContentFromIntent(Context context, Intent intent)
```
#### Returned values
Strings of the custom parameters (custom_content) delivered with the push 
#### Parameter description
- `context`: `Context` object, which cannot be `null`
- intent: Activity intent. Directly pass in `this.getIntent()` in onCreate, and pass in the `intent` called back in onNewIntent.
[](id:examplecode)
#### Sample code
```
String customContent = XGPushManager.getCustomContentFromIntent(this, intent);
```
### Setting the `AccessID`
#### API description
If the `accessKey` is already set in `AndroidManifest.xml`, you do not need to call this API again; if you still call this API, the `accessKey` set through this API will prevail.
```java
public static boolean setAccessId(Context context, long accessId)
```
#### Parameter description
- `Context`: Object
- `accessId`: `accessId` obtained through registration in the console
#### Sample code
```java
long accessId = 0L; // `accessId` of the current application
XGPushConfig.setAccessId(context, accessId);
```
#### Returned values
- true: Success.
- false: Failure.
>? The `accessId` set through this API will also be stored in the `AndroidManifest.xml` file.
>
### Setting the `accessKey`
#### API description
If the `accessKey` is already set in `AndroidManifest.xml`, you do not need to call this API again; if you still call this API, the `accessKey` set through this API will prevail.
```java
public static boolean setAccessKey(Context context, String accessKey) 
```
#### Parameter description
- `Context`: Object
- `accessKey`: `accessKey` obtained through registration in the console
#### Sample code
```java
String accessKey = ""; // `accessKey` of your application
XGPushConfig.setAccessKey(context, accessKey);
```
#### Returned values
- true: Success.
- false: Failure.
>? The access key set through this API will also be stored in the `AndroidManifest.xml` file.
>
### Reporting logs
#### API description
If you find exceptions with TPush, you can call this API to trigger reporting of local push logs. To report the problem, [contact our online customer service](https://cloud.tencent.com/act/event/Online_service) with the file address provided to facilitate troubleshooting.
```
public static void uploadLogFile(Context context, HttpRequestCallback httpRequestCallback)
```
#### Parameter description
- `context`: `Context` object, which cannot be `null`
- `httpRequestCallback`: Log reporting result callback, which include callbacks for success and failure and cannot be `null`
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
>?You need to enable `XGPushConfig.enableDebug(this, true);` first.
