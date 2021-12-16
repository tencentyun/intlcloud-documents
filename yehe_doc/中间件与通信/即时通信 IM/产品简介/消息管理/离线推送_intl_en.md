## Application Scenarios
You can use the offline push feature to notify users upon the arrival of new messages even when the app is running in the background or the process has been killed. iOS devices use APNs for offline push, while Android users need to register for offline message callbacks.

## iOS APNs Push Notifications
### Push notification formats

![](https://main.qcloudimg.com/raw/8bb11ef0a0ff210c1b0a1ab65da63c2f.png)


The preceding figure shows the examples of a one-to-one chat message and group chat message.
For more information about iOS APNs push formats, see [Push Formats](https://intl.cloud.tencent.com/document/product/1047/34347).

### Basic APIs
The following APIs must be called to support APNs. For more information, see [iOS APNs Event Reporting](https://intl.cloud.tencent.com/document/product/1047/34347):
- Set the token.
- Switch to the background and report unread messages.
- Switch to the foreground and push notifications.

### Setting the Ext extension field
In some cases, an app needs to set the Ext extension field for push based on specific circumstances to facilitate user operations such as redirect clicks. You can input it into the Ext field in TIMCustomElem, and during push, the IM backend will input the field into Ext. Please refer to [Customizing Offline Message Attributes](https://intl.cloud.tencent.com/document/product/1047/34347) to customize the extension field.

### Setting push sounds
In some cases, an app needs to set the push sound of a single message to alert the user. You can input the sound into the sound field in TIMCustomElem, and during push, the IM backend will input the field into Ext. Please refer to [Setting Custom Push Alert Sounds](https://intl.cloud.tencent.com/document/product/1047/34347).

## Android Offline Push
Android 1.8.0 and later versions support separating services from processes. When the app process is killed, the service survives and can continue to receive offline push notifications. For more information about the relevant settings and configuration, see [Android Offline Push](https://intl.cloud.tencent.com/document/product/1047/34336).

## Sending Messages from the Backend
For iOS, you can refer to [Push Formats](https://intl.cloud.tencent.com/document/product/1047/34347) to set the display format of APNs push messages; for Android, you can refer to [Offline Push OfflinePushInfo](https://intl.cloud.tencent.com/document/product/1047/33527) to set the display format.

## References
- [Managing Offline Push Certificates](https://intl.cloud.tencent.com/document/product/1047/34540)
- [Applying for an Apple Push Certificate](https://intl.cloud.tencent.com/document/product/1047/34346)
