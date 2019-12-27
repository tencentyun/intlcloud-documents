## Use Cases
Use offline push notifications to notify users upon the arrival of new messages even when the app is working in the background or the process has been killed. iOS devices use APNs for offline messages, while Android users need to register for offline message callbacks.

## iOS APNs Push Notifications
### Push notification formats

![](https://main.qcloudimg.com/raw/8bb11ef0a0ff210c1b0a1ab65da63c2f.png)


The preceding figure shows the examples of a one-to-one chat message and group chat message.

### Basic APIs
To support APNs, the following APIs must be called:
- Set the token.
- Switch to the background and report unread messages.
- Switch to the foreground and push notifications.

### Setting the Ext extension field
Depending on the situation, the app may need to set the `Ext` extended field to allow users to take actions such as clicking to be redirected. In this case, fill in the `Ext` field in TIMCustomElem, and the IM backend will pass the value of the field into `Ext` when pushing notifications.

### Setting push sounds
Depending on the situation, the app may need to play a specific sound when pushing notifications for a certain type of messages. In this case, fill in the `sound` field in TIMCustomElem, and the IM backend will pass the value of the field into `Ext` when pushing notifications.
## Android Offline Push
Android 1.8.0 and later support separating services from processes. When the app process is killed, the service survives and can continue to receive offline push notifications.

## Sending Messages from the Backend
When sending messages from the backend, refer to the push format to set the display of APNs push notifications for iOS devices. For Android devices, see [Offline Push OfflinePushInfo](https://intl.cloud.tencent.com/document/product/1047/33527).
