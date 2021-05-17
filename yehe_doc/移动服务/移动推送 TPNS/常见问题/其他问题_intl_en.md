### How do I migrate a TPNS application under Tencent Cloud account A to account B?
To migrate an application, the root account owner should apply for account migration as follows using the **corporate email address** or **registered email address** of account A.

- Subject: Tencent Cloud Account Migration for a TPNS Application
- To: tpns_team@tencent.com
- Email content:
>1. Source Tencent Cloud account ID:
2. AccessID and name of the application to be migrated:
3. Target Tencent Cloud account ID:
4. Company name:
5. Contact information (mobile):


### How do I use the `AccessID`, `AccessKey`, and `SecretKey` of a TPNS application?
- AccessID: unique identifier of the TPNS application. Use cases: 1. SDK integration; 2. Authentication signature generation during RESTful API call.
- AccessKey: client authentication key of the TPNS application. Use cases: SDK integration.
- SecretKey: server authentication key of the TPNS application. Use cases: authentication signature generation during RESTful API call.



### Is there a limit on the number of messages displayed in the notification bar?
There is no limit on the number of notification bar messages that a phone can receive and display. The reasons for not displaying messages may include:
- The notification bar on a Mi phone displays the latest message by default. If you want multiple messages to be displayed, you need to set a unique `n_id` for different messages.
- The message broadcast is blocked by a phone manager application.
- A Meizu phone has a message box, and uncommon messages will go directly to it. Please view the messages there.


### How do I set a custom ringtone?

1. In the console: choose **Push Notification** > **Advanced Settings** > **Reminder Mode** > **Sound** > **Customize** (for Android, select the ringtone file in the `raw` directory, which does not need the extension, for example, `xg_ring`. For iOS, select the ringtone file in the `bundle` directory, which requires the extension, for example, `xg_ring.wav)`.
2. In RESTful API v3: for Android, set `ring=1` in the push message body, and set `ring_raw` to the name of the specified ringtone file without the extension in the `raw` directory of the Android project. For iOS, set the sound in the push message body to the name of the specified ringtone file with the extension in the `bundle` directory of the project.

>!If the client has integrated with a vendor channel, due to the limitations of Huawei and Meizu, a custom ringtone file is not allowed on their phones, and the system sound will be used by default. Currently, a custom ringtone can be used on Mi phones.


### Why can't callback information be received for device registration?
- A vendor channel's callbacks are returned by the vendor server.
- Check whether broadcast is blocked by any security application.

### Why can't I find the records of pushes created through API?
Log in to the [TPNS console](https://console.cloud.tencent.com/tpns) and select **Created via API** on the **Push Management** > **Task List** page to view the records of pushes created through API.
![](https://main.qcloudimg.com/raw/0319075f0a90f18592e33b0da9698e9c.png)


### If an account changes its bound device, what will happen when a message is sent to this account?
The currently bound device (B) can receive the push, but the original bound device (A) cannot, as only the last device bound to the account can receive pushes.


### What is the order in which multiple push messages are received after a user goes back online?
The messages are in ascending order by message ID. The client will also receive messages in this rule; therefore, the order in which the messages are received is the same as that in which they are sent.

### If a past time is selected for a scheduled push, will the push be sent?
Yes. If a past time is selected, the system will send the push immediately.




