
# FAQs

## Issues with Push Data

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

---
## FAQs
**Q: What if the system prompts that the number package is invalid when I try to upload a number package for push to the console?**

A: If you compress a folder using the zip command on macOS, the hidden files will be compressed too, making the console unable to recognize the zipped package. It is recommended to compress the folder on Windows or retry after deleting the hidden files on macOS.
**Q: What if error 48, 10302, or 10303 is returned for account push?**

A: Check whether the token is bound to the account. For more information, see [Account-device Binding Query](https://xg.qq.com/docs/server_api/v3/account-api.html#账号-设备绑定查询（批量操作）).

**Q: Why can't the pushes be received on a Nubia phone?**
```
A: At present, TPNS does not support Nubia phones released after 2015, because the new version of Nubia operating system has a super power-saving feature which will kill background processes very quickly. Therefor, the TPNS service cannot be started normally, making it impossible to register successfully.

```

**Q: What if the pushes can be received in the development environment on iOS but not in the production environment after packaging?**
```
A:
1. Check whether the file archived-expanded-entitlements.xcent is present in the package.
If not, an error may occur:

No valid 'aps-environment' entitlement string found for application 'com.xxx.xxx': (null).

Solution: Go to TARGET -> Build Setting -> Code Signing Identity -> Code Signing Entitlements
 Check whether there is the aps-environment field; if not, add it. 
<plist version="1.0">
<dict>
	<key>aps-environment</key>
	<string>production</string>
</dict>
</plist>

2. If the device prompts for error "Error Domain=NSCocoaErrorDomain Code=3000" "No valid 'aps-environment' entitlement string found" or "UserInfo=0x16545fc0 {NSLocalizedDescription= No valid 'aps-environment' entitlement string found}":
Check whether the bundle id configured in the Xcode project matches the configured Provision Profile file, and whether the Provision Profile file corresponding to the app has been configured with the message push capability.
```



**Q: Why is the iOS token invalid?**
```
A: 
(1) The system was logged out or the app was uninstalled
(2) The user installed the app on a new device
(3) The user restored the device from a backup
(4) The user reinstalled the OS
(5) Other system-defined events (1. After calling the unregisterNotification API, register the notification again and clear device data and settings)

```
**Q: How to generate a pem certificate for TPNS?**
```
A: 
(1) Download the TPNS testing tool on the iOS app configuration page.
(2) Upload a p12 certificate and push a message successfully to APNs using a TPNS token.
(3) The tool will generate the pem certificate required by TPNS in the directory of the p12 certificate.
```

**Q: Why cannot pushed be received in the production environment?**

```

A: The production environment must meet the following testing conditions: The app is the ad-hoc/App Store build (with the release certificate "Production"), and the release certificate is uploaded and successfully verified.
```


**Q: Is TPNS currently adapted to Android P?**


A: V4.X is already compatible with Android P. HTTPS is used by default. If you want to use HTTP, you need to configure it by yourself ([Click here to view the configuration method](http://docs.developer.qq.com/xg/android_access/android_p_compatibility.html)).


**Q: What if "[TPush] channelId is not initialized" appears in the log for v4.X?**

```

A: This is a internal log of TPNS and does not affect registration.
```

**Q: What if "Server response error code:404, error:{"ret":-1, "msg":"invalid appkey"}" appears in the log for v4.X?**


A: The MTA SDK is embedded in the TPNS SDK. This log is an MTA log and does not affect the registration in TPNS.

**Q: What if the log prints out "otherpushToken = null" when I register with a vendor-specific channel?**

```

A: 1. TPNS v4.X integrates the vendor-specific channels in a dynamic loading manner. When the app is launched for the first time, the vendor dex configuration package corresponding to the phone model will be downloaded. After the download is completed, the app process will be killed and the registration will be done when the app is restarted.
2. If the dex configuration package cannot be downloaded at all, you can use the non-dynamic loading method to integrate it. In this case, you need to use the TPNS v4.X jar without the vendor-specific channels and then integrate the jars of each vendor-specific channel. For more information about how to integrate, see the relevant document.

```



**Q: After the Mi channel is integrated, there is no tap callback. How to achieve redirection to the specified page when the notification bar message is tapped?**


A: The integrated vendor-specific channel must use the [intent](http://docs.developer.qq.com/xg/android_access/android_faq.html#消息点击事件以及跳转页面方法) method to redirect.

**Q: Why can only one push message be displayed on a device that has integrated the Mi channel?**

```
A: According to the documentation at Mi's official website, the notification bar only displays one push message by default. If you want multiple messages to be displayed in the notification bar, you need to set a unique notify_id for different messages (a new notification bar message with the same notify_id will override the previous one).

```
**Q: Is there a limit to the number of messages displayed in the device notification bar? Why is a message not displayed after it arrives at the device?**

```
A: There is no limit to the number of notification bar messages that a phone can receive and display. The reasons for not displaying may include:
(1) The notification bar on a Mi phone displays the latest message by default. If you want multiple messages to be displayed, you need to set a unique n_id for different messages.
(2) The message broadcast is blocked by a phone manager app.
(3) A Meizu phone has a message box, and uncommon messages will go directly to the message box. The messages can be viewed there.
```

**Q: Why is there no historical record after a push is sent?**

```
A: The details of push history displayed in the TPNS console include device push, full push, tag push, and number package push. Account list push and device group push through APIs will not be displayed in the console.
```


**Q: How to set a custom ringtone?**

```
A:
1. In the console: Go to Create a push > Notification bar message > Advanced settings > Reminder mode > Customize (for Android, select the ringtone file in the raw directory, which does not need the extension, such as xg_ring. For iOS, select the ringtone file in the bundle directory, which requires the extension, such as xg_ring.wav).
2. In Rest API V3: For Android, set ring=1 in the push message body, and set ring_raw to the name of the specified ringtone file without the extension in the raw directory of the Android project. For iOS, set the sound in the push message body to the name of the specified ringtone file with the extension in the bundle directory of the project.
Note: If the client has integrated a vendor-specific channel, due to the limitations of Huawei and Meizu, custom ringtone file is not allowed on their phones, and the system sound will be used by default. Currently, custom ringtone can be used on Mi phones.

```
**Q: How to customize the icon in the status bar? Why is the icon gray?**

```
A: ROMs running native Android 5.0 or above will process icon of an app and add a layer of color if target sdk is greater than or equal to 21, causing the icon to be gray. If you want to display it as colored, you need to set the target sdk to below 21. If you don't want the target sdk to be below 21, you can rename a transparent background .png image to notification_icon.png and place it in drawable; in this way, the icon will be displayed as gray but shaped.
```




**Q: Can an app still receive push messages after it is closed or its process is ended?**

```
A: TPNS mainly uses the TPNS service to push and receive messages. When the process is killed, the TPNS service will also be killed. 
Only after the service is pulled back or the app is restarted can the messages be received and pushed. If another app accessing TPNS is launched on the phone, messages can be received and pushed using the service of that app.
However, the shared service channel is also limited by the phone's ROM, and 100% success rate cannot be guaranteed.
```
**Q: How many offline messages can be retained for a single device? And how long can they be retained?**

```
A: TPNS only retains two offline messages: If the device receives multiple messages when it is offline, TPNS will only retain the last two ones, and the previous ones will be lost. When the device goes back online, only the last two messages can be received.
```


**Q: What if Android v4.4.4 prompts a compiling error where XGPushProvider and MidProvider can be found?**

```
A: If the number of loading methods in the project exceeds 65 K, please create subpackages for the project.
```

**Q: What are the restrictions on tags?**

```
A: A maximum of 100 tags can be set for a single device, and one single app can have up to 10,000 different tags.
```

**Q: After the initial registration is successful, no unregistration is performed. Do I need to register again afterward?**

```
A: No, as long as no unregistration is performed, you do not need to register again.
```

**Q: Why can't callback information be received for device registration?**

```
A: In the registration operation, there are only three types of errors in the backend:

(1) No response;

(2) A data packet in a wrong format is returned;

(3) An error code is returned. The device should be able to detect all these three types of errors and give a callback accordingly.
```

**Q: What is the difference between token and account?**

```
A: Token is the identifier of the app for receiving the push message (device); while account is the identifier of a user.
```

**Q: If an account is logged in to on device A and then on device B, what happens when a message is sent to this account?**

```
A: Device B can receive the push, but device A cannot, as only the last device bound to the account can receive pushes.
```

**Q: What is the difference between tag and account?**

```
A: A tag is used to identify a token or a user's attributes, such as Guangdong, male, and gamers. An account is the user's account. Please do not use tags as aliases.

```

**Q: What if I specified to open an activity page but it often cannot be redirected to normally?**

```
A: On some phones, redirection upon tap on the notification bar may have permission issues.
Solution: In AndroidManifest.xml, add android:exported="true" to the activity to be opened.
```

**Q: What does the "number of covered devices" in the app list mean?**

```
A: It refers to the number of devices on which the app is in registered status. It is also the maximum number of devices that the app can cover when pushing a message. If a device calls the unregister API for unregistration, the number of covered devices will decrease.

```

**Q: Why are there many platform-specific .so files in the libs directory, such as armabi and x86?**

```
A: TPNS has developed the .so libraries for all Android platforms.
Solution: You can delete the unwanted platform-specific directories. For example, if your game only has armabi, you can delete other directories.
```

**Q: Why is the server busy when I push on the web side?**

```
A: Please check whether the token and the selected push environment are correct, then check whether the certificate has been submitted correctly. If the error persists, you can create a new certificate without a password, submit it, and retry.

```

**Q: Can a non-scheduled push (i.e., immediate push) be canceled during the pushing process?**

```
A: No. Only tasks that return the push_id can be canceled.
```

**Q: When I check the push list after performing a push task, it shows that the push has been completed, but its status is displayed as "pushing". What should I do?**

```
A: The webpage has a delay. Please refresh and retry.
```

**Q: What is the order in which multiple push messages are received after the user goes back online?**

```
A: They are in the ascending order by message ID. The client also receives messages according to this rule; there, the order in which the messages are received is the same as that in which they are sent.
```

**Q: I have Android users and iOS users. Do I have to write two different APIs in the PHP backend for pushes to users on different platforms?**

```
A: You need to call two push APIs to encapsulate them as one.
```

**Q: If a past time is selected for a scheduled push, will the push be sent?**

```
A: If a past time is selected, the system will send the push immediately.
```

**Q: Why is there only sound but no text when a push notification arrives?**

```
A: This issue has a lot to do with the system. You need to analyze the cause using the logcat of the device.
```

**Q: Can TPNS push messages to regions outside mainland China?**

```
A: As long as the TPNS server's domain name (openapi.xg.qq.com) is pingable, push messages can be received. The global server of TPNS is deployed in Hong Kong, but due to high network latency in overseas regions, the push effect of TPNS is slightly inferior to that in mainland China.

```

**Q: Is the APPID data of TPNS and the Tencent Open Platform interconnected?**

```
A: After you register your app on the open platform and use TPNS, the app information will be automatically synchronized from the open platform to the TPNS platform, so that you don't need to register the app again when using TPNS alone.
 However, apps registered with TPNS won't be synchronized to the open platform.
```

**Q: Can TPNS be used if there is no SD card?**

```
A: It can be used, but the location where the log is stored is different.
```

**Q: Can the registration method be created in the thread? Can it be created in APPLICATON onCreate?**

```
A: The registration method can be called anywhere, but the applicationContext needs to be passed.
```

**Q: How to delete the Toast prompt for successful registration?**

```
A: The CustomPushReceiver in the demo comes with a Toast prompt processing method, which is to delete the content of the Toast inside CustomPushReceiver.

```

## Issues with Payments
**Q: What if my order cannot be placed as the system prompts that there is already a VIP package corresponding with the access_id?**

```
A: Please log in to the TPNS console, go to your app, and select "App configuration" > "App information" to check whether there is a VIP package that has not been renewed. If yes, please renew it directly.
```
**Q: What if my order cannot be placed as the system prompts that the access_id is invalid?**

```
A: Please log in to the TPNS console, go to your app, and select "App configuration" > "App information" to check whether the access_id is correct.
```
**Q: Who can I contact if my payment keeps failing?**

```
A: Please call 4009-100-100.
```
**Q: Besides the Tencent business manager, who can I contact if my payment for the order is successful but I cannot proceed with the upgrade process?**

```
A: Please call 4009-100-100 or add xg_push (TPNS assistant) on WeChat and specify "payment issues".
```




















