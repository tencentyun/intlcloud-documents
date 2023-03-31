## Feature Description
Both local messages and cloud messages can be deleted.
When cloud messages are deleted, such messages will be deleted both locally and from the cloud and **cannot be recovered**.

If the last message is deleted, the `lastMessage` in the conversation will become the last but one message.



### Deleting a local message

Call `MsgDelete` ([Details](https://comm.qq.com/im/doc/unity/en/api/MessageApi/MsgDelete.html)) to delete a local message.

> ?
> 1. After a historical local message is deleted, the message will be marked as deleted locally by the SDK and can no longer be pulled through `MsgGetMsgList`.
> 2. If the application is uninstalled and reinstalled, the deletion marker will be lost locally, and the message can still be pulled through `MsgGetMsgList`.

Sample code:


```c#
public static void MsgDelete()
    {
      string conv_id = "287646";

      MsgDeleteParam message_delete_param = new MsgDeleteParam();
      message_delete_param.msg_delete_param_msg = new Message(); // The message to be deleted
      message_delete_param.msg_delete_param_is_remble = false; // Delete the local message
      TIMResult res = TencentIMSDK.MsgDelete(conv_id, TIMConvType.kTIMConv_C2C, message_delete_param, (int code, string desc, string user_data) => {
        // Process the callback logic
      });
  }
```



### Deleting a message from the cloud

Call `MsgDelete` ([Details](https://comm.qq.com/im/doc/unity/en/api/MessageApi/MsgDelete.html)) to delete messages from the cloud.

This API deletes messages both locally and from the cloud, which cannot be recovered.

> ?
> 1. Up to 30 messages can be deleted per call.
> 2. Messages to be deleted per call **must** be from the same conversation.
> 3. This API can be called only once per second.
> 4. If messages have been pulled on a device by an account, they will remain on the device after the API is called to delete them from the cloud; in other words, deleted messages are not synced.

Sample code:


```c#
public static void MsgDelete()
    {
      string conv_id = "287646";

      MsgDeleteParam message_delete_param = new MsgDeleteParam();
      message_delete_param.msg_delete_param_msg = new Message(); // The message to be deleted
      message_delete_param.msg_delete_param_is_remble = true; // Delete the roaming message
      TIMResult res = TencentIMSDK.MsgDelete(conv_id, TIMConvType.kTIMConv_C2C, message_delete_param, (int code, string desc, string user_data) => {
        // Process the callback logic
      });
  }
```
