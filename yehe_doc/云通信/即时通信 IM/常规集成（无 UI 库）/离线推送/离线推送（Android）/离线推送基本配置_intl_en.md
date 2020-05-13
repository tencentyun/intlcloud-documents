## Overview

IM terminal users need to obtain the latest messages at all times. However, due to the limited performance and battery power of mobile devices, when the app is running in the background, IM recommends that you use the system-grade push channels provided by vendors for message notifications to avoid excessive resource consumption caused by maintaining a persistent connection. Compared with third-party push, system-grade push channels provide more stable system-grade persistent connections, enabling users to receive push messages at any time and greatly reducing resource consumption.

Currently, IM supports APNs, MI push, Huawei push, Meizu push, vivo push, OPPO push, and the push services of other vendors. The details are as follows:

<table> 
   <tr> 
     <th nowrap="nowrap">Push Channel</th> 
     <th nowrap="nowrap">System Requirements</th> 
     <th>Conditions</th> 
   </tr> 
   <tr> 
     <td><a href="https://intl.cloud.tencent.com/document/product/1047/34347" target="_blank">APNs</a></td> 
     <td>iOS</td> 
     <td>iOS system push channel, the only iOS push channel</td> 
   </tr> 
   <tr> 
     <td><a href="https://intl.cloud.tencent.com/document/product/1047/34339" target="_blank">MI push</a></td> 
     <td>MIUI</td> 
     <td>Use MI push MiPush_SDK_Client_3_6_12.jar.</td> 
   </tr> 
   <tr> 
     <td><a href="https://intl.cloud.tencent.com/document/product/1047/34340" target="_blank">Huawei push</a></td> 
     <td>EMUI</td> 
     <td>Huawei mobile service versions of 20401300 and later, SDK version push:2.6.3.301</td> 
   </tr> 
   <tr> 
     <td nowrap="nowrap"><a href="https://intl.cloud.tencent.com/document/product/1047/34341" target="_blank">Google FCM push</a></td> 
     <td nowrap="nowrap">Android 4.1 and later versions</td> 
     <td>The mobile phone needs to install Google Play Services and be used outside Mainland China.</td> 
   </tr> 
   <tr> 
     <td><a href="https://intl.cloud.tencent.com/document/product/1047/34342" target="_blank">Meizu push</a></td> 
     <td>Flyme</td> 
     <td>Use Meizu push push-internal:3.6.+.</td> 
   </tr> 
   <tr> 
     <td nowrap="nowrap"><a href="https://intl.cloud.tencent.com/document/product/1047/34344" target="_blank">OPPO push</a></td> 
     <td>ColorOS</td> 
     <td>Not all OPPO models and versions support OPPO push. SDK version mcssdk-2.0.2.jar</td> 
   </tr>  
   <tr> 
     <td nowrap="nowrap"><a href="https://intl.cloud.tencent.com/document/product/1047/34343" target="_blank">vivo push</a></td> 
     <td nowrap="nowrap">FuntouchOS</td> 
     <td>Not all vivo models and versions support vivo push. SDK version: vivo_pushsdk_v2.3.1.jar.</td> 
   </tr> 
</table>


Here, “offline” means that the app is closed by the system or user without logging out. In such cases, if you want to receive IM SDK message reminders, you can integrate IM offline push.

>
> - Users who have logged out normally or have been forced offline will not receive any message notifications.
> - Currently, offline push notifications are only supported for [ordinary chat messages](https://intl.cloud.tencent.com/document/product/1047/34320), and not for [system messages](https://intl.cloud.tencent.com/document/product/1047/34320#.E7.B3.BB.E7.BB.9F.E6.B6.88.E6.81.AF).

## Basic Configuration of IM SDK Offline Push
### Setting global offline push configuration
The IM SDK provides a feature for setting a global offline push configuration, allowing users to set whether to enable offline push and the alert sound when receiving offline push messages. The setting method is `setOfflinePushSettings` provided by `TIMManager`.

>
> - Calls to this method take effect only after successful login.
> - Currently, only APNs custom alert sounds are supported, and the audio file needs to be a built-in audio file in the app.

**Prototype:**

```java
/**
 * Initializing offline push configuration. The settings take effect only after login.
 * @param settings Offline push configuration information
 */
public void setOfflinePushSettings(TIMOfflinePushSettings settings)

/**
 * Obtaining offline push configuration from the server. It can be obtained only after login.
 * @param cb Callback. The offline push configuration is returned in the onSuccess parameter.
 */
public void getOfflinePushSettings(final TIMValueCallBack<TIMOfflinePushSettings> cb)
```

**Parameter description:**

| Parameter | Description |
|---|---|
| settings | Offline push configuration |

**TIMOfflinePushSettings description:**

```java
/**
 * Obtaining whether the feature is enabled
 * @return true: enabled. false: not enabled.
 */
public boolean isEnabled()

/**
 * Setting whether to enable offline push
 * @param enabled Whether to enable offline push
 */
public void setEnabled(boolean enabled)

/**
 * Obtaining the alert sound for receiving offline push for C2C messages
 * @return URI of the audio file. If it has not been set, ‘null’ is returned.
 */
public Uri getC2cMsgRemindSound()

/**
 * Setting the alert sound for receiving offline push for C2C messages
 * @param c2cMsgRemindSound URI of the audio file. To restore the default sound, enter ‘null’.
 */
public void setC2cMsgRemindSound(Uri c2cMsgRemindSound)

/**
 * Obtaining the alert sound for receiving offline push for group messages
 * @return URI of the audio file. If it has not been set, ‘null’ is returned.
 */
public Uri getGroupMsgRemindSound()

/**
 * Setting the alert sound for receiving offline push for group messages
 * @param groupMsgRemindSound URI of the audio file. To restore the default sound, enter ‘null’.
 */
public void setGroupMsgRemindSound(Uri groupMsgRemindSound)
```

**Example:**

```java
TIMOfflinePushSettings settings = new TIMOfflinePushSettings();
//Enable offline push
settings.setEnabled(true);
//Set the alert sound for receiving offline C2C messages. In this example, the audio file is stored in the res/raw folder.
settings.setC2cMsgRemindSound(Uri.parse("android.resource://" + getPackageName() + "/" + R.raw.dudulu));
//Set the alert sound for receiving offline group messages. In this example, the audio file is stored in the res/raw folder.
settings.setGroupMsgRemindSound(Uri.parse("android.resource://" + getPackageName() + "/" + R.raw.dudulu));

TIMManager.getInstance().setOfflinePushSettings(settings);
```

### Setting offline push for a single message
The IM SDK provides a feature to set offline push configurations for specific messages. For any specified message, developers can set whether to enable offline push, the alert sound when receiving offline push messages, the offline push message description, and extension fields.

>
> - The offline push configuration for an individual message has the highest priority. That is, if a global offline push configuration and single-message offline push configuration are both set, the latter will prevail.
> - Currently, only APNs custom alert sounds are supported, and the audio file needs to be a built-in audio file in the app.


**Prototype:**

```java
/**
 * Setting the configuration for the time when the target user receives an offline push notification for the current message (optional, set when sending the message)
 * @param settings Offline push configuration
 */
public void setOfflinePushSettings(TIMMessageOfflinePushSettings settings)

/**
 * Obtaining offline push configuration for the current message
 * @return Offline push configuration. If the sender has not set it, ‘null’ is returned.
 */
public TIMMessageOfflinePushSettings getOfflinePushSettings()
```

**`TIMMessageOfflinePushSettings`：**

```java
/**
 * Display title for offline push on both iOS and Android platforms. If you want to set the display title for the two platforms separately, set IOSSettings -> title and AndroidSettings -> title.
 *
 * @param title Notification bar title
 * @return
 */
public TIMMessageOfflinePushSettings setTitle(String title)

/**
 * Display text for offline push on both iOS and Android platforms. If you want to set the display text for the two platforms separately, set IOSSettings -> desc and AndroidSettings -> desc.
 * @param descr Text content
 */
public TIMMessageOfflinePushSettings setDescr(String descr)

/**
 * Obtaining the offline push display content of the current message
 * @return Text content
 */
public String getDescr()

/**
 * Setting the extension field of the current message (optional, set when sending the message)
 * @param ext Extension field content
 */
public TIMMessageOfflinePushSettings setExt(byte[] ext)

/**
 * Obtaining the extension field of the current message
 * @return Extension field content. If it has not been set, ‘null’ is returned.
 */
public byte[] getExt()

/**
 * Setting whether the current message allows offline push. By default, it is allowed (optional, set when sending the message)
 * @param enabled true: allow offline push. false: do not allow offline push.
 */
public TIMMessageOfflinePushSettings setEnabled(boolean enabled)

/**
 * Obtaining whether the current message allows push
 * @return Indicates whether the message allows push. true: allows push. false: does not allow push.
 */
public boolean isEnabled()

/**
 * Obtaining the offline push configuration for the current message on Android devices
 * @return Offline push configuration on Android devices
 */
public AndroidSettings getAndroidSettings()

/**
 * Setting the offline push configuration for the current message on Android devices (optional, set when sending the message)
 * @param androidSettings Offline push configuration for the current message on Android devices
 */
public TIMMessageOfflinePushSettings setAndroidSettings(AndroidSettings androidSettings)

/**
 * Obtaining the offline push configuration for the current message on iOS devices
 * @return Offline push configuration on iOS devices
 */
public IOSSettings getIosSettings()

/**
 * Setting the offline push configuration for the current message on iOS devices (optional, set when sending the message)
 * @param iosSettings Offline push configuration for the current message on iOS devices
 */
public TIMMessageOfflinePushSettings setIosSettings(IOSSettings iosSettings)

```

**TIMMessageOfflinePushSettings.AndroidSettings:**

```java
/**
 * Obtaining the notification title
 * @return Notification title
 */
public String getTitle()

/**
 * Setting the title to display for offline push
 
 * @param title Notification title
 */
public AndroidSettings setTitle(String title)

/**
 * Setting the custom text to display for offline push
 *
 * @param desc Display content of notification
 */
public AndroidSettings setDesc(String desc)

/**
 * Obtaining the offline push alert sound URI of the current message on Android devices
 * @return Sound URI. If it has not been set, ‘null’ is returned.
 */
public Uri getSound()

/**
 * Setting the offline push alert sound for the current message on Android devices (optional, set when sending the message)
 * @param sound Sound URI, which supports only built-in audio resource files in apps
 */
public AndroidSettings setSound(Uri sound)

/**
 * Obtaining the notification mode of the current message
 * @return Notification mode
 */
public NotifyMode getNotifyMode()

/**
 * Setting the notification mode of the current message when the receiver receives offline push (optional, will be deprecated soon).
 * 
 * @param mode Notification mode. The default notification mode is ordinary notification bar message mode.
 */
public AndroidSettings setNotifyMode(NotifyMode mode)
```

**TIMMessageOfflinePushSettings.NotifyMode:**

```java
/**
 * Ordinary notification bar message mode. When an offline message is delivered, click the notification bar message to directly launch the app. It will not trigger callback for the app.
 */
NotifyMode.Normal

```

**TIMMessageOfflinePushSettings.IOSSettings:**

```java
/**
 * Setting the title to display for offline push
 *
 * @param title Notification title
 */
public IOSSettings setTitle(String title)

/**
 * Setting the custom text to display for offline push
 *
 * @param desc
 */
public IOSSettings setDesc(String desc)

/**
 * Obtaining the offline push alert sound for the current message on iOS devices
 *
 * @return Audio file path. If it has not been set, ‘null’ is returned.
 */
public String getSound()

/**
 * Setting the offline push alert sound for the current message on iOS devices (optional, set when sending the message)
 *
 * @param sound Audio file path. When it is set to {@see IOSSettings#NO_SOUND_NO_VIBRATION}, it means no alert sound and no vibration.
 */
public void setSound(String sound)

/**
 * Obtaining whether Badge count is enabled for the current message
 *
 * @return true: Badge count is enabled for the current message.
 */
public boolean isBadgeEnabled()

/**
 * Setting whether Badge count is enabled for the current message. By default, it is enabled (optional, set when sending the message).
 *
 * @param badgeEnabled Whether Badge count is enabled
 */
public IOSSettings setBadgeEnabled(boolean badgeEnabled)
```

**Example:**

```java
// Construct a message
TIMMessage msg = new TIMMessage();

// Add text content
TIMTextElem elem = new TIMTextElem();
elem.setText("a new msg from " + selfId);
if(msg.addElement(elem) != 0) {
    Log.d(tag, "addElement failed");
    return;
}

// Set offline push configuration for the current message
TIMMessageOfflinePushSettings settings = new TIMMessageOfflinePushSettings();
settings.setEnabled(true);
// Set the title and content of notification bar messages on iOS and Android platforms. If you want the two platforms to display different titles and content in the notification bars, set them in AndroidSettings and IOSSettings respectively.
settings.setTitle("I'm title");
settings.setDescr("I'm description");
// Set offline push extension information
JSONObject object = new JSONObject();
try {
    object.put("level", 15);
    object.put("task", "TASK15");
    settings.setExt(object.toString().getBytes("utf-8"));
} catch (JSONException e) {
    e.printStackTrace();
} catch (UnsupportedEncodingException e) {
    e.printStackTrace();
}

// Set offline configuration for receiving messages on Android devices
TIMMessageOfflinePushSettings.AndroidSettings androidSettings = new TIMMessageOfflinePushSettings.AndroidSettings();
// Construction mode prior to IM SDK 2.5.3
// TIMMessageOfflinePushSettings.AndroidSettings androidSettings = settings.new AndroidSettings();
// Set the title and content of notification bar messages on Android platform
// androidSettings.setTitle("I'm title for android");
// androidSettings.setDesc("I'm desc for android");
// Set the alert sound for receiving messages on Android devices. The audio file needs to be put in the raw folder.
androidSettings.setSound(Uri.parse("android.resource://" + getPackageName() + "/" +R.raw.hualala));
settings.setAndroidSettings(androidSettings);

//Set offline configuration for receiving messages on iOS devices.
TIMMessageOfflinePushSettings.IOSSettings iosSettings = new TIMMessageOfflinePushSettings.IOSSettings();
//Construction mode prior to IM SDK 2.5.3
//TIMMessageOfflinePushSettings.IOSSettings iosSettings = settings.new IOSSettings();
// Set the title and content of notification bar messages on iOS platform
// iosSettings.setTitle("I'm title for iOS");
// iosSettings.setDesc("I'm desc for iOS");

// Enable the badge count
iosSettings.setBadgeEnabled(true);  
// Set no alert sound and no vibration for receiving messages on iOS devices (new feature introduced by IM SDK 2.5.3)
//iosSettings.setSound(TIMMessageOfflinePushSettings.IOSSettings.NO_SOUND_NO_VIBRATION);
// Set the alert sound for receiving offline messages on iOS devices
iosSettings.setSound("/path/to/sound/file");

msg.setOfflinePushSettings(settings);

// Obtain a one-to-one conversation
TIMConversation conversation = TIMManager.getInstance().getConversation(
        TIMConversationType.C2C,    // Conversation type: one-to-one chat
        peer); // Conversation peer’s account

// Send the message
conversation.sendMessage(msg, new TIMValueCallBack<TIMMessage>() {// Callback for sending a message
    @Override
    public void onError(int code, String desc) {// Failed to send the message
        // "code" (error code) and "desc" (error description) can be used to locate the cause of the request failure
        // For a list of error codes, see the Error Code Table
        Log.e(tag, "send message failed. code: " + code + " errmsg: " + desc);
    }

    @Override
    public void onSuccess(TIMMessage msg) {//Message sent successfully
        Log.d(tag, "SendMsg ok! peer:" + peer );
    }
});
```



