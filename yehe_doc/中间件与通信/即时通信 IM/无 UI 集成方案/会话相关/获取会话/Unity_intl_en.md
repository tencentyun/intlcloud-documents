## Feature Description
The IM SDK provides an API for getting conversations, which you can use to get the `ConvInfo` object information of one or multiple specified conversations.
Call `ConvGetConvInfo` ([c#](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_ConvGetConvInfo_System_Collections_Generic_List_com_tencent_imsdk_unity_types_ConvParam__com_tencent_imsdk_unity_callback_ValueCallback_System_Collections_Generic_List_com_tencent_imsdk_unity_types_ConvInfo___)) to get the information of one or multiple conversations.


Sample code:


```c#
List<ConvParam> list = new List<ConvParam>();
ConvParam conv1 = new ConvParam();
conv1.get_conversation_list_param_conv_id = "group_conv_id";
conv1.get_conversation_list_param_conv_type = TIMConvType.kTIMConv_Group;
list.Add(conv1);
ConvParam conv2 = new ConvParam();
conv2.get_conversation_list_param_conv_id = "c2c_conv_id";
conv2.get_conversation_list_param_conv_type = TIMConvType.kTIMConv_C2C;
list.Add(conv2);
TIMResult res = TencentIMSDK.ConvGetConvInfo(list, (int code, string desc, List<ConvInfo> info_list, string user_data)=>{
 // Process the async logic
});
```


