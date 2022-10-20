## TUIKit Overview
TUIKit is a UI component library based on Tencent Cloud IM SDK. It provides universal UI components to offer features such as conversation, chat, search, relationship chain, group, and audio/video call features.
With these UI components, you can quickly build your own business logic.
When implementing UI features, components in TUIKit will also call the corresponding APIs of the IM SDK to implement IM-related logic and data processing, allowing developers to focus on their own business needs or custom extensions.


## TUIKit Components
TUIKit provides different UI components to implement different features and display different content. Details are as follows:

| Component               | Description           |
| -------------------- | ------------------ |
| TIMUIKitConversation | Conversation list component       |
| TIMUIKitChat         | Chat component           |
| TIMUIKitAddFriend    | Friend adding component       |
| TIMUIKitAddGroup     | Group adding component       |
| TIMUIKitBlackList    | Blocklist component     |
| TIMUIKitContact      | Contacts component       |
| TIMUIKitGroup        | Group list component       |
| TIMUIKitGroupProfile | Group information component       |
| TIMUIKitNewContact   | New contacts list component |
| TIMUIKitProfile      | User information component       |
| TIMUIKitSearch / TIMUIKitSearchMsgDetail      | Global search/In-conversation search component           |


The UI effect is as shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/29ae8ebd00b201bcf60f031c7dc763a8.png" style="zoom:50%;"/>

<img src="https://qcloudimg.tencent-cloud.cn/raw/51e1a447ea02808f6b6fdea8bd8824d1.png" style="zoom:50%;"/>

### TIMUIKitChat
TIMUIKitChat is responsible for message UI display. You can use it to directly send different types of messages, reply with emojis, copy or quote messages, query message read receipt details, etc.
The UI effect is as shown below:
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="500px">Message UI</th>
    <th style="text-align:center;" width="500px">Sending different types of messages</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/c64b7ca7083f6858c6bb67f27fafce66.png"/></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/8b3d14018072db74145ce4bc24b91e89.png"/></td>
	 </tr>
</table>
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="300px">Emoji Reply/Copy/Quote</th>
    <th style="text-align:center;" width="300px">Automatic File Icon Matching</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/9728707f05092a8ef8945b9b611a1fb9.png" /></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/1d9f794578306b39e39a8fee3647a57b.png" /></td>
	 </tr>
</table>
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="300px">Message Read Receipt</th>
    <th style="text-align:center;" width="300px">Message Read Receipt Details</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/91de492b091ed713f3249f31f9bd502b.png" /></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/4fe4d1d57c9ba945d19a6993c290016f.png" /></td>
	 </tr>
</table>
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="300px">Group Tips</th>
    <th style="text-align:center;" width="300px">Group Joining Request Approval</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/280aacf5b254fe263ec47cc712435c8e.png" /></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/26d87e8f2e54cac8de224735a39e6158.png" /></td>
	 </tr>
</table>
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="300px">Link Parsing</th>
    <th style="text-align:center;" width="300px">Geographical Location Message</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/6f9b523937e482c7aa86d30f02cd1739.png" /></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/b012b5a54c59748cb964782e37340495.png" /></td>
	 </tr>
</table>

### Relationship chain components
Relationship chain components are responsible for displaying the information of contacts, group chats, and blocklist of the current user.
The UI effect is as shown below:
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="500px">Contacts List (TIMUIKitContact)</th>
    <th style="text-align:center;" width="500px">New Contacts List (TIMUIKitNewContact)</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/aed62aba0272da2900a5db8c9c0fcc8f.png"/></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/ed169aaccead28dfa2fc6ef6192b64f3.png"/></td>
	 </tr>
</table>
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="300px">List of Joined Group Chats (TIMUIKitGroup)</th>
    <th style="text-align:center;" width="300px">Blocklist (TIMUIKitBlackList)</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/c6bc53492ba9c620680396e687bda3a9.png" /></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/5eaaa4aa89d5c7a549813b1b3ab054b5.png" /></td>
	 </tr>
</table>


### TIMUIKitConversation
TIMUIKitConversation is responsible for conversation list display and editing.
The UI effect is as shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/214007feb3be18519c4ad3947ef0e266.png" style="zoom:40%;"/>

### TIMUIKitProfile
TIMUIKitProfile is responsible for contacts profile display and management.
The UI effect is as shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/e3831ff35e1571c8dbd6b26517cac819.png" style="zoom:40%;"/>

### User adding and user group joining
TIMUIKitAddFriend is a friend adding component.
TIMUIKitAddGroup is a group adding component.
The UI effect is as shown below:
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="500px">Friend Adding Page (TIMUIKitAddFriend)</th>
    <th style="text-align:center;" width="500px">Group Joining Page (TIMUIKitAddGroup)</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/cf0eaf557c607a139d8c4afd7da8bb21.png"/></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/398e1fa730ffe17acdaffaa252c3de3c.png"/></td>
	 </tr>
</table>

### TIMUIKitGroupProfile
TIMUIKitGroupProfile is responsible for the display and management of group profiles, members, and permissions.
The UI effect is as shown below:
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="500px">Group Profile and Management</th>
    <th style="text-align:center;" width="500px">Group Member Management</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/3424c3e391c321bf607fcd807ef70afe.png"/></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/e35200ce0b9653a98205ad135caa2b45.png"/></td>
	 </tr>
</table>
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="300px">Group Joining Mode Management</th>
    <th style="text-align:center;" width="300px">Group Operation</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/2af746e239e4f43d142dc634a114a680.png" /></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/d39a4b2c84e3b62bcd1a770cf26dc209.png" /></td>
	 </tr>
</table>


### Local search
TIMUIKitSearch is responsible for local global search, including contacts, group chat, and chat record search.
TIMUIKitSearchMsgDetail is responsible for searching for chat records in a conversation.
For details, see [here](https://intl.cloud.tencent.com/document/product/1047/50036). The UI effect is as follows:
<img src="https://qcloudimg.tencent-cloud.cn/raw/199a69d9da6126690a34c7bb01552081.png" style="zoom:40%;"/>


### Audio/Video call
[The TUICalling plugin](https://intl.cloud.tencent.com/document/product/1047/50023) is responsible for audio/video calls.
One-to-one audio call UIs:
<img src="https://qcloudimg.tencent-cloud.cn/raw/1ee168e84c31bcac54e1d5ffb98b4491.png" style="zoom:40%;"/>
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
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/a54e097733331db4593589959ab52a82.png" /></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/4f9ecb8c9c585271e1c9a527876e6efc.png" /></td>
	 </tr>
</table>


### Message push
You can use Tencent's [Flutter push plugin](https://intl.cloud.tencent.com/document/product/1047/50032) to integrate message push capabilities, including offline and online push capabilities.
The message push effect is as shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/b2717640d161ea0cea66d509311dc6a7.png" style="zoom:40%;"/>

[](id:feedback)


