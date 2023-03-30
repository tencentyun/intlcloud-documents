- [](id:toc)
  This document describes how to integrate the SDK for Unity.

  ## Environment Requirements

  | Environment | Version                                                      |
  | ----------- | ------------------------------------------------------------ |
  | Unity       | 2019.4.15f1 or later                                         |
  | Android     | Android Studio 3.5 or later; devices with Android 4.1 or later for apps |
  | iOS         | Xcode 11.0 or later. Ensure that your project has a valid developer signature. |

  ## Supported Platforms

  We are committed to building a set of Chat SDK and TUIKit for all Unity platforms, allowing you to run one set of code on all platforms.

  | Platform    | Chat SDK              |
  | ----------- | --------------------- |
  | iOS         | Supported             |
  | Android     | Supported             |
  | macOS       | Supported             |
  | Windows     | Supported             |
  | [Web](#web) | Supported from 1.8.1+ |

  >? For web, you need to perform a few extra steps for SDK integration. For details, see [Part 5](#web).

  ## Prerequisite

  1. You have [signed up](https://intl.cloud.tencent.com/document/product/378/17985) for a Tencent Cloud account and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).
  2. You have created an application as instructed in [Creating and Upgrading an Application](https://intl.cloud.tencent.com/document/product/1047/34577) and recorded the `SDKAppID`.

  [](id:part1)

  ## Part 1. Creating Test Accounts

  In the [Chat console](https://console.cloud.tencent.com/im), select your application and click **Auxiliary Tools** > **UserSig Generation & Verification** on the left sidebar. Create two `UserID` values and their `UserSig` values, and copy the `UserID`, `Key`, and `UserSig` for subsequent logins.

  >? This account is for development and testing only. Before the application is launched, the correct `UserSig` distribution method is to use the server to generate `UserSig` and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).

  ![](https://main.qcloudimg.com/raw/2286644d987d24caf565142ae30c4392.png)

  [](id:part2)

  ## Part 2. Integrating Chat SDK into Your Unity Project

  1. Use Unity to create a project, and record the project directory.
  Or open an existing Unity project.
  2. Open the project with an IDE (such as Visual Studio Code):
  ![](https://qcloudimg.tencent-cloud.cn/raw/1a21933037a72a6bd4c8ed14f08c6ca7.png)
  3. Find Packages/manifest.json based on the directory, and modify dependencies as follows:
  ```json
     {
       "dependencies":{
         "com.tencent.imsdk.unity":"https://github.com/TencentCloud/chat-sdk-unity.git#unity"
       }
     }
  ```

  To help you better understand Chat SDK APIs, sample APIs are provided [here](https://github.com/TencentCloud/tc-chat-sdk-unity/tree/main/Assets/IM_Api_Example) to demonstrate how to call APIs and trigger listeners.

  [](id:part3)

  ## Part 3. Loading Dependencies

  Open the project in the Unity Editor, wait until dependencies are loaded, and confirm the Tencent Cloud Chat is successfully loaded.
  ![](https://qcloudimg.tencent-cloud.cn/raw/d98dfb17bbee6c0319e370de6f2ba9dd.jpg)

  [](id:part4)

  ## Part 4. Implementing UI on Your Own

  ### Prerequisites

  You have created a Unity project or have a project that can be based on Unity, and have loaded Tencent Cloud Chat SDK.

  ### Initializing the SDK

  [Detailed documentation](https://intl.cloud.tencent.com/document/product/1047/48570)

  Call `TencentIMSDK.Init` to initialize the SDK.

  Pass in your `SDKAppID`.

  ```c#
  public static void Init() {
    int SDKAppID = 0; // Get the `SDKAppID` from the Chat console
    SdkConfig sdkConfig = new SdkConfig();
  
    sdkConfig.sdk_config_config_file_path = Application.persistentDataPath + "/TIM-Config";
  
    sdkConfig.sdk_config_log_file_path = Application.persistentDataPath + "/TIM-Log";
  
    TIMResult res = TencentIMSDK.Init(long.Parse(SDKAppID), sdkConfig);
  }
  ```

  After `Init`, you can mount some listeners to the Chat SDK, mainly including those for network status and user information change. For more information, see [here](https://intl.cloud.tencent.com/document/product/1047/48570).

  ### Logging in with a test account

  [Detailed documentation](https://intl.cloud.tencent.com/document/product/1047/48571)

  Log in with a test account initially generated for verification.

  Call the `TencentIMSDK.Login` method to log in with the test account.

  If the returned `res.code` is `0`, the login is successful.

  ```c#
  public static void Login() {
    if (userid == "" || user_sig == "")
    {
        return;
    }
    TIMResult res = TencentIMSDK.Login(userid, user_sig, (int code, string desc, string json_param, string user_data)=>{
      // Process the login callback logic
    });
  }
  ```

  >?This account is for development and testing only. Before the application is launched, the correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).

  ### Sending a message

  [Detailed documentation](https://intl.cloud.tencent.com/document/product/1047/48572)

  The following shows how to send a text message:

  Sample code:

  ```c#
  public static void MsgSendMessage() {
          string conv_id = ""; // The conversation ID of a one-to-one message is the `userID`, and that of a group message is the `groupID`.
          Message message = new Message
          {
            message_conv_id = conv_id,
            message_conv_type = TIMConvType.kTIMConv_C2C, // For a group message, this value is `TIMConvType.kTIMConv_Group`
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
                // The message ID messageId returned when the message is sent
  }
  ```

  > ?If sending fails, it may be that your `SDKAppID` doesn't support sending messages to strangers. In this case, you can enable the feature in the console for testing.
  >
  > Disable the friend relationship chain check [here](https://console.cloud.tencent.com/im/login-message).

  ### Obtaining the conversation list

  [Detailed documentation](https://intl.cloud.tencent.com/document/product/1047/50020)

  Log in with the other test account to pull the conversation list.

  The conversation list can be obtained in two ways:

  1. Listen for the persistent connection callback to update the conversation list in real time.
  2. Call the API to get the paginated conversation list at a time.

  Common use cases include:

  Get the conversation list upon application start and listen for the persistent connection to update the conversation list in real time.

  #### Requesting the conversation list at a time

  ```c#
  TIMResult res = TencentIMSDK.ConvGetConvList((int code, string desc, List<ConvInfo> info_list, string user_data)=>{
   // Process the async logic
  });
  ```

  At this point, you can see the message sent by the other test account in the previous step.

  #### Listening for the persistent connection to get the conversation list in real time

  Mount listeners to the SDK, process the callback event, and update the UI.

  1. Mount listeners.
  ```c#
  TencentIMSDK.SetConvEventCallback((TIMConvEvent conv_event, List<ConvInfo> conv_list, string user_data)=>{
   // Process the callback logic
  });
  ```
  2. Process the callback event and display the latest conversation list on the UI.

  ### Receiving messages

  [Detailed documentation](https://intl.cloud.tencent.com/document/product/1047/48573)

  Messages can be received with the Chat SDK in two ways:

  1. Listen for the persistent connection callback to get message changes and update and render the historical message list in real time.
  2. Call the API to get the paginated message history at a time.

  Common use cases include:

  1. After a new conversation is opened on the UI, request a certain number of historical messages at a time to display the historical message list.
  2. Listen for the persistent connection to receive messages in real time and add them to the historical message list.

  #### Requesting the historical message list at a time

  To avoid affecting the pull speed, we recommend you limit the number of messages to be pulled per page to 20.

  You need to dynamically record the current number of pages for the next request.

  Sample code:

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

  #### Listening for the persistent connection to get new messages in real time

  After the historical message list is initialized, new messages are from the persistent connection `TencentIMSDK.AddRecvNewMsgCallback`.

  After the `AddRecvNewMsgCallback` callback is triggered, you can add new messages to the historical message list as needed.

  Sample code for binding a listener:

  ```c#
  TencentIMSDK.AddRecvNewMsgCallback((List<Message> message, string user_data) => {
    // Process new messages
  });
  ```

  At this point, you have completed the Chat module development, and now users can send and receive messages and enter different conversations.

  You can develop more features, such as [group](https://intl.cloud.tencent.com/document/product/1047/48169), [user profile](https://intl.cloud.tencent.com/document/product/1047/48859), [relationship chain](https://intl.cloud.tencent.com/document/product/1047/49563), and [local search](https://intl.cloud.tencent.com/document/product/1047/50066).

  For more information, see [Integration Solution (Implementing UI on Your Own)](https://www.tencentcloud.com/document/product/1047/34299).

  [](id:part5)

  ## Part 5. Enabling Unity Support for WebGL[](id:web)

  Tencent Cloud Chat SDK for Unity 1.8.1 or later supports building WebGL.

  To enable support for web, you need to perform the following extra steps, compared with the steps to enable support for Android and iOS:

  ### Importing JS

  Download the following three JS files from GitHub and place them in the WebGL artifacts directory under the project:

  - [tim-js](https://github.com/TencentCloud/TIMSDK/blob/master/Web/IMSDK/tim-js.js)
  - [tim-js-friendship.js](https://github.com/TencentCloud/TIMSDK/blob/master/Web/IMSDK/tim-js-friendship.js)
  - [Rename this file to tim-upload-plugin.js](https://github.com/TencentCloud/TIMSDK/blob/master/Web/IMSDK/tim-upload-plugin/index.js)
  Open `index.html` and import the three JS files as follows:

  ```html
  <script src="./tim-js.js"></script>
  <script src="./tim-js-friendship.js"></script>
  <script src="./tim-upload-plugin.js"></script>
  ```

  ## FAQs

  #### What platforms are supported?

  iOS, Android, Windows, macOS, and WebGL are supported.

  #### What should I do if clicking **Build And Run** for an Android device triggers an error, stating no available device is found?

  Check that the device is not occupied by other resources. Alternatively, click **Build** to generate an APK package, drag it to the simulator, and run it.

  #### What should I do if an error occurs during the first run for an iOS device?

  If an error is reported for an iOS device after the demo configured as above is run, choose **Product** > **Clean** to clean the product, and build the demo again. You can also close Xcode and open it again, and then build the demo again.

  #### What should I do if Unity v2019.04 reports the following error for iOS?

  Library/PackageCache/com.unity.collab-proxy@1.3.9/Editor/UserInterface/Bootstrap.cs(23,20): error CS0117: 'Collab' does not contain a definition for 'ShowChangesWindow'
  Choose **Window** > **Package Manager** on the toolbar of the Editor and downgrade Unity Collaborate to 1.2.16.

  #### What should I do if Unity v2019.04 reports the following error for iOS?

  Library/PackageCache/com.unity.textmeshpro@3.0.1/Scripts/Editor/TMP_PackageUtilities.cs(453,84): error CS0103: The name 'VersionControlSettings' does not exist in the current context
  Open the source code and delete the code snippet of `|| VersionControlSettings.mode != "Visible Meta Files"`.

  #### How do I query error codes?

  - For Chat SDK API error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
