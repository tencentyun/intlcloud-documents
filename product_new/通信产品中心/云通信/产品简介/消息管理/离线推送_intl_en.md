## Use Cases
Use offline push notifications to notify users upon the arrival of new messages even when the app is working in the background or the process has been killed. iOS devices use APNs for offline messages, while Android users need to register for offline message callbacks.

## iOS APNs Push Notifications
### Push notification formats

![](https://main.qcloudimg.com/raw/1563432f165349e680c7e3ebb05b546d.png)


The preceding figure shows the examples of a one-to-one chat message and group chat message.
For more information on iOS APNs push notification formats, see [Push Notification Formats](https://cloud.tencent.com/document/product/269/9154#.E9.80.9A.E7.94.A8.E6.8E.A8.E9.80.81.E8.A7.84.E5.88.99).

### Basic APIs
To support APNs, the following APIs must be called. For more information, see [iOS APNs Event Reporting](https://cloud.tencent.com/document/product/269/9154#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.AE.9E.E7.8E.B0-apns-.E6.8E.A8.E9.80.81):
- Set the token.
- Switch to the background and report unread messages.
- Switch to the foreground and push notifications.

### Setting the Ext extension field
Depending on the situation, the app may need to set the `Ext` extended field to allow users to take actions such as clicking to be redirected. In this case, fill in the `Ext` field in TIMCustomElem, and the IM backend will pass the value of the field into `Ext` when pushing notifications. For information on customizing extended fields, see [Offline Push Notification Properties](https://cloud.tencent.com/document/product/269/9154#.E6.AF.8F.E6.9D.A1.E7.A6.BB.E7.BA.BF.E6.8E.A8.E9.80.81.E5.B1.9E.E6.80.A7).

### Setting push sounds
Depending on the situation, the app may need to play a specific sound when pushing notifications for a certain type of messages. In this case, fill in the `sound` field in TIMCustomElem, and the IM backend will pass the value of the field into `Ext` when pushing notifications. For more information, see [Setting Custom Push Sounds](https://cloud.tencent.com/document/product/269/9154#.E8.AE.BE.E7.BD.AE.E8.87.AA.E5.B7.B1.E7.9A.84.E6.8E.A8.E9.80.81.E5.A3.B0.E9.9F.B3).

## Android Offline Push
Android 1.8.0 and later support separating services from processes. When the app process is killed, the service survives and can continue to receive offline push notifications. For more information on the settings and configuration, see [Android Offline Push](https://cloud.tencent.com/document/product/269/9234).

## Sending Messages from the Backend
When sending messages from the backend, refer to the [push format](https://cloud.tencent.com/document/product/269/9154#.E9.80.9A.E7.94.A8.E6.8E.A8.E9.80.81.E8.A7.84.E5.88.99) to set the display of APNs push notifications for iOS devices. For Android devices, see [Offline Push OfflinePushInfo](https://cloud.tencent.com/document/product/269/2720#.E7.A6.BB.E7.BA.BF.E6.8E.A8.E9.80.81-offlinepushinfo-.E8.AF.B4.E6.98.8E).
