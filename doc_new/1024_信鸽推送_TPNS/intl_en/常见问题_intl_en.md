## Common Android SDK issues

### 1.1   Cannot receive push notifications

Initiate push from the official TPNS website using the Token received. If you did not receive the push notification, troubleshoot the issues accordingly as follows.  

Note: Please make sure you are using the latest SDK version. Issues from older versions could be fixed on the latest version. Refresh web page if the web client has push errors.

#### 1.1.1 Registration successful, but cannot receive push notifications

- Please check if the current App package name matches the name entered when registering TPNS App. If there is any discrepancy, we recommend enabling multiple App package names for pushing.
- Check if there are any mobile device network abnormalities. Switch to 4G network and try again.
- There are two kinds of TPNS push notifications: Notification bar messages and In-App messages. Notification bar messages can be displayed in the notification bar whereas In-App messages cannot.
- Ensure that the phone is functioning normally. Certain phones will restrict TPNS's background process when operating in Do-not-disturb mode, Battery-saver mode or when the battery level is low.
- Check if the device has enabled notification bar permissions. Phones from brands such as OPPO and Vivo require manual enabling of notification bar permissions.

#### 1.1.2 Registration unsuccessful and cannot receive push notifications

- New apps take about 1 minute to sync their data. Registering during this period may result in Error Code 20. Please try again after awhile.

**Parameter Errors**

- Check if access id and access key are properly configured. Common issues include the misuse of the secret key or adding spaces to the front or end of the access key.

**Registration Errors**

- If the Command Tool returns error codes such as 10004, 10002 or 20, please refer to the [Android SDK Error Code Reference List](https://intl.cloud.tencent.com/document/product/1024/30722)

**No callback on registration**

- Check if wup package is added.
- Check if the current network is stable. We recommend trying with 4G networks as Wi-Fi may suffer from a lack of bandwidth due to having too many users.
- Devices released by Nubia in the second half of 2015 and 2016 are all unable to register. Models include the Nubia Z11 series, Nubia Z11S series and the Nubia Z9S series. Only earlier devices are able to register. This includes devices in the Z7 series, My Prague series (applies for TPNS 2.47 and 3.X versions).

#### 1.1.3 Unable to receive push notifications once App is closed

- No current third party push notification guarantees users can receive notifications after the App is closed, as it is the phone custom ROM restricting TPNS service. TPNS service has to be connected to network to enable TPNS activity. Once the service is terminated, re-initiation depends on the system, security software and user controls.
- QQ and WeChat are both whitelisted on the system level, so their services will not be terminated when apps are closed, and users feel like they can receive messages when apps are  closed. As a matter of fact, the service are still running in the background.
- If messages are sent to an Android device after the App is exited and TPNS service is disconnected from the TPNS server, it will become an offline message, which can be stored for up to 72 hours. Each device can store a maximum of 2 offline messages. If offline messages cannot be retrieved upon re-starting the App, please check if the following reversed application endpoint is called: XGPushManager.unregisterPush(this);

#### 1.1.4 Fail to push to Accounts

Accounts, also known as usernames, refers to a user account that has the ability to log onto an App. This extends to all user accounts, even those outside of QQ and WeChat. For example, the QQ's Account is the QQ account number, Gmail&#39;s account is the Gmail address and the Account used for China Telecom is the user&#39;s telephone number.

For users who wish to push notifications according to specific accounts, they must first bind their account with the Token, or else it will fail to push. The binding Android account is bound on registration, through the registerPush(context,account) interface, whereas iOS can configure this via setAccount.

- When choosing Accounts to push to, the &quot;Token not found, check registration.&quot; prompt implies that the Account has not been bound properly to the Token. There are two ways this might happen:

(1) The Account or username has logged off. This is not necessarily due to the App&#39;s call. Under certain circumstances, Accounts may automatically log off.

(2) This device has been registered to another Account or username. If this happens, the original Acccount will be automatically unbound. (A device can only be linked to one username. If the username is already linked to another account, it will return &quot;not found&quot;.)

- After binding the Account, notifications can be sent according to the username (Account). Under normal circumstances, all devices that this Account has recently logged in from will be able to receive notifications. When the user&#39;s Account logs off, call registerPush(context,&quot;\*&quot;) to unbind the current Account.
- Account (username) cannot be a single character. An Account can be bound to at most 100 devices. Only the last bound device can receive push notifications.

#### 1.1.5 Unable to receive Push Tags

Ensure that the Tag is bound correctly. An App can have at most 10,000 Tags, with each Token under the App having at most 100 Tags. No spaces are allowed in Tags.

- **Use server side push SDK to check if Tags and Tokens are bound**
``` php
/**
     * Check Token's Tags
     */public function QueryTokenTags($deviceToken){
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




### 1.2 Issue with push data

**[Pause Push]**

- Restrictions on Push All (V3):


  1.Up to 30 Push All notifications can be sent per hour. Failure will occur when there are more than 30.
  2.The same Push All notification cannot be sent within the same hour. Failure will occur when trying to send the same Push All notification within an hour.

- Restrictions on Tag Pushing (V3):


  1.Up to 30 Tag push notifications can be sent per hour. Failure will occur when there are more than 30.
  2.The same Tag push notification cannot be sent within the same hour. Failure will occur when trying to send the same Tag notification within an hour.

**Result Analysis**

- Next-day: See result data one day after pushing notification.
- Real-time: See results immediately after pushing notification. Currently only supports 14 real-time result analyses every week.

**Actual Delivery Count**

- Number of devices that managed to successfully connect to the TPNS server and receive notifications during the offline storage period. (For example: Offline messages are stored for 3 days, so the Actual Delivery Count will stabilize on the fourth day. The statistics will continuously increase as more and more devices connect to TPNS server.)

**Detailed History**

- Detailed History only displays: Push all, Tag push, and package push. (Batch pushes to Accounts and devices are not supported)

**Statistics Overview**

- Display statistic data for the current day. A certain day&#39;s data is equal to the total push count in that day, inclusive of all kinds of different push notifications. (Separated into single push, broadcast - also known as batch push and push all, notification bar messages and In-App messages)



### 1.3 Message tap event and page redirection

Due to the fact that a tap event will occur whenever a message is tapped on the current SDK, the default tap event is configured to open the main interface. Thus, when redirects are set within the endpoint tap message callback &quot;onNotifactionClickedResult&quot; method, conflicts occur between custom redirects and the default tap event. This results in the user being first redirected to the specified interface, then returning to the main interface afterwards. Therefore, no redirects should be set within &quot;onNotifactionClickedResult&quot;.

**The solution is as follows (first method is recommended):**

**[1] Use Intent to redirect to the desired page (use this method for Android versions 3.2.3 and above)**

- This requires the manifest on the client app to be properly configured to the desired page to be redirected to. For example, if the desired page is AboutActivity:

```java
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

- If the SDK service is used to configure Intent for redirection, Intent can be set to (using Java SDK as an example):

```java
action.setIntent("xgscheme://com.xg.push/notify_detail");
```
- If param1 or param2 needs to be attached, it can be configured as follows:
```java
action.setIntent("xgscheme://com.xg.push/notify_detail?param1=aa&param2=bb");
```

- Endpoint received parameters: In the onCreate method that lies within the target redirection page:
```java
Uri uri = getIntent().getData();
      if (uri ! = null) {                
String url = uri.toString();
String p1= uri.getQueryParameter("param1");
String p2= uri.getQueryParameter("param2");
}
```

**[2] Configure on-tap redirection page of message while sending message**

(a) Deepllink package name + category name can be directly configured in the web end, under advanced functions;

(b) The SetActivity method found under the Action string in the backend Message settings can retrieve related information about messages via XGPushClickedResult: Header, contents and attached parameters.

- The method of configuring backend redirects is as follows (using Java SDK as an example):

```java
XingeApp android = new XingeApp(accessID,secretkey);
Message message_android =new Message();
message_android.setExpireTime(86400);
message_android.setTitle("push test");
message_android.setType(1);
message_android.setContent("android test2");
ClickAction action =new ClickAction();
action.setActivity("com.qq.xgdemo.activity.SettingActivity");
message_android.setAction(action);
JSONObject ret1 = android.pushSingleDevice("token",message_android);
......
```
- The following is how the endpoint receives Message parameters:

```java
//this must be context provided for redirecting on message tap.
XGPushClickedResult clickedResult = XGPushManager.onActivityStarted(this);
//Receive paramters related to message
String ster = clickedResult.getCustomContent();
//Receive message header
String set = clickedResult.getTitle();
//Receive message contents
String s = clickedResult.getContent();
```

**[3] Send the In-App message to the endpoint, the user-customized notification bar. Use local notifications to pop up the notifications, configure page for redirection.**

### 1.4 Issues related to TPNS Android SDK&#39;s integrated Manufacturer Channel

#### 1.4.1 Supported functions on Manufacturer Channel

- Xiaomi&#39;s Channel supports delivery callbacks and In-app notifications, but does not support tap callbacks.
- Huawei&#39;s Channel does not support delivery callbacks, but supports In-app notifications (ignores custom parameters) and tap callbacks (requires custom parameters).
- Meizu&#39;s Channel supports delivery callbacks and tap callbacks, but does not support In-app notifications.

**Note:** Use Intent to obtain parameters from tap callbacks or redirect to the user defined page. [**Tap To View Instructions**](https://intl.cloud.tencent.com/document/product/1024/30720)



### 1.5 Android SDK Related Issues

**Question: Is it compatible with Android P?**

Answer: Version 4.X and higher is compatible with Android P. HTTPS is supported by default. Configure the settings to support HTTP. ([Click to View Configuration Instructions](https://intl.cloud.tencent.com/document/product/1024/30723))

**Question: The Xiaomi Channel does not offer tap callback. How can the user be redirected to the designated page after tapping the message in the notification bar?**

Answer: Use [[intent](https://intl.cloud.tencent.com/document/product/1024/30720)] to redirect for integrated manufacturer channels

**Question: Why can only one push notification be displayed on a device with integrated Xiaomi Channel?**

Answer: The official Xiaomi user guide states: By default, only one push notification is displayed in the notification bar To display multiple notifications in the notification bar, each notification must be assigned a different notify\_id (for notification bar messages with the same notify\_id, only the newest message will be displayed in the notification bar).

**Question: Why is there no detailed history record for push notification?**

Answer: TPNS management platform&#39;s Detailed Histroy displays: single device push, push all, tag push, and the website&#39;s package push. The push records of account list push and device group push by API is not displayed in the management platform.

**Question: How to set up custom ringtone?**

Answer:

1. Management platform setup method: Create Push -\&gt; Notification Bar Message -\&gt; Advanced Settings -\&gt; Alert -\&gt; Custom (For android, select the ringtone file from the raw directory. The ringtone file does not need the filename extension, for example: xg\_ring. For iOS, select the ringtone file from the bundle directory. The ringtone file should contain the filename extension, for example: xg\_ring.wav)

2. Rest API V3 setup method: For Android, set the push notification body&#39;s ring=1 and set ring\_raw with the ringtone file name found under the Android project&#39;s raw directory. The filename extension is not required. For iOS, set the push notification body&#39;s sound with the file name of the ringtone that is located in the bundle directory of the designated project. The filename extension is required.

Note: When integrating manufacturer channels, be aware of Huawei and Meizu&#39;s restrictions. These manufacturers&#39; devices do not allow the use of user defined ringtone files, but use the system&#39;s tones by default. Xiaomi can now allow users to customize the ringtone.

**Question: How to customize the icons in the status bar?**** Why is the icon gray?**

Answer: The ROMs of native Android 5.0 or higher will process the app icons by applying a layer of color causing the icon to become gray if the target sdk is higher or equal to 21. Set the target sdk to be less than 21 to display icons with colors. If you do not wish to set the target sdk to below 21, rename a transparent png image as notification\_icon.png and place the image in the drawable folder. By doing so the icon will still be gray but will have an outline.

**Question: Can push notifications be received after the application closes or when its process ends?**

Answer: TPNS Push relies on the TPNS service for receiving and delivering messages. Killing the process will also kill the service.

The service must be activated or the app must be launched in order to receive notifications. If the device contains other running apps that had integrated TPNS then the services of these running apps can be used to receive messages,

but sharing services is restricted by the device&#39;s ROM therefore the success is not guaranteed.

**Question: How many offline messages can be stored on a single device?**** For how long?**

Answer: Android devices can store up to 2 offline messages while iOS devices can only store 1 message. The offline message can be stored up to 72 hours.

**Question: The compilation for Android version 4.4.4 failed with the error message of Cannot find XGPushProvider and MidProvider?**

Answer: The size of the projects being loaded exceeded 65K and needs to be split.

**Question: What are the restrictions on tags?**

Answer: A single device can have up to 100 tags. A single app can have up to 10,000 different tags.

**Question: After successfully registering for the first time, is it necessary to register again in the future if I had not unregistered?**

Answer: No, if you had not unregistered then there is no need to register again.

**Question: Why is there no callback message after registering the device?**

Answer: There are only three kinds of errors that the backend may encounter throughout the registration process:

    (1) No response;
    
    (2) Returned data package format error;
    
    (3) Error code returned. The client side should be able to detect these errors and respond with callbacks.

**Question: What is the difference between Token and Account?**

Answer: Token is an app&#39;s identification for receiving push notifications while the Account is a specific user&#39;s identification.

**Question: If an account had been registered on device A, can it be registered on device B?**** What is the result of pushing a notification to this account?**

Answer: The notification will be received on device B, but not on device A. Only the last device that was bound to the account will receive the push notification.

**Question: What is the difference between Tag and Account?**

Answer: A Tag is used to tag a token or a user&#39;s properties such as Guangdong province, male, player, etc. An Account is a user&#39;s account.

Do not use a Tag as a username.

**Question:**** An activity page had been designated to be opened, but the redirect fails quite often.**

Answer: The permission to redirect from the notification bar may be restricted on some phones.

Solution: Open the androidManifest.xml and add android:exported=&quot;true&quot; to the activity in question.

**Question: There is a Device Coverage Count in the application list. What is it?**

Answer: This number represents the number of devices or endpoints registered to the application. This number also represents the maximum device coverage for pushing notifications. If the endpoint calls

the unregister interface to unregister then the device coverage count will decrease.

**Question:**** Why are there multiple platforms&#39; .so files, such as armabi and x86, under the libs directory?**

Answer: TPNS had developed .so libraries for all android platforms.

Solution: Delete the unnecessary platform directories. For example, games generally only require armabi therefore the other folders can be deleted.

**Question: Why is the server busy message displayed when pushing from the web?**

Answer: Check whether the Token and the selected push environment are set up correctly. Then check whether the certificate had been submitted successfully. If the problem persists, create a new

certificate without a password and try submitting.

**Question: Can a non-scheduled push (immediate push) be canceled during the push process?**

Answer: No, only tasks that return push\_id can be canceled.

**Question: When checking the pushed list after pushing the notification, why is the push status still displayed as in process despite the notification being delivered already?**

Answer: The page may not have been refreshed, try refreshing the page.

**Question: In what order will push notifications be received when an offline user comes on line?**

Answer: According to the notification ID in ascending order. The user also receives the messages in this order therefore the messages will be received in accordance to message&#39;s push order.

**Question: I have Android users and iOS users. Should I develop two different interfaces in my php backend, one for Android users and another for iOS users?**

Answer: The push API needs to be called twice or the two can be encapsulated into one.

**Question: If the designated time for scheduled push is in the past will the notification be pushed?**

Answer: If the designated time is in the past then the notification will be pushed immediately.

**Question: Why is there only sound and no text displayed sometimes when the push notification is received?**

Answer: This issue is related to the system, specific analysis of the device&#39;s logcat is required.

**Question:**** Is TPNS Push supported for overseas users?**

Answer: As long as you are able to ping the TPNS server domain name openapi.xg.qq.com, push notifications can be received.TPNS&#39;s overseas servers are deployed in Hong Kong, therefore

the performance of push notifications overseas will be slightly lower than that in China due to higher network delays overseas.

**Question: Are the APPID data for TPNS and Tencent Open Platform synchronized?**

Answer: When you register on Open Platform and use TPNS, application details will be synchronized between Open Platform and TPNS. There is no need to

access the application again when only using TPNS. However, applications accessed from TPNS will not be synchronized to Open Platform.

**Question:**** Would TPNS be unavailable without a SD card?**

Answer: Nope, logs will just be written in another location.

**Question:**** Can the registration method be created in threads? Is it possible to create them in APPLICATION onCreate?**

Answer: The registration method can be called anywhere. However, do take note of the delivery of applicationContext.

**Question:**** How can we delete Toast notifications which are successfully registered?**

Answer: The Custom Push Receiver in the demo is equipped with its own Toast prompt handling method: Delete Toast in Custom Push Receiver

Related Content

## 2 Common iOS SDK issues

### 2.1 Cannot receive Push notifications

Push notifications involve the collaboration of many associated modules. Abnormalities in any link may result in the failure to receive notifications. The most common issues are as follows:

#### 2.1.1. Client Troubleshooting

- Check Notification System for device.

Please check [Notifications] - [Application Name] and check if notification permissions has been granted to your application.

- Check Network settings for device.

Network issues with the devices may result in the client&#39;s inability to obtain Tokens when registering APNs. This will result in inability to use the TPNS Push Service for selected devices;

Furthermore, even if the client correctly obtains and registers the Tokens to TPNS, the client will still be unable to receive notifications if the device is not connected to network, even with successfully delivery of notifications on the TPNS server. If the device recovers the network connection within a short period of time, it is still possible to receive the notifications (APNs will hold for a period of time before sending the notifications again).

SDK Access Issues. Upon accessing SDK, please ensure that you are able to obtain the Device Token for receiving notifications. For further details, refer to[iOS SDK Integration Guide](https://intl.cloud.tencent.com/document/product/1024/30726).

#### 2.1.2. Server Troubleshooting

- APN Server Issues

As the TPNS service delivers notifications for iOS devices through APNs, notification delivery requests will fail for the TPNS server if there are errors with the APNs.

- TPNS Server Issues

The TPNS server involves the collaboration of multiple function modules to deliver notifications. Should there be a problem with any of the modules, there will be errors with the push notifications.

#### 2.1.3. Push Notification Certificate Troubleshooting

When the TPNS server requests for notification deliveries from APNs, there is a need for two parameters: Push Notification Certificate and Device Tokens. Please ensure that the Push Notification Certificate is valid when requesting push notifications. For Push Notification Certificate settings, please refer to [iOS Push Certificate](https://intl.cloud.tencent.com/document/product/1024/30728).

The [TPNS testing tool](http://xg.qq.com/pigeon_v2/resource/sdk/XGPushTool.zip) can be used to verify server issues. This tool will not only aid in the verification of the TPNS server and APN servers, it will also be able to verify the validity of Push Notification Certificates and generate formats for TPNS-specific Push Notification Certificates automatically.

**Certificates usually require an estimated 5 minutes to take effect upon submission to the TPNS Management Platform.**



### 2.2 Account/Tag Binding and Unbinding functions are not working.

When using SDK API to bind or unbind accounts and tags, the TPNS server requires about 10 seconds to synchronize data.



### 2.3 Register Token Interface cannot be found in the new version.

Device Token registration has been automated for iOS SDK 3.1.0 + versions and later, and will be processed internally by SDK. There is no longer a need for manual trigger by developers.

### 2.4 Do the badge quantities for iOS applications support automatic configuration?

The TPNS server does not support logic control of badge quantities at the moment as research and development is still underway.

Should there be an urgent need for automatic configuration, the accessor is required to retrieve the API for badge quantities from the client and report to the accessor server for logic control.

### 2.5 Other common iOS SDK issues

#### 2.5.1. The device prompts for error &quot;No valid &#39;aps-environment&#39; entitlement string found&quot; .

Please check whether the bundle id configured in the Xcode project matches the configured Provision Profile file, and whether the Provision Profile file corresponding to the app has been configured with the message push capability.

#### 2.5.2 How is the client redirected depending on message content and other responses?

When the iOS device receives a push notification and the user taps on the push notification to open the application, the application should process the action according to different situations:

- If the app is not currently running, this function will be called.

If launchOptions include UIApplicationLaunchOptionsRemoteNotificationKey, it means that the user activated the app by tapping on the push notification;

If the corresponding key values are not included, the app was not activated by the tapping of notifications. The app can then be activated by tapping the icon or other gestures.

**Code examples**

- (BOOL)application: (UIApplication \*)application didFinishLaunchingWithOptions: (NSDictionary \*)launchOptions

{

    // Receive Message Content
    
    NSDictionary \*remoteNotification = [launchOptions objectForKey:UIApplicationLaunchOptionsRemoteNotificationKey];
    
    // Process logically according to the content of messages

}

- If the app is currently in the foreground or active in the background,

based on the system version iOS 7.0+, there is a need to use the following function if you use the Remote Notification feature.

- (void)application: (UIApplication \*)application didReceiveRemoteNotification: (NSDictionary \*)userInfo fetchCompletionHandler: (void (^)(UIBackgroundFetchResult))completionHandler;

based on the system version iOS 10.0+, there is a need to use the new UserNotifications Framework to process if you use the Remote Notification feature. For versions after iOS TPNS SDK3.1.0, TPNS SDK has encapsulated the new framework so please use the two methods in the XGPushDelegate protocol:

**Code examples**

- (void)xgPushUserNotificationCenter: (UNUserNotificationCenter \*)center didReceiveNotificationResponse: (UNNotificationResponse \*)response withCompletionHandler: (void (^)(void))completionHandler {

    NSLog(@&quot;[XGDemo] click notification&quot;);

    completionHandler();

}

// Call out this interface when the app is pushing notifications while in foreground

- (void)xgPushUserNotificationCenter: (UNUserNotificationCenter \*)center willPresentNotification: (UNNotification \*)notification withCompletionHandler: (void (^)(UNNotificationPresentationOptions))completionHandler {

    completionHandler(UNNotificationPresentationOptionBadge | UNNotificationPresentationOptionSound | UNNotificationPresentationOptionAlert);

}

#### 2.5.3 How does the client play custom push message audio?

Firstly on the terminal development side, place the audio file in the bundle directory; if the TPNS Management Platform is used to create the push notification, fill in the audio file name in [Advanced Settings] (full path of audio file not required). If the REST API is used to call, set the sound parameter to the audio file name (full path of audio file not required).

#### 2.5.4 Does iOS support offline saving?

No. The TPNS server sends the message requests to APNs. If the APNs discover that the device is offline, APNs will hold for a period of time. APNs have not provided a specific answer to the exact timing.

#### 2.5.5 Why is delivered data unavailable for iOS?

Prior to iOS 9.x, the operating system did not provide an API interface to monitor messages delivered to the terminal, thus making it impossible to collect the statistics. For iOS 10.0+, the operating system provided a Service Extension interface which can be called by the client to monitor delivery of messages. However, the statistics for TPNS iOS does not include this portion of data currently, please stay tuned.

#### 2.5.6 How to create a silent push with TPNS server SDK?

Assign a value of 1 to the parameter content-available without using alert, badge, sound.



## 3 Other common issues

1.  Q: Is the nubiaUI V6.0 system supported by TPNS Push?

 A: No, nubia includes a Super Energy Saving feature which will kill the background process very quickly. The older versions of nubia are supported.

2.    Q: Will the Android 0 (target=26) version of Android force kill background resident server processes?

       A: Yes. If the specific target=26 compiled application runs on top of all these systems, service will be further restricted alongside a great reduction in the persistence capability for this system version when the app is not in the foreground.

3. Q: Will it be restricted by the Doze mechanism?

   A: Yes, Android 6.0 and above are restricted by the Doze mechanism. The service will be in sleep mode after a period of time if the app is not added to the whitelist.

4. Q: Why are notifications not shown on Oppo or Vivo systems?

   A: For customized systems such as Oppo or Vivo, TPNS is able to receive notifications. However, as the app&#39;s default notification bar display permission is turned off, notifications cannot be displayed and requires the client to guide the user in enabling the function.

5. Q: If notifications meant for overseas delivery (app log-in from overseas) are pushed from the Chinese servers to TPNS, will there be delays or congestion for the notifications in this case? If yes, how long will they last?

A: Currently, notifications are released overseas from the Tencent dedicated line if going through the fcm channel. The process flow would be



[Client Server] - Public Network -\&gt; [TPNS REST API Server] - Internal Line -\&gt; Hong Kong Node - Public Network -\&gt; [Google Server]

The most time-consuming stage is the transfer out of mainland China. However, it is still fast (within 10ms) becaused a dedicated internal line is used. Only one network operator is used for the whole process to take advantage of the same carrier traffic rather than cross-operator traffic. As a result, the entire network process can be finished within 100ms.

Therefore, any latency is usually not caused by network issues, but due to offline devices, FCM heartbeat maintenance, etc.

Congestion happens with concurrent occurrences of peak periods. This situation should not happen to the current VIP cluster. As messages are all sent to the fcm server in real time, the concurrent capacity can be increased through extensions for machine linearity in situations of congestion.




