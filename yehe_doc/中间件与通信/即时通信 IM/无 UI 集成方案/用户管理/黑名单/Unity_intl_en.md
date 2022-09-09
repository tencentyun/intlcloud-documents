## Feature Description
To block a user's messages, add the user to the blocklist.

## Blocklist
### Blocking a user
Call the `FriendshipAddToBlackList` API ([c#](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_FriendshipAddToBlackList_System_Collections_Generic_List_System_String__com_tencent_imsdk_unity_callback_ValueCallback_System_Collections_Generic_List_com_tencent_imsdk_unity_types_FriendResult___)) to add a user to the blocklist, that is, block the user.

By default, a blocked user does not know that he/she is "blocked". After the user sends a message, the error code indicating that he/she has been blocked will not be returned.
To have the "You have been blocked by the user" error message returned after a blocked user sends a message, you can log in to the [IM console](https://console.cloud.tencent.com/im), select **Feature Configuration** > **Login and Message** > **Blocklist Check**, and disable **Show "Sent successfully" After Sending Messages**. Then the SDK will report error code 20007 after a blocked user sends a message.



```c#
// Add a user to the blocklist
List<string> param = new List<string>
  {
    "user_id"
  };
TIMResult res = TencentIMSDK.FriendshipAddToBlackList(param, (int code, string desc, List<FriendResult> result, string user_data)=>{
 // Process the async logic
});
```


### Unblocking a user
Call `FriendshipDeleteFromBlackList` ([c#](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_FriendshipDeleteFromBlackList_System_Collections_Generic_List_System_String__com_tencent_imsdk_unity_callback_ValueCallback_System_Collections_Generic_List_com_tencent_imsdk_unity_types_FriendResult___)) to remove a user from the blocklist, after which messages from the user can be received.



```c#

// Remove a user from the blocklist
List<string> param = new List<string>
  {
    "user_id"
  };
TIMResult res = TencentIMSDK.FriendshipDeleteFromBlackList(param, (int code, string desc, List<FriendResult> result, string user_data)=>{
 // Process the async logic
});
```


### Getting the blocklist
Call `FriendshipGetBlackList` ([c#](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_FriendshipGetBlackList_com_tencent_imsdk_unity_callback_ValueCallback_System_Collections_Generic_List_com_tencent_imsdk_unity_types_FriendProfile___)) to view how many users have been blocked and manage them.



```c#
// Get the blocklist
TIMResult res = TencentIMSDK.FriendshipGetBlackList((int code, string desc, List<FriendProfile> result, string user_data)=>{
 // Process the async logic
});
```




