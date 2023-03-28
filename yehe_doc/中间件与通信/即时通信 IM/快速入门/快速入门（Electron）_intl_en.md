This document describes how to quickly run the Tencent Cloud Chat demo for Electron and integrate the Electron SDK.

## Environment Requirements

| Platform     | Version                |
| -------- | ------------------- |
| Electron | v13.1.5 or later |
| Node.js | v14.2.0 |

## Supported Platforms

Currently, both macOS and Windows platforms are supported.

## Trying Out Demo

Before integration, you can try out our [demo](https://intl.cloud.tencent.com/document/product/1047/34279) to quickly understand the capabilities of the Tencent Cloud Chat SDK for Electron.

## Prerequisites

You have [signed up](https://intl.cloud.tencent.com/document/product/378/17985) for a Tencent Cloud account and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions

[](id:step1)

### Step 1. Create an app

1. Log in to the [Chat console](https://console.cloud.tencent.com/im).
  >? If you already have an app, record its SDKAppID and [obtain key information](#step2).
  >A Tencent Cloud account can create a maximum of 300 Chat apps. If you want to create a new app, [disable and delete](https://intl.cloud.tencent.com/document/product/1047/34540) an unwanted app first. **Once an app (along with its SDKAppID) is deleted, the service it provides and all its data are lost. Proceed with caution**.
2. Click **Create Application**, enter your app name, and click **Confirm**.
    ![](https://main.qcloudimg.com/raw/15e61a874a0640d517eeb67e922a14bc.png)
3. After creation, you can see the status, service version, SDKAppID, tag, creation time, and expiry time of the new app on the overview page of the console. Record the SDKAppID.
   ![](https://main.qcloudimg.com/raw/7954cc2882d050f68cd5d1df2ee776a6.png)
4. Click the created app. In the left sidebar, click **Auxiliary Tools** > **UserSig Tools** to create a UserID and the corresponding UserSig. Then copy the UserSig for future login.
    ![](https://main.qcloudimg.com/raw/2286644d987d24caf565142ae30c4392.png)

[](id:step2)

### Step 2. Select an appropriate method to integrate the Electron SDK

Tencent Cloud Chat offers two integration schemes:

| Integration Scheme  | Applicable Scenario                                                                                                                                                                |
| --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Using a demo | The Chat demo includes all chat features and provides open-source code. If you need to implement chat scenarios, you can use the demo for secondary development. Try it out [here](https://intl.cloud.tencent.com/document/product/1047/34279). |
| Self implementation    | Implement Chat on your own if the demo does not meet your UI requirements.                                                                                                                |

To help you better understand Chat SDK APIs, sample APIs are provided [here](https://comm.qq.com/im/doc/electron/zh/).

[](id:step3)

### Step 3. Use the demo

1. Clone the source code of the Chat Electron demo to the local system.
  ```javascript
  git clone https://github.com/TencentCloud/tc-chat-demo-electron.git
  ```
2. Install project dependencies.
  ```javascript
  // Root directory of the project
  npm install

  // Rendering process directory
  cd src/client
  npm install
  ```
3. Run the project.
```javascript
// Root directory of the project
npm start
```
4. Build the project.
  ```javascript
  // Build the project in macOS
  npm run build:mac
  // Build the project in Windows
  npm run build:windows
  ```

>? In the demo, the main process directory `src/app/main.js`, and the rendering process directory is `src/client`. If any problem occurs during running, see the FAQs for troubleshooting first.

[](id:step4)

### Step 4. Self implementation

**Installing the Electron SDK**
Install the latest version of the Electron SDK as follows.
Run the following command:

```
npm install im_electron_sdk
```

** Initializing the SDK**

1. Pass in your `sdkAppID` in `TimMain`.
```javascript
// Main process
const TimMain = require('im_electron_sdk/dist/main')

const sdkappid = 0;// You can apply for it in the Chat console.
const tim = new TimMain({
  sdkappid:sdkappid
})
```
2. Call `TIMInit` to initialize the SDK.
```javascript
// Rendering process
const TimRender = require('im_electron_sdk/dist/render')
const timRender = new TimRender();
// Initialize the component
timRender.TIMInit()
```
3. Log in as a test user.
Log in with the test account initially generated in the console for login verification.
Call the `timRender.TIMLogin` method to log in as the test user.
If the returned `code` is `0`, the login is successful.
```javascript
const TimRender = require('im_electron_sdk/dist/render')
const timRender = new TimRender();
let {code} = await timRender.TIMLogin({
  userID:"userID",
  userSig:"userSig" // See how to generate a userSig
})
```

>? This account is for development and testing only. Before the application is launched, the correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).

**Sending a message**
The following sample shows how to send a text message. If the returned `code` is `0`, the message is sent successfully.
Sample code:

```javascript
const TimRender = require('im_electron_sdk/dist/render')
const timRender = new TimRender();
let param:MsgSendMessageParamsV2 = {    // param of TIMMsgSendMessage
    conv_id: "conv_id",
    conv_type: 1,
    params: {
        message_elem_array: [{
            elem_type: 1,
            text_elem_content:'Hello Tencent!',

        }],
        message_sender: "senderID",
    },
    callback: (data) => {}
  }
let {code} = await timRender.TIMMsgSendMessageV2(param);
```

>? If sending the message fails, it may be that your `sdkAppID` does not support sending messages to strangers. In this case, you can [disable the friend relationship chain check](https://console.cloud.tencent.com/im/login-message) in the console for testing.

**Getting the conversation list**
Log in with the other test account to pull the conversation list.
Common use cases include:
Get the conversation list upon application start and listen for the persistent connection to update the conversation list in real time.

```javascript
let param:getConvList = {
            userData:userData,
        }
let data:commonResult<convInfo[]> = await timRenderInstance.TIMConvGetConvList(param)
```

At this point, you can see the message sent by the other test account in the previous step.

**Receiving a message**
Common use cases include:

1. After a new conversation is opened on the UI, request a certain number of historical messages at a time to display the historical message list.
2. Listen for the persistent connection to receive messages in real time and add them to the historical message list.

Requesting the historical message list at a time

```javascript
let param:MsgGetMsgListParams = {
        conv_id: conv_id,
        conv_type: conv_type,
        params: {
            msg_getmsglist_param_last_msg: msg,
            msg_getmsglist_param_count: 20,
            msg_getmsglist_param_is_remble: true,
        },
        user_data: user_data
    }
    let msgList:commonResult<Json_value_msg[]> = await timRenderInstance.TIMMsgGetMsgList(param);
```

Listening for new messages in real time
The following is the sample code for callback binding:

```javascript
let param : TIMRecvNewMsgCallbackParams = {
            callback: (...args)=>{},
            user_data: user_data
        }
timRenderInstance.TIMAddRecvNewMsgCallback(param);
```

At this point, you have completed the Chat module development, and now users can send and receive messages and enter different conversations.
You can develop more features, such as group, user profile, relationship chain, offline push, and local search.
For detailed directions, see [here](https://comm.qq.com/im/doc/electron/zh/Callback/readme.html).

## FAQs

#### What platforms are supported?

Currently, both macOS and Windows platforms are supported.

#### How do I query error codes?

For Chat SDK API error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).

#### What should I do if the error `npm ERR! gyp ERR! stack TypeError: Cannot assign to read only property 'cflags' of object '#<Object>'` is reported during development environment installation?

Downgrade the node version to 16.18.1.

#### What should I do if the error `gypgyp ERR!ERR` is reported during development environment installation?

See [gypgyp ERR!ERR! ](https://stackoverflow.com/questions/57879150/how-can-i-solve-error-gypgyp-errerr-find-vsfind-vs-msvs-version-not-set-from-c).

#### What should I do if the error `npm ERR! Fix the upstream dependency conflict, or retry` is reported when `npm install` is run?

In versions earlier than npm v7, dependency conflicts that occur during installation are automatically ignored.
In npmv7 or later versions, dependency conflicts will not be automatically ignored, and you need to manually enter a command to ignore them.
The command for ignoring dependency conflicts is as follows:
<dx-codeblock>
:::  sh
npm install --force
:::
</dx-codeblock>


#### What should I do if the error `Error: error:0308010C:digital envelope routines::unsupported` is reported when `npm run start` is run?

Downgrade the node version to 16.18.1.

#### What should I do if the screen turns white when I run `npm run start` on a macOS client demo?

The error occurs because the rendering process code is not completely built and the port 3000 opened by the main process points to an empty page. The error will be resolved after the rendering process code is completely built and you refresh the window. Alternatively, you can run `cd src/client && npm run dev:react` and `npm run dev:electron` to start the rendering process and main process separately.

#### How do I use native modules in projects built with vue-cli-plugin-electron-builder?

For issues related to using native modules in projects built with vue-cli-plugin-electron-builder, see [No native build was found for platform = xxx](https://github.com/nklayman/vue-cli-plugin-electron-builder/issues/1492).

#### How do I use native modules in projects built with webpack?

For issues related to using native modules in projects built with webpack, see [FAQs in the Windows environment](https://blog.csdn.net/Yoryky/article/details/106780254).

#### What should I do if the error "Dynamic Linking Error" is reported?

Dynamic Linking Error. electron-builder configuration

``` javascript
   extraFiles:[
    {
      "from": "./node_modules/im_electron_sdk/lib/",
      "to": "./Resources",
      "filter": [
        "**/*"
      ]
    }
  ]
```
