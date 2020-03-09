This document describes the usage of some basic features of the Tencent Cloud IM SDK to give you a better understanding of the basic processes of Instant Messaging (IM).

## Initialization

Before using the SDK to perform IM operations, you need to initialize the SDK.
**Example:**
```c
int sdk_app_id = 12345678;
std::string json_init_cfg;
Json::Value json_value_dev;
json_value_dev[kTIMDeviceInfoDevId] = "12345678";
json_value_dev[kTIMDeviceInfoPlatform] = TIMPlatform::kTIMPlatform_Windows;
json_value_dev[kTIMDeviceInfoDevType] = "";

Json::Value json_value_init;
json_value_init[kTIMSdkConfigLogFilePath] = path;
json_value_init[kTIMSdkConfigConfigFilePath] = path;
json_value_init[kTIMSdkConfigAccountType] = "107";
json_value_init[kTIMSdkConfigDeviceInfo] = json_value_dev;

TIMInit(sdk_app_id, json_value_init.toStyledString().c_str());
```

You can obtain the SDKAppID after creating an app in the IM [console](https://console.cloud.tencent.com/im). For more information on initialization operations, see [Initialization](https://cloud.tencent.com/document/product/269/33546).


## Login/Logout
### Login
- Users can normally send and receive messages only after they have logged in to the Tencent backend server. To log in to the Tencent backend server, a user needs to provide information including UserID and UserSig. For more information, see [Login Authentication](https://cloud.tencent.com/document/product/269/31999).
Login is an asynchronous process, and the result returned by the callback function indicates whether the login was successful. Users can proceed to subsequent operations only after successful login. When login succeeds or fails, the system will trigger the corresponding callback.

**Example:**

```c
const void* user_data = nullptr; // Return of the callback function
const char* id = "WIN01"; 
const char* user_sig = "WIN01UserSig";
TIMLogin(id, user_sig, [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
    if (code != ERR_SUCC) {
        // Failed to log in
        return;
    }
    // Logged in successfully
    
}, user_data);
```

>Here, code indicates the error code and desc indicates error description. For more information, see [Error Codes](https://cloud.tencent.com/document/product/269/1671).

**onForceOffline**

If this user has been forced logout by another client, the login fails and returns the error code (`ERR_IMSDK_KICKED_BY_OTHERS: 6208`). If a user is forced logout, be sure to notify the user of this with a notification window such as an Alert window. For more information on forcible logout, see [User State Changes](https://cloud.tencent.com/document/product/269/33551#timsetkickedofflinecallback).


**onUserSigExpired**
Every UserSig has an expiration time. When a UserSig expires, `login` returns error code `70001`. If you receive this error code, request a new UserSig from your business server. For more information, see [User Ticket Expiration](https://cloud.tencent.com/document/product/269/33551#timsetusersigexpiredcallback).


## Logout
The logout operation needs to be called if the user wants to log out or switch to another user.

**Example:**

```c
const void* user_data = nullptr; // Return of the callback function
TIMLogout([](int32_t code, const char* desc, const char* json_param, const void* user_data) { 
    if (code != ERR_SUCC) { 
        // Failed to log out
        return;
    }
    // Logged out successfully
    
}, user_data);
```

> When you need to switch to another account, `login` can be called again only after the `logout` callback succeeds or fails. Otherwise, `login` may fail.
For more information on login and logout operations, see [Login and Logout](https://cloud.tencent.com/document/product/269/33547).

## Sending Messages

### Obtaining conversations

A conversation refers to a conversation with a user or a group. To send or receive messages in a one-to-one or group conversation, you need to first obtain the conversation by specifying the conversation type (one-to-one chat or group chat) and the peer’s identifier (the peer’s account or group ID).


**Example of obtaining the one-to-one conversation with a recipient whose UserID is Windows-02**

```c
const void* user_data = nullptr; // Return of the callback function
const char* userid = "Windows-02";
int ret = TIMConvCreate(userid, kTIMConv_C2C, [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
    // The callback returns details about the conversation.
}, user_data);
if (ret != TIM_SUCC) {
    // Failed to call the TIMConvCreate API
}
```

**Example of obtaining the conversation with the group ID of Windows-Group-01** 

```c
const void* user_data = nullptr; // Return of the callback function
const char* groupid = "Windows-Group-01";
int ret = TIMConvCreate(groupid, kTIMConv_Group, [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
    // The callback returns details about the conversation.
}, user_data);
if (ret != TIM_SUCC) {
    // Failed to call the TIMConvCreate API
}
```


### Sending messages

In the IM SDK, messages are represented by `TIMMessage`. Each `TIMMessage` consists of multiple `TIMElem` objects. A `TIMElem` object can be text or an image, which means a message can contain multiple objects including the text, image, and other objects.

![](https://main.qcloudimg.com/raw/2841a6842e0f46d2ac71eae1e5a13e05.png)

**Example:**

```c
const void* user_data = nullptr; // Return of the callback function
Json::Value json_value_text;
json_value_text[kTIMElemType] = kTIMElem_Text;
json_value_text[kTIMTextElemContent] = "Message Send to Windows-02";
Json::Value json_value_msg;
json_value_msg[kTIMMsgElemArray].append(json_value_text);

const char* userid = "Windows-02";
int ret = TIMMsgSendNewMsg(userid, kTIMConv_C2C, json_value_msg.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
    if (code != ERR_SUCC) { 
        // Failed to send the message
        return;
    }
    // Sent the message successfully
    
}, user_data);
if (ret != TIM_SUCC) {
    // Failed to call the TIMMsgSendNewMsg API
}
```

## Receiving Messages
In most cases, users need to be notified of new messages. For this purpose, you simply need to register the new message notification callback `TIMMessageListener`. When the user logs in, offline messages will be pulled. To avoid missing message notifications, register the listener callback for new messages before login.

**Example of setting a message listener**

```c
// Sets a new message listener. When a new message arrives, a callback is triggered through this listener.
const void *user_data = nullptr;
TIMSetRecvNewMsgCallback([](const char* json_msg_array, const void* user_data) {
    Json::Value json_value_msgs; // Parse the message
    Json::Reader reader;
    if (!reader.parse(json_msg_array, json_value_msgs)) {
        printf("reader parse failure!%s", reader.getFormattedErrorMessages().c_str());
        return;
    }
    for (Json::ArrayIndex i = 0; i < json_value_msgs.size(); i++) {  // Traverse messages
        Json::Value& json_value_msg = json_value_msgs[i];
        Json::Value& elems = json_value_msg[kTIMMsgElemArray];
        for (Json::ArrayIndex m = 0; m < elems.size(); m++) {   // Traverse Elems
            Json::Value& elem = elems[i];

            uint32_t elem_type = elem[kTIMElemType].asUInt();
            if (elem_type == TIMElemType::kTIMElem_Text) {  // Text
                
            }else if (elem_type == TIMElemType::kTIMElem_Sound) {  // Audio
                
            } else if (elem_type == TIMElemType::kTIMElem_File) {  // File
                
            } else if (elem_type == TIMElemType::kTIMElem_Image) { // Image
                
            }
        }
    }
    
}, user_data);
```

For more information on receiving and sending messages, see [Sending Messages](https://cloud.tencent.com/document/product/269/33549) and [Receiving Messages](https://cloud.tencent.com/document/product/269/33551#timaddrecvnewmsgcallback).

## Group Management

There are multiple group types in IM. For information on their characteristics and limits, see the [Group System](https://cloud.tencent.com/document/product/269/1502#.E7.BE.A4.E7.BB.84.E5.BD.A2.E6.80.81.E4.BB.8B.E7.BB.8D). A group is identified by a unique ID, which allows for different operations. Group-related operations are implemented by `TIMGroupManager`, which can be used after login.

| Type | Description |
| --------------------------- | ----------------------------------------------------------- |
| Private | This is suitable for more private chat scenarios, where the group profile is not made public and a user can join the group only by being invited by a group member. Private groups are similar to groups in WeChat. |
| Public | This is suitable for public chat scenarios. Public groups have a strict management and admission mechanism. |
| ChatRoom | Chatroom members can join and quit freely. |
| AVChatRoom | This is similar to ChatRoom, but supports an unlimited number of group members. |
| BChatRoom | This is suitable for scenarios where messages are pushed to all online users. |


### Creating a group

The following example shows how to create a public group named Windows-Group-Name and invite user Windows_002 to the group. 
**Example:**

```c
Json::Value json_group_member_array(Json::arrayValue);
// Initial group members
Json::Value json_group_member;
json_group_member[kTIMGroupMemberInfoIdentifier] = "Windows_002";
json_group_member[kTIMGroupMemberInfoMemberRole] = kTIMGroupMemberRoleFlag_Member;
json_group_member_array.append(json_group_member);

Json::Value json_value_createparam;
json_value_createparam[kTIMCreateGroupParamGroupId] = "Windows-Group-01";
json_value_createparam[kTIMCreateGroupParamGroupType] = kTIMGroup_Public;
json_value_createparam[kTIMCreateGroupParamGroupName] = "Windows-Group-Name";
json_value_createparam[kTIMCreateGroupParamGroupMemberArray] = json_group_member_array;

json_value_createparam[kTIMCreateGroupParamNotification] = "group notification";
json_value_createparam[kTIMCreateGroupParamIntroduction] = "group introduction";
json_value_createparam[kTIMCreateGroupParamFaceUrl] = "group face url";
json_value_createparam[kTIMCreateGroupParamMaxMemberCount] = 2000;
json_value_createparam[kTIMCreateGroupParamAddOption] = kTIMGroupAddOpt_Any;

const void* user_data = nullptr;
int ret = TIMGroupCreate(json_param.c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
    if (code != ERR_SUCC) { 
        // Failed to create the group
        return;
    }
    
    // Created the group successfully and parsed the JSON string to obtain the GroupID
    
}, user_data))
```

For more information on group operations, see [Group APIs](https://cloud.tencent.com/document/product/269/33550).

### Group messages
Group messages are similar to C2C (one-to-one chat) messages and require you to enter the group ID and group type `kTIMConv_Group` when the message is sent. For more information, see [Sending Messages](https://cloud.tencent.com/document/product/269/33549) in SDK documentation.
