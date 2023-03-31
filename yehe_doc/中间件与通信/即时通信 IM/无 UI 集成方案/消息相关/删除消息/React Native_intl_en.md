## Feature Description

Both local messages and cloud messages can be deleted.
When cloud messages are deleted, such messages will be deleted both locally and from the cloud and **cannot be recovered**.

If the last message is deleted, the `lastMessage` in the conversation will become the last but one message.

### Deleting a local message

Call `deleteMessageFromLocalStorage` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMMessageManager/deleteMessageFromLocalStorage.html)) to delete a local message.

> ?
>
> 1. This API can only be used to delete a local historical message. After deleted, the message will be marked as deleted locally by the SDK and can no longer be pulled through `getHistoryMessage`.
> 2. If the application is uninstalled and reinstalled, the delete marker will be lost locally, and the message can still be pulled through `getHistoryMessage`.

Below is the sample code:

```javascript
TencentImSDKPlugin.v2TIMManager
  .getMessageManager()
  .deleteMessageFromLocalStorage("");
```

### Deleting a message from the cloud

Call `deleteMessages` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMMessageManager/deleteMessages.html)) to delete messages from the cloud.

This API deletes messages both locally and from the cloud, which cannot be recovered.

> ?
>
> 1. Up to 30 messages can be deleted per call.
> 2. Messages to be deleted per call **must** be from the same conversation.
> 3. This API can be called only once every second.
> 4. If messages have been pulled on a device by an account, they will remain on the device after the API is called to delete them from the cloud; in other words, deleted messages are not synced.

Below is the sample code:

```javascript
TencentImSDKPlugin.v2TIMManager
  .getMessageManager()
  .deleteMessages(["messageid"]);
```
