## TUIKit Overview
TUIKit is a UI component library based on Tencent Cloud IM SDK. It provides universal UI components to offer features such as conversation, chat, search, relationship chain, group, and audio/video call features.
With these UI components, you can quickly build your own business logic.
When implementing UI features, components in TUIKit will also call the corresponding APIs of the IM SDK to implement IM-related logic and data processing, allowing developers to focus on their own business needs or custom extensions.
Starting from version 6.9.3557, TUIKit provides a new set of minimalist version UI components. The previous version UI components are still retained, which are called the classic version UI components. You can choose either the classic or minimalist version as needed.

## TUIKit Components
TUIKit provides the following UI components: TUISearch, TUIConversation, TUIChat, TUICallKit, TUIContact, TUIGroup, and TUIOfflinePush. Each of these components is responsible for displaying different content.
The UI effect is as shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/9c893f1a9c6368c82d44586907d5293d.png" style="zoom:50%;"/>

### TUIChat
TUIChat is responsible for message UI display. You can use it to directly send different types of messages, long press on a message to like/reply to/quote messages, query message read receipt details, etc.
The UI effect is as shown below:

<table style="text-align:center; vertical-align:middle; width:600px">
  <tr>
    <th style="text-align:center;" width="600px">Message UI | Sending Multiple Types of Messages</th>
  </tr>
  <tr>
    <td><img style="width:600px" src="https://qcloudimg.tencent-cloud.cn/raw/5684d3acaf42b95cc942dad24980e129.png"/></td>
	 </tr>
</table>
<table style="text-align:center; vertical-align:middle; width:600px">
  <tr>
    <th style="text-align:center;" width="600px">Message Liking | Reply  </th>
  </tr>
  <tr>
    <td><img style="width:600px" src="https://qcloudimg.tencent-cloud.cn/raw/f457d0855163c13c1e12a06b13e54e3e.png" /></td>
	 </tr>
</table>
<table style="text-align:center; vertical-align:middle; width:600px">
  <tr>
    <th style="text-align:center;" width="600px">Message Read Receipt | Read Receipt Details</th>
  </tr>
  <tr>
    <td><img style="width:600px" src="https://qcloudimg.tencent-cloud.cn/raw/00e2ed68b44bd9406732674eeb3164f9.png" /></td>
	 </tr>
</table>


### TUIContact
TUIContact is responsible for contacts display and permission setting.
The UI effect is as shown below:

<table style="text-align:center; vertical-align:middle; width:600px">
  <tr>
    <th style="text-align:center;" width="600px">Relationship Chain List | Contact Profiles and Management</th>
  </tr>
  <tr>
    <td><img style="width:600px" src="https://qcloudimg.tencent-cloud.cn/raw/fde8afab364cef589ffe9f059aede058.png"/></td>
	 </tr>
</table>
<table style="text-align:center; vertical-align:middle; width:600px">
  <tr>
    <th style="text-align:center;" width="600px">List of Joined Group Chats | Blocklist</th>
  </tr>
  <tr>
    <td><img style="width:600px" src="https://qcloudimg.tencent-cloud.cn/raw/140f2dd618e8eb26a434277cbdac7fe3.png" /></td>
	 </tr>
</table>



### TUIConversation
TUIConversation is responsible for conversation list display and editing.
The UI effect is as shown below:

<img src="https://qcloudimg.tencent-cloud.cn/raw/f421db60d6a85bb948217ffdfc7836a9.png" style="zoom:40%;"/>


### TUIGroup
TUIGroup is responsible for managing group profiles, group members, and group permissions.
The UI effect is as shown below:

<table style="text-align:center; vertical-align:middle; width:600px">
  <tr>
    <th style="text-align:center;" width="600px">Group Profile and Management | Group Member Management</th>
  </tr>
  <tr>
    <td><img style="width:600px" src="https://qcloudimg.tencent-cloud.cn/raw/88b77b431ac007a0c9a5f913c0e73a0c.png"/></td>
	 </tr>
</table>
<table style="text-align:center; vertical-align:middle; width:600px">
  <tr>
    <th style="text-align:center;" width="600px">Group Joining Mode Management | Permission Management</th>
  </tr>
  <tr>
    <td><img style="width:600px" src="https://qcloudimg.tencent-cloud.cn/raw/24afe0858bfda4fca3e11626341a1954.png" /></td>
	 </tr>
</table>

### TUISearch
TUISearch is responsible for local search, including contacts, group chat, and chat record search.
The UI effect is as shown below:


<img src="https://qcloudimg.tencent-cloud.cn/raw/0c70b9d8abbb494a51d152438e195fbf.png" style="zoom:40%;"/>

### TUICallKit
TUICallKit is responsible for audio or video calls.
The one-to-one chat UI is as shown below:

<table style="text-align:center;vertical-align:middle;width:600px">
  <tr>
    <th style="text-align:center;" width="500px">Video Call<br></th>
    <th style="text-align:center;" width="500px">Audio Call<br></th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/44d4c8a412752abda898341665a90016.png"  />    </td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/5eb84936666da81b0331a28c3c779b77.png" />     </td>
	 </tr>
</table>


The group chat UI is as shown below:
<table style="text-align:center;vertical-align:middle;width:600px">
  <tr>
    <th style="text-align:center;" width="500px">Video Call<br></th>
    <th style="text-align:center;" width="500px">Audio Call<br></th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/83d6cd991cd0e9251caafebe75e46f12.png"  />    </td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/842c563a9dd99da4950402e7a61836dd.png" />     </td>
	 </tr>
</table>


If you have integrated TUIChat, TUIContact, and TUICallKit, you can initiate an audio or video call via a TUIChat message page or TUIContact individual profile page.
The UI effect is as shown below:


<table style="text-align:center; vertical-align:middle; width:600px">
  <tr>
    <th style="text-align:center;" width="600px">Initiating a Call via a Message Page | Initiating a Call via a Profile Page</th>
  </tr>
  <tr>
    <td><img style="width:600px" src="https://qcloudimg.tencent-cloud.cn/raw/0302a0a9eed1c58ef14f05d3f17d96c4.png" /></td>
	 </tr>
</table>


### TUIOfflinePush
TUIOfflinePush is responsible for displaying messages pushed offline.
The offline push effect is as shown below:
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/CFL3713_TUIofflinepush.png" style="zoom:90%;"/>

[](id:feedback)
