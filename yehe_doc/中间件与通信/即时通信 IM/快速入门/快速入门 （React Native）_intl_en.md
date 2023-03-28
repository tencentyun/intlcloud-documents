This document describes how to quickly run the Tencent Cloud Chat demo for React Native.

## Environment Requirements

|              | Version                                                                 |
| ------------ | -------------------------------------------------------------------- |
| React Native | v0.63.4 or later                                                      |
| Android | Android Studio 3.5 or later; devices with Android 4.1 or later for apps |
| iOS | Xcode 11.0 or later. Ensure that your project has a valid developer signature. |

## Prerequisites

You have [signed up](https://intl.cloud.tencent.com/document/product/378/17985) for a Tencent Cloud account and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Part 1. Creating Test Accounts

In the [Chat console](https://console.cloud.tencent.com/im), select your application and click **Auxiliary Tools** > **UserSig Generation & Verification** on the left sidebar. Create two `UserID` values and their `UserSig` values, and copy the `UserID`, `Key`, and `UserSig` for subsequent logins.

>? This account is for development and testing only. Before the application is launched, the correct `UserSig` distribution method is to use the server to generate `UserSig` and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).

![](https://main.qcloudimg.com/raw/2286644d987d24caf565142ae30c4392.png)

[](id:part2)

Part 2. Integrating the SDK for React Native

### Prerequisites

You have created a React Native application or have an application that can be based on React Native.

### Directions

#### Installing the Chat SDK
Run the following command to install the latest version of the Chat SDK for React Native:
```shell
// npm
npm install react-native-tim-js

// yarn
yarn add react-native-tim-js
```

#### Initializing the SDK
Call `initSDK` to initialize the SDK and pass in your `sdkAppID`.
```javascript
import { TencentImSDKPlugin, LogLevelEnum } from 'react-native-tim-js';

TencentImSDKPlugin.v2TIMManager.initSDK(
    sdkAppID: 0, // Replace 0 with the SDKAppID of your Chat application when integrating
    loglevel: LogLevelEnum.V2TIM_LOG_DEBUG, // Log
    listener: V2TimSDKListener(),
);
```

In this step, you can mount some listeners to the Chat SDK, mainly including those for network status and user information change. For more information, see [Interface V2TimSDKListener](https://comm.qq.com/im/doc/RN/zh/Interface/Listener/V2TimSDKListener.html).

#### Logging in with a test account
1. Log in with a test account initially generated in the console for verification.
2. Call the `TencentImSDKPlugin.v2TIMManager.login` method to log in with a test account. If the returned `res.code` is `0`, the login is successful.
```javascript
import { TencentImSDKPlugin } from 'react-native-tim-js';
 const res = await TencentImSDKPlugin.v2TIMManager.login(
    userID: userID,
    userSig: userSig,
  );
```
>?This account is for development and testing only. Before the application is launched, the correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).

#### Sending messages

The following shows how to send a text message:
1. Call `createTextMessage(String)` to create a text message.
2. Get the message ID from the returned value.
3. Call `sendMessage()` to send the message with the ID. `receiver` can be the ID of the other test account created earlier. `groupID` is not required for sending a one-to-one message.

Sample code:

```javascript
import { TencentImSDKPlugin } from 'react-native-tim-js';

const createMessage =
      await TencentImSDKPlugin.v2TIMManager
          .getMessageManager()
          .createTextMessage("The text to create");

const id = createMessage.data!.id!; // The message creation ID

const res = await TencentImSDKPlugin.v2TIMManager
      .getMessageManager()
      .sendMessage(
          id: id, // Pass in the message creation ID to
          receiver: "The userID of the destination user",
          groupID: "The groupID of the destination group",
          );
```

> ?If sending fails, it may be that your `sdkAppID` doesn't support sending messages to strangers. In this case, you can enable the feature in the console for testing.
>
> Disable the friend relationship chain check [here](https://console.cloud.tencent.com/im/login-message).

#### Obtaining the conversation list

Log in with the other test account to pull the conversation list.

The conversation list can be obtained in two ways:

1. Listen for the persistent connection callback to update the conversation list in real time.
2. Call the API to get the paginated conversation list at a time.

Common use cases include:

Get the conversation list upon application start and listen for the persistent connection to update the conversation list in real time.

##### Requesting the conversation list at a time

To get the conversation list, you need to maintain `nextSeq` and record its current position.

```typescript
import { useState } from "react";
import { TencentImSDKPlugin } from "react-native-tim-js";

const [nextSeq, setNextSeq] = useState<string>("0");

const getConversationList = async () => {
  const count = 10;
  const res = await TencentImSDKPlugin.v2TIMManager
    .getConversationManager()
    .getConversationList(count, nextSeq);
  setNextSeq(res.data?.nextSeq ?? "0");
};
```

At this point, you can see the message sent by the other test account in the previous step.

##### Listening for the persistent connection to get the conversation list in real time

Mount listeners to the SDK, process the callback event, and update the UI.

1. Mount listeners.
```javascript
import { TencentImSDKPlugin } from "react-native-tim-js";

const addConversationListener = () => {
  TencentImSDKPlugin.v2TIMManager
    .getConversationManager()
    .addConversationListener({
      onNewConversation: (conversationList) => {
        // new conversation created callback
        _onConversationListChanged(conversationList);
      },
      onConversationChanged: (conversationList) => {
        // conversation changed callback
        _onConversationListChanged(conversationList);
      },
    });
};
```

2. Process the callback event and display the latest conversation list on the UI.
```javascript
const _onConversationListChanged = (list) => {
  // you can use conversation list to update UI
};
```

#### Receiving messages

Messages can be received with the Chat SDK for React Native in two ways:

1. Listen for the persistent connection callback to get message changes and update and render the historical message list in real time.
2. Call the API to get the paginated message history at a time.

Common use cases include:

1. After a new conversation is opened on the UI, request a certain number of historical messages at a time to display the historical message list.
2. Listen for the persistent connection to receive messages in real time and add them to the historical message list.

##### Requesting the historical message list at a time

To avoid affecting the pull speed, we recommend you limit the number of messages to be pulled per page to 20.

You need to dynamically record the current number of pages for the next request.

Sample code:

```javascript
import { TencentImSDKPlugin } from "react-native-tim-js";

const getGroupHistoryMessageList = async () => {
  const groupID = "";
  const count = 20;
  const lastMsgID = "";
  const res = await TencentImSDKPlugin.v2TIMManager
    .getMessageManager()
    .getGroupHistoryMessageList(groupID, count, lastMsgID);
  const msgList = res.data ?? [];
  // here you can use msgList to render your message list
};
```

##### Listening for the persistent connection to get new messages in real time

After the historical message list is initialized, new messages are from the persistent connection `V2TimAdvancedMsgListener.onRecvNewMessage`.

After the `onRecvNewMessage` callback is triggered, you can add new messages to the historical message list as needed.

Sample code for binding a listener:

```javascript
import { TencentImSDKPlugin } from "react-native-tim-js";

const adVancesMsgListener = {
  onRecvNewMessage: (newMsg) => {
    _onReceiveNewMsg(newMsg);
    /// ... other listeners related to message
  },
};

const addAdvancedMsgListener = () => {
  TencentImSDKPlugin.v2TIMManager
    .getMessageManager()
    .addAdvancedMsgListener(adVancesMsgListener);
};
```

At this point, you have completed the Chat module development, and now users can send and receive messages and enter different conversations.
You can develop more features, such as group, user profile, relationship chain, offline push, and local search. For detailed directions, see [here](https://comm.qq.com/im/doc/RN/zh/).

## FAQs

#### What should I do if `Undefined symbols for architecture x86_64 [duplicate]` is reported during demo running?

See [here](https://stackoverflow.com/questions/71933392/react-native-ios-undefined-symbols-for-architecture-x86-64).

#### What should I do if `Failed to resolve: react-native-0.71.0-rc.0-debug` is reported during demo running?

See [here](https://blog.csdn.net/weixin_44132277/article/details/127731985).
