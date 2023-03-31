## Overview
Message extension allows you to configure keys and values for messages to implement polling, group notices, survey and other types of messages.
- For polling, create a custom message, where `custom_elem_data` stores the polling title and options. And store the user ID of the voter and selected option(s) in the `key` and `value` of the message extension, respectively. With the selected options of users, we can calculate the polling percentage in real time.
- For group notices, create a custom message for group notification, where `custom_elem_data` stores the title of the group notice, and then store the user ID and the corresponding info in the `key` and `value` of the message extension, respectively.
- For survey, create a custom message, where `custom_elem_data` stores the title and options of the survey, and then store the user ID and the corresponding info in the `key` and `value` of the message extension, respectively.

> ?
- To use this feature, you need to purchase the [Ultimate edition](https://www.tencentcloud.com/document/product/1047/34577).
- This feature is supported only on native SDK 6.7 or later.
- You need to enable this feature via [Chat console](https://console.cloud.tencent.com/im) > **Feature Configuration** > **Login and Message** > **Set message extension**.
- This feature is not available for communities and audio/video groups.

### Setting message extension
Call the `MsgSetMessageExtensions` API ([details](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgSetMessageExtensions.html)) to set the message extension. If an extension already exists, modify its `value` info. Otherwise, add new ones.

The request parameters of the `setMessageExtensions` API are detailed as follows:
<table>
<thead>
<tr>
<th>Attribute</th>
<th>Definition</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>message</td>
<td>Message object</td>
<td>Three message conditions to meet:<ul style="margin-bottom: 0px;"><li>Set <code>message_support_message_extension</code> (<a href="https://comm.qq.com/im/doc/unity/zh/types/MessageAttributes/Message.html">details</a>) to `true` before message sending.</li><li>The message is sent successfully.</li><li>The message is not a message of a community/audio-video group. </li></ul></td>
</tr>
<tr>
<td>extensions</td>
<td>Extensions</td>
<td>Modify the `value` info of an existing extension, or add new extensions.</td>
</tr>
</tbody></table>

> ?
> 1. The `key` and `value` of an extension can contain up to 100 B and 1 KB, respectively. You can set up to 20 extensions each time and 300 extensions for a message.
1. If multiple users set or delete the `key` of the same extension simultaneously, only the first user can operate successfully, and other users will receive the error code 23001 and the latest extension info in the setting response packet, who can set it again if necessary.
2. We recommend setting unique keys of extensions by different users to avoid conflicts in most cases. For example, the `userID` can be set as the `key` of the extension in polling, group notices and survey.

Sample code:

```c#
    // Setting message extension
    var list = new List<MessageExtension>
    {
      new MessageExtension
      {
        message_extension_key = "key",
        message_extension_value = "value"
      }
    };
    TIMResult res = TencentIMSDK.MsgSetMessageExtensions(message, list, (int code, string desc, List<MessageExtensionResult> results, string user_data)=>{
      // Async result of the message extension setting
    });
```

### Getting message extensions

Call the `MsgGetMessageExtensions` API ([details](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgGetMessageExtensions.html)) to get the message extension list.

> ? If the network is unavailable, the SDK will return the message extension list cached locally.

Sample code:

```c#
    // Get message extensions
    TIMResult res = TencentIMSDK.MsgGetMessageExtensions(message, (int code, string desc, List<MessageExtension> list, string user_data)=>{
      // Async result of the message extension getting
    });
```

### Deleting message extensions

Call the `MsgDeleteMessageExtensions` API ([details](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgDeleteMessageExtensions.html)) to delete message extensions. If the value of the `keys` field is set to `null`, all message extensions will be cleared.

Sample code:

```c#
    // Delete message extensions
    var list = new List<MessageExtension>
    {
      new MessageExtension
      {
        message_extension_key = "key",
        message_extension_value = "value"
      }
    };
    TIMResult res = TencentIMSDK.MsgDeleteMessageExtensions(message, list, (int code, string desc, List<MessageExtensionResult> results, string user_data)=>{
      // Async result of the message extension deletion
    });
```

### Updating message extensions

If you have added an event listener for advanced messages via the `SetMsgExtensionsChangedCallback` API, when a message extension is added or updated, you will receive a `MsgExtensionsChangedCallback` ([details](https://comm.qq.com/im/doc/unity/zh/callback/MsgExtensionsChangedCallback.html)) callback.
If you have added an event listener for advanced messages via the `SetMsgExtensionsDeletedCallback` API, when a message extension is added or updated, you will receive a `MsgExtensionsDeletedCallback` ([details](https://comm.qq.com/im/doc/unity/zh/callback/MsgExtensionsDeletedCallback.html)) callback.

Sample code:

```c#
    // Add an event listener for advanced messages
    TencentIMSDK.SetMsgExtensionsChangedCallback((string message_id, List<MessageExtension> message_extension_array, string user_data) => {
      // `message_extension_array` is the list of the modified message extension objects
    });
    TencentIMSDK.SetMsgExtensionsDeletedCallback((string message_id, List<MessageExtension> message_extension_array, string user_data) => {
      // `message_extension_array` is the list of the deleted message extension objects
    });
```
