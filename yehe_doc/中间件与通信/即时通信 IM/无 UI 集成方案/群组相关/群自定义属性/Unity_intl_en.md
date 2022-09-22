## Feature Description
The methods to manipulate group attributes are `GroupGroupInitGroupAttributes`, `GroupGroupDeleteGroupAttributes`, and `GroupGroupGetGroupAttributes`.

A new custom group field is designed based on the API 2.0. It is a "group attribute" that enables seat management in audio chat rooms. When a member mics on, a group attribute can be set to manage the member information. When the member mics off, the group attribute can be deleted. Other members can get the group attribute list to display the seat list.

> ? Currently, the group attribute feature is available only for audio-video groups (AVChatRoom).

The group attribute has the following features:
1. You can create, read, update and delete (CRUD) group attributes directly in the client without console configuration.
2. Up to 16 group attributes are supported. Each group attribute can be up to 4 KB in size, and the total size of all the group attributes can be up to 16 KB.
3. The `GroupInitGroupAttributes`, `setGroupAttributes`, and `GroupDeleteGroupAttributes` APIs can be called by a logged-in user 10 times every 5 seconds in total in the SDK, after which the error code 8511 will be returned, or 5 times every second in total on the backend, after which the error code 10049 will be returned.
4. The `GroupGetGroupAttributes` API can be called by a logged-in user 20 times every 5 seconds in the SDK.

### Initializing the group attributes
Call the `GroupInitGroupAttributes` API ([c#](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_GroupInitGroupAttributes_System_String_com_tencent_imsdk_unity_types_GroupAttributes_com_tencent_imsdk_unity_callback_NullValueCallback_)) to initialize the group attributes, and the original group attributes, if any, will be cleared first.

Sample code:



```c#
// Initialize the group attributes
GroupAttributes attributes = new GroupAttributes
{
  group_atrribute_key = "key",
  group_atrribute_value = "value"
};
TIMResult res = TencentIMSDK.GroupInitGroupAttributes(group_id, attributes, (int code, string desc, string user_data)=>{
 // Process the async logic
});
```


### Deleting the group attributes

Call the `GroupDeleteGroupAttributes` API ([c#](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_GroupDeleteGroupAttributes_System_String_System_Collections_Generic_List_System_String__com_tencent_imsdk_unity_callback_NullValueCallback_)) to delete a specified group attribute. If `keys` is `null`/`nil`, all the group attributes will be cleared.

Sample code:



```c#
// Delete the group attributes
GroupAttributes attributes = new List<string>
{
  "attr1"
};
TIMResult res = TencentIMSDK.GroupDeleteGroupAttributes(group_id, attributes, (int code, string desc, string user_data)=>{
 // Process the async logic
});
```


### Getting the group attributes

Call the `GroupGetGroupAttributes` API ([c#](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_GroupGetGroupAttributes_System_String_System_Collections_Generic_List_System_String__com_tencent_imsdk_unity_callback_ValueCallback_System_Collections_Generic_List_com_tencent_imsdk_unity_types_GroupAttributes___)) to get a specified group attribute. If `keys` is `null`, all the group attributes will be obtained.

Sample code:



```c#
// Get the group attributes
GroupAttributes attributes = new List<string>
{
  "attr1"
};
TIMResult res = TencentIMSDK.GroupGetGroupAttributes(group_id, attributes, (int code, string desc, List<GroupAttributes> attributes, string user_data)=>{
 // Process the async logic
});
```


### Updating the group attributes

If you have called `SetGroupAttributeChangedCallback` to add a group event listener, all the group attributes will be called back through `GroupAttributeChangedCallback` ([c#](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.callback.GroupAttributeChangedCallback.html)) when a group attribute is changed.

Sample code:



```c#
TencentIMSDK.SetGroupAttributeChangedCallback((string group_id, List<GroupAttributes> group_attributes, string user_data)=>{
 // Process the callback logic
});
```





