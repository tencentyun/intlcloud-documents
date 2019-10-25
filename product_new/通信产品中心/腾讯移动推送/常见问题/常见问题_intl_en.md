
# FAQs


**Q: If the push can be received in the developer environment on iOS, why cannot it be received in the production environment after packaging?**

```
A:
1. Check whether the “archived-expanded-entitlements.xcent” file is in the package.
If not, an error may occur:

No valid 'aps-environment' entitlement string found for application 'com.xxx.xxx': (null).

Solution: Go to TARGET -> Build Setting -> Code Signing Identity -> Code Signing Entitlements
 Check whether there is the aps-environment field; if not, add it. 
<plist version="1.0">
<dict>
	<key>aps-environment</key>
	<string>development</string>
</dict>
</plist>

```

**Q: Why can't the push be received in the production environment?**


A: Testing of the production environment must meet the following conditions: The app is ad-hoc package/App Store version (with the release certificate "Production"), and the release certificate is uploaded and successfully verified.


**Q: Why is iOS token invalid?**

A: <br>
(1) The system is logged out or the app is uninstalled<br>
(2) The user installs the app on a new device<br>
(3) The user restores the device from a backup<br>
(4) The user re-installs the OS<br>
(5) Events defined by other systems (1. After calling the unregisterNotification API, register the notification again and clear device data and settings)

**Q: Why can device that has integrated the Mi channel only display one push message?**

A: According to the documentation on Xiaomi's official website, the notification panel by default only displays one push message. If you want to display multiple messages in the notification panel, you need to set different notify_id for different messages (notification panel messages with the same notify_id will override previous ones). The TPNS official parameter is n_id.


**Q: Is there a limit to the number of messages displayed in the device notification panel? Why is the message not displayed after arriving at the device?**


A: <br>There is no limit to the number of notification panel messages a phone can receive and display. If not displayed, the reasons may be:<br>
(1) The notification panel on a Mi phone by default displays the latest message. If you want all messages to be displayed, you need to set the n_id.<br>
(2) The message broadcast is blocked by a phone manager app.<br>
(3) A Meizu phone has a message box, and not commonly used messages will go directly to the message box, where they can be viewed.


**Q: How to set a custom ringtone?**


A: <br>
1. Set in the console: Go to Push Notification > Advanced Settings > Reminder Mode > Sound > Customize. For Android, select the ringtone file in the raw directory, which does not need an extension such as xg_ring. For iOS, select the ringtone file in the bundle directory, which requires an extension such as xg_ring.wav.<br>
2. Set in Rest API V3: For Android, set ring=1 in the push message body, and set ring_raw as the name of the ringtone file in the raw directory of the specified Android project, without any extension. For iOS, set the sound of the push message body as the ringtone file name in the bundle directory of the specified project, with the extension.<br>
Note: If the client has integrated a vendor channel, due to the limitations of Huawei and Meizu, custom ringtone file is not available, and the system sound will be used by default. Currently, the Mi phone supports custom ringtone.


**Q: How do I customize the icon in the status bar?**

A: ROMs in native Android 5.0 and above will process the app icon whose target SDK is greater or equal to 21, adding a layer of color and turning it into grey. If you want an icon with color, set target SDK to a value below 21. If you need the target SDK to be no smaller than 21, rename an image with a clear background and in png format to notification_icon.png and place it in drawable. Thus, the icon will be in gray and has a shape.


**Q: Can an app still receive push messages after it is closed or its process has ended?**


A: <br>
(1) TPNS channel mainly relies on the TPNS service to send and receive messages. If a process ends, the TPNS service will also end, and push messages will only be received after the service is reactivated or the app is restarted. If another app that is connected to TPNS is opened in the mobile phone, you can use other app’s service to receive messages, but the shared service channel is subject to the restriction of the mobile phone’s ROM, and cannot guarantee a 100% success rate.<br>
(2) The vendor channel supports receiving push messages after the process ends.


**Q: What if Android v4.4.4 reports a compiling error where XGPushProvider and MidProvider cannot be found?**

A: As the number of loading methods in the project exceeds 65K, please create sub-packages for the project.



**Q: Why can't device registration receive the callback information?**


A: 

(1) The vendor channel’s callback is returned by the vendor’s server.<br>

(2) Check whether security software has blocked the broadcast.


**Q: If an account is logged into on device A and then on device B, what will happen when a message is sent to this account?**


A: Device B can receive the push, but device A cannot. Only the last device bound to the account can receive the push.


**Q: What if I cannot redirect to another page when opening a specified activity page?**

```
A: On some phones, redirection from a notification panel to another page may incur permission issues.
Solution: In AndroidManifest.xml, add android:exported="true" to the activity you want to open.
```

**Q: When the user goes back online, what is the order in which multiple push messages are received?**

A: Incremental according to the message ID. The client also receives messages according to this rule. Thus, the order in which messages are received is the same as that in which they are sent.

**Q: If the scheduled push selects a time in the past, will the push be sent?**

A: If the time selected is in the past, the system will send the push immediately.


**Q: Can the registration method be created in the thread? Can it be created in APPLICATON onCreate?**

A: The registration method can be called anywhere, but applicationContext needs to be passed in.

























