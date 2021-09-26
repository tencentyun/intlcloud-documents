## Roaming Message Storage

IM supports message roaming, which means that, when users log in on different devices, they still have access to chat history with other users or groups.
By default, one-to-one chat messages and group chat messages roam for 7 days, and they will be deleted then. IM allows you to change the message roaming period in the console. Extending the message roaming period is a value-added service. For the billing details, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).
[](id:MsgType)
Different SDK versions allow you to extend the storage time of historical messages for different message types, as shown in the following table.

| SDK Version | Text | Custom Message | Image | File | Short Audio | Short Video | Rich Media Message | 
|---------|---------|---------|---------|---------|---------|---------|---------|
| Android 5.X | &#10003; | &#10003;  | &#10003;| &#10003; | &#10003; | &#10003; | &#10003; |
| Android 4.X | &#10003; | &#10003;  | &#10003;| &#10003; | &#10003; | &#10003; | &#10003; |
| Android 3.X | &#10003; | &#10003;  | × | × | × | × | × |
| Android 2.X | &#10003; |  &#10003; | × | × | × | × | × |
| iOS 5.X | &#10003; | &#10003;  | &#10003;| &#10003; | &#10003; | &#10003; | &#10003; |
| iOS 4.X | &#10003; | &#10003;  | &#10003;| &#10003; | &#10003; | &#10003; | &#10003; |
| iOS 3.X | &#10003; |  &#10003; | × | × | × | × | × |
| iOS 2.X | &#10003; |  &#10003; | × | × | × | × | × |
| PC SDK 2.X | &#10003; |  &#10003; | × | × | × | × | × |
| Web and mini program SDK 2.X | &#10003; | &#10003;  | &#10003;| &#10003; | &#10003; | &#10003; | &#10003; |
| Web and mini program SDK 1.X | &#10003; |  &#10003; | × | × | × | × | × |

>?We recommend you upgrade to the latest SDK version for improved user experience.

## Unread Message Storage

IM supports the storage of unread messages; that is, messages sent to users when they are offline will be pulled upon next login.

For one-to-one chat, unread messages in up to 100 conversations are saved for each user for 7 days by default, with up to 100 unread messages in each conversation. Excessive messages will not be counted as unread messages, but they will still be saved in message roaming. For group chat, there are no such limits.

## Recent Contacts

Similar to the list of recent contacts on QQ, recent contacts display the users who have recently contacted the current user as well as their last messages.

By default, the client will pull the recent contacts through the SDK upon login to display the conversation list, and the recent 100 contacts are stored by default for the same period as the last messages; for example, if no messages have been sent to or received from a contact for 7 days, this contact cannot be obtained in the recent contacts after the last message expires.

## App Local Storage

Users do not need to store messages because the SDK stores the messages it receives by default. Users can call the API to obtain local messages (no networking required). Additionally, local messages can be obtained through the getMessage API. When gaps exist in local message history, roaming messages are used to fill in the gaps.
By default, the SDK does not delete user messages, but you are provided with the option to delete local messages.
>!As local storage consumes disk space and affects CPU performance, you can disable local storage when it is not required. For example, in a live broadcasting scenario, message processing performance is emphasized, whereas historical messages are not a concern.





