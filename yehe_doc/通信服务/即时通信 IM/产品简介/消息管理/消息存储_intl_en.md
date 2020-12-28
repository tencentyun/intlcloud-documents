## Offline Message Storage

Instant Messaging (IM) supports offline message caching. This means offline messages can be pulled when users log in the next time. Offline messages are retained for 7 days by default. If users do not log within 7 days, they cannot receive offline messages from 7 or more days ago. For one-to-one messages, the offline message cache of each user can store up to 100 one-to-one conversations and 100 unread messages per one-to-one conversation. Unread messages beyond these limits are excluded from the unread count. but these messages are still stored in the roaming server. These limits are not imposed on group messages.

By default, after a user device pulls offline messages through the SDK, the IM server deletes these offline messages. If support for multiple devices is required, or you want to pull unread offline messages after switching to a different device, you need to manage these offline messages by yourself. After the automatic read reporting feature of the SDK is disabled, the IM server deletes these offline messages only when you explicitly call the read reporting API. Otherwise, these offline messages will be automatically deleted after expiration. If you do not explicitly call the read reporting API, unread offline messages still can be pulled after you switch to another device.

## Roaming Message Storage

IM supports message roaming. That is, when users log in on different devices, they still have access to chat history with other users or groups.
By default, one-to-one messages and group messages are stored in the roaming server for 7 days. Messages beyond the time limit of 7 days are deleted. You can change the roaming duration of messages in the console. To increase the roaming duration, you need to purchase a value-added service. For more information on billing, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).
[](id:MsgType)
Different SDK versions allow you to extend the storage time of historical messages for different message types, as shown in the following table.

| SDK Version | Text | Custom Message | Image | File | Short Audio | Short Video | Rich Media Message | 
|---------|---------|---------|---------|---------|---------|---------|---------|
| Android 4.X | &#10003; | &#10003;  | &#10003;| &#10003; | &#10003; | &#10003; | &#10003; |
| Android 3.X | &#10003; | &#10003;  | × | × | × | × | × |
| Android 2.X | &#10003; |  &#10003; | × | × | × | × | × |
| iOS 4.X | &#10003; | &#10003;  | &#10003;| &#10003; | &#10003; | &#10003; | &#10003; |
| iOS 3.X | &#10003; |  &#10003; | × | × | × | × | × |
| iOS 2.X | &#10003; |  &#10003; | × | × | × | × | × |
| PC SDK 2.X | &#10003; |  &#10003; | × | × | × | × | × |
| Web and mini program SDK 2.X | &#10003; | &#10003;  | &#10003;| &#10003; | &#10003; | &#10003; | &#10003; |
| Web and mini program SDK 1.X | &#10003; |  &#10003; | × | × | × | × | × |

>? We recommend you upgrade to the latest SDK version for an improved user experience.

## Recent Contacts

Information on recent contacts is similar to the recent contact list in QQ, which displays the users who recently contact you and their last messages.

By default, the client pulls the recent contact information through the SDK upon login. If such information has not been stored locally, the client obtains it through the onNewMessage callback.

If the recent contacts feature is used, some traffic will be consumed upon login when the client pulls the last messages of recent contacts from the server. The recent contacts feature can be disabled through the SDK if it is not needed. The recent contacts list stores your 100 most recent contacts, but the storage duration of a contact is dependent on when the last message was sent. For example, if a contact has not talked to you in 7 days, when the last message expires, this contact will not appear in the recent contacts list.

## App Local Storage

Users do not need to store messages because the SDK stores the messages it receives by default. Users can call the API to obtain local messages (no networking required). Additionally, local messages can be obtained through the getMessage API. When gaps exist in local message history, roaming messages are used to fill in the gaps.
By default, the SDK does not delete user messages, but you are provided with the option to delete local messages.
>! As local storage consumes disk space and affects CPU performance, you can disable local storage when it is not required. For example, in a live broadcasting scenario, message processing performance is emphasized, whereas historical messages are not a concern.





