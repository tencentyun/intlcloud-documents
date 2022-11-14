This document will guide you through the whole process of intergating Tencent Cloud IM SDK into your project.

## Environment Requirements

| Platform    | Version                                                         |
| ------- | ------------------------------------------------------------ |
| Unity   | 2019.4.15f1 or above                                     |
| Android | Android Studio 3.5 or above; devices with Android 4.1 or above for apps|
| iOS     | Xcode 11.0 or above. Ensure that your project has a valid developer signature.|

## Supported Platforms

We apply ourselves to the development of full platform coverage Tencent Cloud IM SDK in Unity, assisting you to run on any platform with one set of code.

| Platform | IM SDK |
|---------|---------|
| iOS | Supported |
| Android | Supported |
| macOS | Supported |
| Windows | Supported |
| [Web](#web) | Supported since v.1.8.1 |

>? Build for Web needs excessive stpes, please check on [Part 5](#web)。

## Prerequisites

1. You have [signed up](https://www.tencentcloud.com/document/product/378/17985) for a Tencent Cloud account and completed [identity verification](https://www.tencentcloud.com/document/product/378/3629).
2. Create an application by the guide [Creating and Upgrading an Application](https://www.tencentcloud.com/document/product/1047/34577), and keep record of your `SDKAppID`.

[](id:part1)

## Part 1. Create an IM app

1. Log in to the [IM console](https://console.cloud.tencent.com/im)。
>?If you already have an app, record its SDKAppID and [obtain key information](#part2)。
>A Tencent Cloud account can create a maximum of 300 IM apps. If you want to create a new app, [disable and delete](https://www.tencentcloud.com/document/product/1047/34540) an unwanted app first. **Once an app (along with its SDKAppID) is deleted, the service it provides and all its data are lost. Proceed with caution.**
>
2. Click **Create Application**, enter your app name, and click **Confirm**.
![](https://main.qcloudimg.com/raw/15e61a874a0640d517eeb67e922a14bc.png)
3. Select **[Auxiliary Tools](https://console.cloud.tencent.com/im/tool-usersig)** > **UserSig Generation and Verification** on the left sidebar. Create a `UserID` and the corresponding `UserSig`, and copy the signature information for login.
![](https://main.qcloudimg.com/raw/2286644d987d24caf565142ae30c4392.png)


[](id:part2)

## Part 2. Intergrate Tencent Cloud IM SDK into your Unity project

1. Use Unity to create a project, and record the project directory. Or open your preexisted Unity project.

2. Open the project with an IDE (such as Visual Studio Code):
![](https://qcloudimg.tencent-cloud.cn/raw/1a21933037a72a6bd4c8ed14f08c6ca7.png)
3. Find Packages/manifest.json based on the directory, and modify dependencies as follows:
```json
{
    "dependencies":{
    "com.tencent.imsdk.unity":"https://github.com/TencentCloud/TIMSDK.git#unity"
  }
}
```

For you to better understand all the APIs within Tencent Cloud IM SDK, we have offered [API Example](https://github.com/TencentCloud/TIMSDK/tree/master/Unity/im_unity_sdk_plus/Assets/IM_Api_Example) for testing SDK APIs and calling certain APIs on the early stage of development.

[](id:part3)
## Part 3. Load dependencies
Open the project in the Unity Editor, wait until dependencies are loaded, and confirm the Tencent Cloud IM is successfully loaded.
![](https://qcloudimg.tencent-cloud.cn/raw/d98dfb17bbee6c0319e370de6f2ba9dd.jpg)

[](id:part4)
## Part 4. Integrate with your own UI

### Prerequisites

You have created an Unity project and loaded Tencent Cloud IM SDK.

### Initialize SDK

[Detailed document for the section](https://www.tencentcloud.com/document/product/1047/48570)

Invoke `TencentIMSDK.Init` to initialize SDK, by passing your `SDKAppID`.

```c#
public static void Init() {
      int sdkappid = 0; // Get the `SDKAppID` from the IM console
      SdkConfig sdkConfig = new SdkConfig();
       sdkConfig.sdk_config_config_file_path = Application.persistentDataPath + "/TIM-Config";
       sdkConfig.sdk_config_log_file_path = Application.persistentDataPath + "/TIM-Log";
       TIMResult res = TencentIMSDK.Init(long.Parse(sdkappid), sdkConfig);
}
```

After `Init`, you are able to add event listeners to listen to network status changes, user information modifications and so on, check more on [here](https://www.tencentcloud.com/document/product/1047/48570).

### Login

[Detailed document for the section](https://www.tencentcloud.com/document/product/1047/48571)

Now, you can login the testing account created on the web console.

Invoke `TencentIMSDK.Login` to login your account.

When return `res.code` equals to 0, login succeeded.

```c#
public static void Login() {
  if (userid == "" || user_sig == "")
  {
      return;
  }
  TIMResult res = TencentIMSDK.Login(userid, user_sig, (int code, string desc, string json_param, string user_data)=>{

  });
}
```

### Send Message

[Detailed document for the section](https://www.tencentcloud.com/document/product/1047/48572)

Here is the example code for sending text message:

```c#
public static void MsgSendMessage() {
      string conv_id = ""; // The conversation ID of a one-to-one message is the `userID`, and that of a group message is the `groupID`.
      Message message = new Message
      {
        message_conv_id = conv_id,
        message_conv_type = TIMConvType.kTIMConv_C2C, // It is `TIMConvType.kTIMConv_Group` for a group message.
        message_elem_array = new List<Elem>
        {
          new Elem
          {
            elem_type = TIMElemType.kTIMElem_Text,
            text_elem_content =  "This is an ordinary text message"
          }
        }
      };
      StringBuilder messageId = new StringBuilder(128);
       TIMResult res = TencentIMSDK.MsgSendMessage(conv_id, TIMConvType.kTIMConv_C2C, message, messageId, (int code, string desc,                         string json_param, string user_data)=>{
        // Async message sending result
      });
            // The message ID `messageId` returned when the message is sent
}
```

### Acquire Conversation List

[Detailed document for the section](https://www.tencentcloud.com/document/product/1047/48871)

In the last step, you have successfully sent testing messages, and now you can login to another account to retrieve the conversation list.

Two ways to acquire conversation list:

1. Listen to the conversation event.
2. Call API to get conversation list.

Common scene is:

After init the app, retrieve the conversation list immediately, and then listen to the conversation events.

#### Get conversaion list from API

```c#
TIMResult res = TencentIMSDK.ConvGetConvList((int code, string desc, List<ConvInfo> info_list, string user_data)=>{

});
```

#### Listen to the conversation updates

```c#
TencentIMSDK.SetConvEventCallback((TIMConvEvent conv_event, List<ConvInfo> conv_list, string user_data)=>{

});
```

### Receive Message

[Detailed document for the section](https://www.tencentcloud.com/document/product/1047/48871)

There are two ways to receive messages:

1. Set message receiver listener.
2. Call API to retrieve messages.

#### Pulling Historical One-to-One Messages

```c#
// Pull historical one-to-one messages
// Set `msg_getmsglist_param_last_msg` to `null` for the first pull
// `msg_getmsglist_param_last_msg` can be the last message in the returned message list for the second pull.
var get_message_list_param = new MsgGetMsgListParam
 {
   msg_getmsglist_param_last_msg = LastMessage
 };
TIMResult res = TencentIMSDK.MsgGetMsgList(conv_id, TIMConvType.kTIMConv_C2C, get_message_list_param, (int code, string desc, string user_data) => {
// Process the callback logic
});

```

#### Pulling Historical Group Messages

```c#
// Pull historical group messages
// Set `msg_getmsglist_param_last_msg` to `null` for the first pull
// `msg_getmsglist_param_last_msg` can be the last message in the returned message list for the second pull.
var get_message_list_param = new MsgGetMsgListParam
 {
   msg_getmsglist_param_last_msg = LastMessage
 };
TIMResult res = TencentIMSDK.MsgGetMsgList(conv_id, TIMConvType.kTIMConv_Group, get_message_list_param, (int code, string desc, string user_data) => {
// Process the callback logic
});

```

#### Set listener for receiving new messages

```c#
TencentIMSDK.AddRecvNewMsgCallback((List<Message> message, string user_data) => {

});
```

Now, you have tested the base functionality of Tencent Cloud IM.

You can further explore the following features:

- [Group](https://www.tencentcloud.com/document/product/1047/48169)
- [User Profile](https://www.tencentcloud.com/document/product/1047/48859)
- [Friendship Management](https://www.tencentcloud.com/document/product/1047/49563)
- [Local Search](https://www.tencentcloud.com/document/product/1047/50066)

[](id:part5)
## Part 5. Unity for WebGL[](id:web)

Tencent Cloud IM SDK (Unity) supports build for WebGL after version `1.8.1`.

After build WebGL, you need to mannually import [Web SDK Script](https://github.com/TencentCloud/TIMSDK/tree/master/Web/IMSDK) to your build folder.

And you need to import those files in your home page `index.html`.
   ``` html
    <script src="./tim-js.js"></script>
    <script src="./tim-js-friendship.js"></script>
    <script src="./tim-upload-plugin.js"></script>
   ```

## FAQs

### What platforms are supported?
iOS, Android, Windows, macOS and WebGL are supported.

### What should I do if clicking Build And Run for an Android device triggers an error, stating no available device is found?
Check that the device is not occupied by other resources. Alternatively, click Build to generate an APK package, drag it to the simulator, and run it.

### What should I do if an error occurs during the first run for an iOS device?
If an error is reported for an iOS device after the demo configured as above is run, choose **Product > Clean** to clean the product, and build the demo again. You can also close Xcode and open it again, and then build the demo again.
### What should I do if Unity v2019.04 reports the following error for iOS?
Library/PackageCache/com.unity.collab-proxy@1.3.9/Editor/UserInterface/Bootstrap.cs(23,20): error CS0117: 'Collab' does not contain a definition for 'ShowChangesWindow'
Choose **Window > Package Manager** on the toolbar of the Editor and downgrade Unity Collaborate to 1.2.16.

### What should I do if Unity v2019.04 reports the following error for iOS?
Library/PackageCache/com.unity.textmeshpro@3.0.1/Scripts/Editor/TMP_PackageUtilities.cs(453,84): error CS0103: The name 'VersionControlSettings' does not exist in the current context
Open the source code and delete the code snippet of `|| VersionControlSettings.mode != "Visible Meta Files"`.
