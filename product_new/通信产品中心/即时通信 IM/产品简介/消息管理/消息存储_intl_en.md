## Offline Message Storage

Instant Messaging (IM) supports offline message caching. This means offline messages are pulled when users log in the next time. Offline messages are retained for 7 days by default. If users log in after 7 days, they will not receive offline messages from more than 7 days ago. There is a capacity limit to each user’s offline message cache. Once exceeding the limit, messages will be deleted one by one in chronological order (earliest messages are deleted first). Messages that have been deleted are not counted as unread messages, but stored in roaming messages. Every user has a maximum cache capacity of 30 KB. The maximum number of offline messages depends on the size of each message, which is determined by the message type and length of text.

By default, after a user device pulls offline messages through the SDK, the IM server deletes these offline messages. If supporting multiple devices is required, or you want to pull unread offline messages after switching to a different device, you need to manage these offline messages yourself. After the automatic read reporting feature of the SDK is disabled, the IM server deletes these offline messages only when you explicitly call the read reporting API. Otherwise, these offline messages will be automatically deleted after expiration. If you do not explicitly call the read reporting API, unread offline messages still can be pulled after you switch to another device.

## Roaming Message Storage

IM supports message roaming, which means that, when users log in on different devices, they still have access to chat history with other users or groups.
By default, roaming one-to-one messages and group messages are stored for 7 days. Messages older than 7 days will be deleted. You can change the number of roaming days in the console. Increasing roaming days is an value-added service.
<span id="MsgType"></span>
Different SDK versions allow you to extend the storage time of historical messages for different message types, as shown in the following table.

| SDK Version | Text | Custom Message | Image | File | Short Audio | Short Video | Rich Media Message |
|---------|---------|---------|---------|---------|---------|---------|---------|
| Android 4.X | &#10003; | &#10003;  | &#10003;| &#10003; | &#10003; | &#10003; | &#10003; |
| Android 3.X | &#10003; | &#10003;  | × | × | × | × | × |
| Android 2.X | &#10003; |  &#10003; | × | × | × | × | × |
| iOS 4.X | &#10003; |  &#10003; | × | × | × | × | × |
| iOS 3.X | &#10003; |  &#10003; | × | × | × | × | × |
| iOS 2.X | &#10003; |  &#10003; | × | × | × | × | × |
| PC SDK 2.X | &#10003; |  &#10003; | × | × | × | × | × |
| Web and mini program SDK 2.X | &#10003; | &#10003;  | &#10003;| &#10003; | &#10003; | &#10003; | &#10003; |
| Web and mini program SDK 1.X | &#10003; |  &#10003; | × | × | × | × | × |

>We recommend you upgrade to the latest SDK version for improved user experience.

## Recent Contacts

Your recent contact information displays users who have talked to you recently and their last messages.

By default, the client pulls the recent contact information through the SDK upon login. If this information has not been stored locally, the client obtains it by performing the onNewMessage callback.

If the recent contacts feature is used, some traffic will be consumed upon login when the client pulls the last messages of recent contacts from the server. The recent contacts feature can be disabled through the SDK if it is not needed. The recent contacts list stores your 100 most recent contacts, but the storage duration of a contact is dependent on when the last message was sent. For example, if a contact has not talked to you in 7 days, when the last message expires, this contact will not appear in the recent contacts list.

## App Local Storage

Users do not need to store messages because the SDK stores the messages it receives by default. Users can call the API to obtain local messages (no networking required). Additionally, local messages can be obtained through the getMessage API. When gaps exist in local message history, roaming messages are used to fill in the gaps.
By default, the SDK does not delete user messages, but you are provided with the option to delete local messages.
>As local storage consumes disk space and affects CPU performance, you can disable local storage when it is not required. For example, in a live broadcasting scenario, message processing performance is emphasized, whereas historical messages are not a concern.





