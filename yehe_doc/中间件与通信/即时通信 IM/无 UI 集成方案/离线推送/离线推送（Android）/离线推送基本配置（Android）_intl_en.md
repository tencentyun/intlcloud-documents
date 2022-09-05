## Overview

IM terminal users need to obtain latest messages at all times. However, due to the limited performance and battery power of mobile devices, when the app is running in the background, IM recommends that you use the system-grade push channels provided by vendors for message notifications to avoid excessive resource consumption caused by maintaining persistent connections. Compared with third-party push, system-grade push channels provide more stable system-grade persistent connections, enabling users to receive push messages at any time and thus greatly reducing resource consumption.

Currently, IM supports APNs, MI push, Huawei push, Meizu push, vivo push, OPPO push, and the push services of other vendors. The details are as follows:

<table> 
   <tr> 
     <th nowrap="nowrap">Push Channel</th> 
     <th nowrap="nowrap">System Requirements</th> 
     <th>Conditions</th> 
   </tr> 
   <tr> 
     <td><a href="https://intl.cloud.tencent.com/document/product/1047/34336" target="_blank">APNs</a></td> 
     <td>iOS</td> 
     <td>iOS system push channel, which is also the only iOS push channel</td> 
   </tr> 
   <tr> 
     <td><a href="https://intl.cloud.tencent.com/document/product/1047/34339" target="_blank">MI push</a></td> 
     <td>MIUI</td> 
     <td>Use MI push MiPush_SDK_Client_3_6_12.jar</td> 
   </tr> 
   <tr> 
     <td><a href="https://intl.cloud.tencent.com/document/product/1047/34340" target="_blank">Huawei push</a></td> 
     <td>EMUI</td> 
     <td>Huawei mobile service versions later than 20401300 and SDK version of push:2.6.3.301</td> 
   </tr> 
   <tr> 
     <td nowrap="nowrap"><a href="https://intl.cloud.tencent.com/document/product/1047/34341" target="_blank">Google FCM push</a></td> 
     <td nowrap="nowrap">Android 4.1 and later versions</td> 
     <td>The mobile phone needs to install Google Play Services and be used outside Mainland China.</td> 
   </tr> 
   <tr> 
     <td><a href="https://intl.cloud.tencent.com/document/product/1047/34342" target="_blank">Meizu push</a></td> 
     <td>Flyme</td> 
     <td>Use Meizu push push-internal:3.6.+</td> 
   </tr> 
   <tr> 
     <td nowrap="nowrap"><a href="https://intl.cloud.tencent.com/document/product/1047/34344" target="_blank">OPPO push</a></td> 
     <td>ColorOS</td> 
     <td>Not all OPPO models and versions support OPPO push. At present, the OPPO push service is available only to A/B-level apps that are already in OPPO’s app store. Therefore, the current demo has no sample of OPPO push.</td> 
   </tr>  
   <tr> 
     <td nowrap="nowrap"><a href="https://intl.cloud.tencent.com/document/product/1047/34343" target="_blank">vivo push</a></td> 
     <td nowrap="nowrap">FuntouchOS</td> 
     <td>Not all vivo models and versions support vivo push. The required SDK version is vivo_pushsdk_v2.3.1.jar.</td> 
   </tr> 
</table>


Here, "offline" means that the app is closed by the system or user without logout. In this case, if you want to receive IM SDK message reminders, you can integrate IM offline push.

>
> - Users who have logged out normally or have been forced logout will not receive any message notifications.
> - Currently, offline push only provides notifications for [ordinary chat messages](https://intl.cloud.tencent.com/document/product/1047/34320) and does not provide notifications for [system messages](https://intl.cloud.tencent.com/document/product/1047/34320).

## Basic Configuration of IM SDK Offline Push
### Configuring global offline push settings
The IM SDK supports configuring global offline push settings, allowing users to set whether to enable offline push and the notification sound when receiving offline push messages. The setting method is `setOfflinePushSettings` provided by `TIMManager`.

>
> - Calls to this method take effect only after successful login.
> - Currently, only APNs custom notification sounds are supported, and audio files must be built-in audio files in the app.

**Prototype:**

```java
/**
 * Initializes offline push configuration. The settings take effect only after login.
 * @param settings Offline push configuration information
 */
public void setOfflinePushSettings(TIMOfflinePushSettings settings)

/**
 * Obtains the offline push configuration from the server. It can be obtained only after login.
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
 * Obtain whether the feature is enabled
 * @return true: enabled. false: disabled.
 */
public boolean isEnabled()

/**
 * Set whether to enable offline push
 * @param enabled Whether to enable offline push
 */
public void setEnabled(boolean enabled)

/**
 * Obtain the notification sound for receiving offline push for C2C messages
 * @return URI of the audio file. If it is not specified, ‘null’ is returned.
 */
public Uri getC2cMsgRemindSound()

/**
 * Set the notification sound for receiving offline push for C2C messages
 * @param c2cMsgRemindSound URI of the audio file. To use the default sound, enter ‘null’.
 */
public void setC2cMsgRemindSound(Uri c2cMsgRemindSound)

/**
 * Obtain the notification sound for receiving offline push for group messages
 * @return URI of the audio file. If it is not specified, ‘null’ is returned.
 */
public Uri getGroupMsgRemindSound()

/**
 * Set the notification sound for receiving offline push for group messages
 * @param groupMsgRemindSound URI of the audio file. To use the default sound, enter ‘null’.
 */
public void setGroupMsgRemindSound(Uri groupMsgRemindSound)
```

**Example:**

```java
TIMOfflinePushSettings settings = new TIMOfflinePushSettings();
//Enable offline push
settings.setEnabled(true);
//Set the notification sound for receiving offline C2C messages. In this example, the audio file is stored in the res/raw folder.
settings.setC2cMsgRemindSound(Uri.parse("android.resource://" + getPackageName() + "/" + R.raw.dudulu));
//Set the notification sound for receiving offline group messages. In this example, the audio file is stored in the res/raw folder.
settings.setGroupMsgRemindSound(Uri.parse("android.resource://" + getPackageName() + "/" + R.raw.dudulu));

TIMManager.getInstance().setOfflinePushSettings(settings);
```

### Setting offline push for a single message
'The IM SDK supports configuring offline push settings for each message. For any specified message, developers can set whether to enable offline push, the notification sound when receiving offline push messages, offline push message description, and extension fields.

>
> - The offline push configuration for a single message has the highest priority. That is, if a global offline push configuration and single-message offline push configuration are both set, the latter will prevail.
> - Currently, only APNs custom notification sounds are supported, and audio files must be built-in audio files in the app.


**Prototype:**

```java
/**
 * Set the configuration for the time when the target user receives an offline push notification for the current message (this is optional and set when sending the message)
 * @param settings Offline push configuration
 */
public void setOfflinePushSettings(TIMMessageOfflinePushSettings settings)

/**
 * Obtain offline push configuration for the current message
 * @return The offline push configuration. If the sender has not specified it, ‘null’ is returned.
 */
public TIMMessageOfflinePushSettings getOfflinePushSettings()
```

**`TIMMessageOfflinePushSettings`：**

```java
/**
 * Set the content to be displayed when the target user receives the offline push notification for the current message (this is optional and set when sending the message)
 * @param descr Text content
 */
public void setDescr(String descr)

/**
 * Obtain the offline push display content of the current message
 * @return Text content
 */
public String getDescr()

/**
 * Set the extension field of the current message (this is optional and set when sending the message)
 * @param ext Content of the extension field
 */
public void setExt(byte[] ext)

/**
 * Obtain the extension field of the current message
 * @return Content of the extension field. If it is not specified, ‘null’ is returned.
 */
public byte[] getExt()

/**
 * Set whether the current message allows offline push. By default, it is allowed (this is optional and set when sending the message)
 * @param enabled true: allow offline push. false: disallow offline push.
 */
public void setEnabled(boolean enabled)

/**
 * Obtain whether the current message allows push
 * @return Whether the message allows push. true: allow. false: disallow.
 */
public boolean isEnabled()

/**
 * Obtain the offline push configuration for the current message on Android devices
 * @return Offline push configuration on Android devices
 */
public AndroidSettings getAndroidSettings()

/**
 * Set the offline push configuration for the current message on Android devices (this is optional and set when sending the message)
 * @param androidSettings Offline push configuration for the current message on Android devices
 */
public void setAndroidSettings(AndroidSettings androidSettings)

/**
 * Obtain the offline push configuration for the current message on iOS devices
 * @return Offline push configuration on iOS devices
 */
public IOSSettings getIosSettings()

/**
 * Set the offline push configuration for the current message on iOS devices (this is optional and set when sending the message)
 * @param iosSettings Offline push configuration for the current message on iOS devices
 */
public void setIosSettings(IOSSettings iosSettings)

```

**TIMMessageOfflinePushSettings.AndroidSettings：**

```java
/**
 * Obtain the notification title
 * @return Notification title
 */
public String getTitle()

/**
 * Set the notification title (this is optional and set when sending the message)
 * @param title Notification title
 */
public void setTitle(String title)

/**
 * Obtain the offline push notification sound URI of the current message on Android devices
 * @return Sound URI. If it is not specified, ‘null’ is returned.
 */
public Uri getSound()

/**
 * Set the offline push notification sound for the current message on Android devices (this is optional and set when sending the message)
 * @param sound Sound URI, which supports only built-in audio files in the app
 */
public void setSound(Uri sound)

/**
 * Obtain the notification mode of the current message
 * @return Notification mode
 */
public NotifyMode getNotifyMode()

/**
 * Set the notification mode for the time when the target user receives the offline push notification for the current message (this is optional and set when sending the message)
 * NotifyMode This is set only for third-party offline push, such as offline push by MI and Huawei.
 * @param mode Notification mode. The default notification mode is the notification bar message mode.
 */
public void setNotifyMode(NotifyMode mode)
```

**TIMMessageOfflinePushSettings.NotifyMode:**
```java
/**
 * Notification bar message mode. When an offline message is delivered, click the notification bar message to directly start the app. This will not trigger callback for the app.
 */
NotifyMode.Normal

```

**TIMMessageOfflinePushSettings.IOSSettings:**

```java
/**
 * Obtain the offline push notification sound for the current message on iOS devices
 * @return Audio file path. If it is not specified, ‘null’ is returned.
 */
public String getSound()

/**
 * Set the offline push notification sound for the current message on iOS devices (this is optional and set when sending the message)
 * @param sound Audio file path. When it is set to {@see IOSSettings#NO_SOUND_NO_VIBRATION}, it means there is no notification sound nor vibration.
 */
public void setSound(String sound)

/**
 * Obtain whether Badge counting is enabled for the current message
 * @return true Badge counting is enabled for the current message.
 */
public boolean isBadgeEnabled()

/**
 * Set whether Badge counting is enabled for the current message. By default, it is enabled (this is optional and set when sending the message.)
 * @param badgeEnabled Whether Badge counting is enabled
 */
public void setBadgeEnabled(boolean badgeEnabled)
```

**Example:**

```java
//Construct a message
TIMMessage msg = new TIMMessage();

//Add text content
TIMTextElem elem = new TIMTextElem();
elem.setText("a new msg from " + selfId);
if(msg.addElement(elem) != 0) {
    Log.d(tag, "addElement failed");
    return;
}

//Set offline push configuration for the current message
TIMMessageOfflinePushSettings settings = new TIMMessageOfflinePushSettings();
settings.setEnabled(true);
settings.setDescr("I'm description");
//Set offline push extension information
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

//Set offline configuration for receiving messages on Android devices
TIMMessageOfflinePushSettings.AndroidSettings androidSettings = new TIMMessageOfflinePushSettings.AndroidSettings();
//Construction mode for versions earlier than IM SDK 2.5.3
//TIMMessageOfflinePushSettings.AndroidSettings androidSettings = settings.new AndroidSettings();
androidSettings.setTitle("I'm title");
//Push custom notification bar message. After the recipient receives a message and clicks the notification bar message, it triggers an app callback (for offline push by MI and Huawei).
androidSettings.setNotifyMode(TIMMessageOfflinePushSettings.NotifyMode.Normal);
//Set the notification sound for receiving messages on Android devices. The audio file must be in the raw folder.
androidSettings.setSound(Uri.parse("android.resource://" + getPackageName() + "/" +R.raw.hualala));
settings.setAndroidSettings(androidSettings);

//Set offline configuration for receiving messages on iOS devices
TIMMessageOfflinePushSettings.IOSSettings iosSettings = new TIMMessageOfflinePushSettings.IOSSettings();
//Construction mode for versions earlier than IM SDK 2.5.3
//TIMMessageOfflinePushSettings.IOSSettings iosSettings = settings.new IOSSettings();

//Enable Badge counting
iosSettings.setBadgeEnabled(true);  
//Set no notification sound nor vibration upon receiving messages on iOS devices (a new feature in IM SDK 2.5.3)
//iosSettings.setSound(TIMMessageOfflinePushSettings.IOSSettings.NO_SOUND_NO_VIBRATION);
//Set the notification sound for receiving offline messages on iOS devices
iosSettings.setSound("/path/to/sound/file");

msg.setOfflinePushSettings(settings);

//Obtain a one-to-one conversation
TIMConversation conversation = TIMManager.getInstance().getConversation(
        TIMConversationType.C2C,    //Conversation type: one-to-one chat
        peer); //Conversation peer’s account

//Send a message
conversation.sendMessage(msg, new TIMValueCallBack<TIMMessage>() {//Send the message callback.
    @Override
    public void onError(int code, String desc) {//Failed to send the message.
        //"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure.
        //For the list of error codes, see the error code table.
        Log.e(tag, "send message failed. code: " + code + " errmsg: " + desc);
    }

    @Override
    public void onSuccess(TIMMessage msg) {//Sent the message successfully.
        Log.d(tag, "SendMsg ok! peer:" + peer );
    }
});
```



