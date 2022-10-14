### Since the push API of Tencent Push Notification Service no longer supports TLS 1.0, how can I know if my service is affected?
You have no need to update the client SDK, and you just need to check the TLS version in the push API callback side.
 - For the push with RESTful APIs, check the TLS version specified in the push code.
 - For the push with the server SDK provided by Tencent Push Notification Service, check whether the current request-related libraries support TLS 1.1 or later, including whether Java JDK is v1.8 or later and OpenSSL supports TLS 1.1 or later.


### How do I migrate a Tencent Push Notification Service application under Tencent Cloud account A to account B?
To migrate an application, the root account owner should apply for account migration as follows using the **corporate email address** or **registered email address** of account A.

- Subject: Migration of Tencent Push Notification Service Applications under Tencent Cloud Account
- To: tpns_team@tencent.com
- Email content:

```
1. Source Tencent Cloud account ID:
2. AccessID and name of the application to be migrated:
3. Target Tencent Cloud account ID:
4. Company name:
5. Contact (mobile):
```


### How do I use the `AccessID`, `AccessKey`, and `SecretKey` of a Tencent Push Notification Service application?
- AccessID: The unique identifier of the application, which is used in SDK integration and in authentication signature generation during RESTful API call.
- AccessKey: The client authentication key of the application, which is used in SDK integration.
- SecretKey: The server authentication key of the application, which is used in authentication signature generation during RESTful API call.



### Is there a limit on the number of messages displayed in the notification bar?
There is no limit on the number of notification bar messages that a phone can receive and display. The reasons for not displaying messages may include:
- The notification bar on a Mi phone displays the latest message by default. If you want multiple messages to be displayed, you need to set a unique `n_id` for different messages.
- The message broadcast is blocked by a phone manager application.
- A Meizu phone has a message box, and uncommon messages will go directly to it. Please view the messages there.


### Why can't callback information be received for device registration?
- A vendor channel's callbacks are returned by the vendor server.
- Check whether broadcast is blocked by any security application.

### Why can't I find the records of pushes created through API?
Log in to the [Tencent Push Notification Service console](https://console.cloud.tencent.com/tpns) and select **Created via API** on the **Push Management** > **Task List** page to view the records of pushes created through API.
![](https://main.qcloudimg.com/raw/0319075f0a90f18592e33b0da9698e9c.png)


### If an account changes its bound device, what will happen when a message is sent to this account?
The currently bound device (B) can receive the push, but the originally bound device (A) cannot, because only the last device bound to the account can receive pushes.


### What is the order in which multiple push messages are received after a user goes back online?
The messages are in ascending order by message ID. The client will also receive messages in this rule; therefore, the order in which the messages are received is the same as that in which they are sent.

### If a past time is selected for a scheduled push, will the push be sent?
Yes. If a past time is selected, the system will send the push immediately.

### Why does the troubleshooting tool show that the notification bar is disabled even though I have granted the notification bar permission?
The notification bar status is not synced. Open the app again to sync the notification bar status to the backend.

