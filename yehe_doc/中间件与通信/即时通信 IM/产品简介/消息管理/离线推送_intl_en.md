## Application Scenarios
You can use the offline push feature to allow users to receive new messages even when the app is running in the background or the process has been killed. iOS devices use APNs for offline push, while Android devices need you to register for offline message callbacks.

## iOS APNs Push Notifications
### Push notification format

![](https://main.qcloudimg.com/raw/8bb11ef0a0ff210c1b0a1ab65da63c2f.png)


The figure shows the examples of a one-to-one chat message and group chat message.
For more information about iOS APNs push formats, see [Push Format](https://intl.cloud.tencent.com/document/product/1047/34347).

### Basic APIs
The following APIs must be called to support APNs. For more information, see [iOS APNs Event Reporting](https://intl.cloud.tencent.com/document/product/1047/34347):
- Set the token.
- Switch to the background and report unread messages.
- Switch to the foreground and push notifications.

### Setting the Ext extension field
In some cases, an app needs to set the Ext extension field for offline push based on specific circumstances to facilitate user operations such as redirect clicks. You can input it into the Ext field in TIMCustomElem, and during push, the IM backend will input the field into Ext. For more information, see [Customizing Offline Message Attributes](https://intl.cloud.tencent.com/document/product/1047/34347) to customize the extension field.

### Setting push alert sounds
In some cases, an app needs to set the push alert sound of a single message to alert users. You can input the sound into the sound field in TIMCustomElem, and during push, the IM backend will input the field into Ext. For more information, see [Setting Custom Push Alert Sounds](https://intl.cloud.tencent.com/document/product/1047/34347).

## Android Offline Push
Android 1.8.0 and later versions support separating services from processes. When the app process is killed, the service survives and continues to receive offline notifications. For more information, see [Android Offline Push](https://intl.cloud.tencent.com/document/product/1047/34336).

## Sending Messages from the Backend
For iOS, you can refer to [Push Format](https://intl.cloud.tencent.com/document/product/1047/34347) to set the display format of APNs push messages; for Android, you can refer to [OfflinePushInfo](https://intl.cloud.tencent.com/document/product/1047/33527) to set the display format.

## References
- [Managing Offline Push Certificates](https://intl.cloud.tencent.com/document/product/1047/34540)
- [Applying for an Apple Push Certificate](https://intl.cloud.tencent.com/document/product/1047/34346)
