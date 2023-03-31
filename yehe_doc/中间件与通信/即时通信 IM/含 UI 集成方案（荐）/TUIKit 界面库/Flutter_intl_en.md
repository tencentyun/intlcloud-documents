## TUIKit Overview

TUIKit is a UI component library based on Tencent Cloud IM SDK. It provides universal UI components to offer features such as conversation, chat, search, relationship chain, group, and audio/video call features.
With these UI components, you can quickly build your own business logic.
When implementing UI features, components in TUIKit will also call the corresponding APIs of the IM SDK to implement IM-related logic and data processing, allowing developers to focus on their own business needs or custom extensions.

## Supported Platforms

| Platform                                                     | Supported or Not             |
| ------------------------------------------------------------ | ---------------------------- |
| iOS                                                          | Supported                    |
| Android                                                      | Supported                    |
| [Web](#web)                                                  | Supported from version 0.1.5 |
| macOS                                                        | Will be supported soon       |
| Windows                                                      | Will be supported soon       |
| [Hybrid development](https://www.tencentcloud.com/document/product/1047/51456) (adding the SDK for Flutter to your existing native app) | Supported from version 1.0.0 |

>? A set of all-platform IM SDKs for Flutter and TUIKit are provided to help you build apps for different platforms by using one set of code.

## Demo[](id:demo)

You can quickly try out the features of TUIKit online through the demos.

**The following demos are all created by integrating TUIKit into the same Flutter project and packaging the build.**

<table style="text-align:center; vertical-align:middle; max-width: 800px">
  <tr>
    <th style="text-align:center;">Mobile app</th>
    <th style="text-align:center;">Web - HTML5</th>
  </tr>
  <tr>
    <td><div style="display: flex; justify-content: center; align-items: center; flex-direction: column; padding-top: 10px">Scan the QR code to download the app for iOS or Android<img style="max-width:200px; margin: 20px 0 20px 0" src="https://qcloudimg.tencent-cloud.cn/raw/ca2aaff551410c74fce48008c771b9f6.png"/></div></td>
    <td><div style="display: flex; justify-content: center; align-items: center; flex-direction: column; padding-top: 10px">Scan the QR code with your mobile phone to try out the online demo for web<img style="max-width:200px; margin: 20px 0 20px 0" src="https://qcloudimg.tencent-cloud.cn/raw/3c79e8bb16dd0eeab35e894a690e0444.png"/></div></td>
  </tr>
</table>

## TUIKit Components

TUIKit provides different UI components to implement different features and display different content. Details are as follows:

| Component                                                    | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [TIMUIKitConversation](#TIMUIKitConversation)                | Conversation list component                                  |
| [TIMUIKitChat](#TIMUIKitChat)                                | Core chat component                                          |
| [TIMUIKitAddFriend](#add) / [TIMUIKitAddGroup](#add)         | Friend adding component and group adding component           |
| [TIMUIKitBlackList](#contacts) / [TIMUIKitNewContact](#contacts) | Blocklist component and new contact request list component   |
| [TIMUIKitContact](#contacts) / [TIMUIKitGroup](#contacts)    | Contacts component and group list component                  |
| [TIMUIKitProfile](#TIMUIKitProfile) / [TIMUIKitGroupProfile](#TIMUIKitGroupProfile) | Contact profile component and group profile component        |
| [TIMUIKitSearch / TIMUIKitSearchMsgDetail](#search)          | Global search component and in-conversation search component |
| [Audio/Video call plugin](#calling)                          | Audio/Video calls for one-to-one or group chats              |
| [Message push plugin](#push)                                 | Vendor offline push and local online push                    |

The UI effect is as shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/b3d5bba6d133d3a0f3a4fa7534037f01.png" style="zoom:50%;"/>

<img src="https://qcloudimg.tencent-cloud.cn/raw/33d706da1fd69cbe92c7dd95357f9486.png" style="zoom:50%;"/>

### Key features of TIMUIKitChat[](id:TIMUIKitChat)

TIMUIKitChat is responsible for message UI display. You can use it to directly send different types of messages, reply with emojis, copy or quote messages, query message read receipt details, etc.
The UI effect is as shown below:
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="500px">Message UI</th>
    <th style="text-align:center;" width="500px">Sending Different Types of Messages</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/9efa78f5687481ab901863dfaeb144d4.png"/></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/bc1c20996f6618ee8fee3c55fe78535f.png"/></td>
  </tr>
</table>
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="300px">Emoji Reply/Copy/Quote</th>
    <th style="text-align:center;" width="300px">Automatic File Icon Matching</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/04c0e4192ca8d62bc6bc1e34b93813b7.png" /></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/c5ba69d29764269cab6262a0982bad97.png" /></td>
  </tr>
</table>
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="300px">Message Read Receipt</th>
    <th style="text-align:center;" width="300px">Message Read Receipt Details</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/e15f2913e6f04a9ff914bcf1a6fc6952.png" /></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/44277387d4df1861e11cc41654f5cf24.png" /></td>
  </tr>
</table>
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="300px">Group Tips</th>
    <th style="text-align:center;" width="300px">Group Joining Request Approval</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/d9895126af46a910586c600aadc475b6.png" /></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/42ba9e61d3cfc5795b17cc89e6b8c248.png" /></td>
  </tr>
</table>
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="300px">Link Parsing</th>
    <th style="text-align:center;" width="300px">Geographical Location Message</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/87a331a8f56326b53eebda543bc89250.png" /></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/d85fb829caf15ca55c63958e1dcb1247.png" /></td>
  </tr>
</table>


### Key features of relationship chain[](id:contacts)

Relationship chain components are responsible for displaying the information of contacts, group chats, and blocklist of the current user.
The UI effect is as shown below:

<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="500px">Contacts List (TIMUIKitContact)</th>
    <th style="text-align:center;" width="500px">New Contacts List (TIMUIKitNewContact)</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/a5b16c58dc6f07245d9c812ed73f0c06.png"/></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/cc507ea91ac78c57d7fedf34f804857a.png"/></td>
  </tr>
</table>
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="300px">List of Joined Group Chats (TIMUIKitGroup)</th>
    <th style="text-align:center;" width="300px">Blocklist (TIMUIKitBlackList)</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/331cc34016bc624819fd249577793e74.png" /></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/cc619a08dfe4da2307b8cb3086731e9c.png" /></td>
  </tr>
</table>


### Key features of TIMUIKitConversation[](id:TIMUIKitConversation)

TIMUIKitConversation is responsible for conversation list display and editing.
The UI effect is as shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/53880bb394b8b665fec6724f16d286ee.png" style="zoom:40%;"/>

### Key features of TIMUIKitProfile[](id:TIMUIKitProfile)

TIMUIKitProfile is responsible for contacts profile display and management.
The UI effect is as shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/338aa97bdc58f79fd49e5cfc1ed1c93c.png" style="zoom:40%;"/>

### Key features of `TIMUIKitAddFriend` and `TIMUIKitAddGroup`[](id:add)

TIMUIKitAddFriend is a friend adding component.
TIMUIKitAddGroup is a group adding component.
The UI effect is as shown below:
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="500px">Friend Adding Page (TIMUIKitAddFriend)</th>
    <th style="text-align:center;" width="500px">Group Joining Page (TIMUIKitAddGroup)</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/bb42196224b3bc2ec5fe69654622da34.png"/></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/5d3f91b40ee4226637f41215e6b625f1.png"/></td>
  </tr>
</table>


### Key features of TIMUIKitGroupProfile[](id:TIMUIKitGroupProfile)

TIMUIKitGroupProfile is responsible for the display and management of group profiles, members, and permissions.
The UI effect is as shown below:
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="500px">Group Profile and Management</th>
    <th style="text-align:center;" width="500px">Group Member Management</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/ae5e50eb857308403d802fed9cbffb83.png"/></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/a25514e0bab675b5f5e356604310bcb5.png"/></td>
  </tr>
</table>
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="300px">Group Joining Mode Management</th>
    <th style="text-align:center;" width="300px">Group Operation</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/78d9a2eae2b8f95226075b1f676f9984.png" /></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/197466803785eeb07297d68a68e2872a.png" /></td>
  </tr>
</table>


### Key features of local search[](id:search)

TIMUIKitSearch is responsible for local global search, including contacts, group chat, and chat record search.
TIMUIKitSearchMsgDetail is responsible for searching for chat records in a conversation.
For details, see [here](https://intl.cloud.tencent.com/document/product/1047/50036). The UI effect is as follows:
<img src="https://qcloudimg.tencent-cloud.cn/raw/35a45f8176005b46e67020e5d9656d0a.png" style="zoom:40%;"/>

### Key features of audio/video call[](id:calling)

<img src="https://qcloudimg.tencent-cloud.cn/raw/78c9aa0717517f9e2c245dba1267771e.png" style="zoom:40%;"/>
One-to-one video call UIs:
<img src="https://qcloudimg.tencent-cloud.cn/raw/e4a376e5d6895059214ccc7412cc6be2.jpg" style="zoom:60%;"/>
Group chat audio/video call UIs:
<img src="https://qcloudimg.tencent-cloud.cn/raw/f00f69d432ce4599b7be643dbf410370.png" style="zoom:40%;"/>

You can initiate audio/video calls via the TIMUIKitChat message page and TIMUIKitProfile individual profile page.
The UI effect is as shown below:
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="300px">Initiating a Call via a Message Page</th>
    <th style="text-align:center;" width="300px">Initiating a Call via a Profile Page</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/fab20b828cf3cb8417d169e890b1b0c6.png" /></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/b1ba063e4ee5bee45c168c799c800a7b.png" /></td>
  </tr>
</table>


### Key features of message push[](id:push)

You can use Tencent's [Flutter push plugin](https://intl.cloud.tencent.com/document/product/1047/50032) to integrate message push capabilities, including offline and online push capabilities.
The message push effect is as shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/9634f4ffa77a91c8c95c73091abb38ae.png" style="zoom:40%;"/>

[](id:feedback)
