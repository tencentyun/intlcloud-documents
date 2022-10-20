## TUIKit Overview
TUIKit is a UI component library based on Tencent Cloud IM SDK. It provides universal UI components to offer features such as conversation, chat, search, relationship chain, group, and audio/video call features.
With these UI components, you can quickly build your own business logic.
When implementing UI features, components in TUIKit will also call the corresponding APIs of the IM SDK to implement IM-related logic and data processing, allowing developers to focus on their own business needs or custom extensions.


## TUIKit Components
TUIKit provides the following UI components: TUISearch, TUIConversation, TUIChat, TUICallKit, TUIContact, TUIGroup, and TUIOfflinePush. Each of these components is responsible for displaying different content.
The UI effect is as shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/62aef6cf20aea982b17970c11b391122.png" style="zoom:50%;"/>

### TUIChat
TUIChat is responsible for message UI display. You can use it to directly send different types of messages, long press on a message to like/reply to/quote messages, query message read receipt details, etc.
The UI effect is as shown below:
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="500px">Message UI</th>
    <th style="text-align:center;" width="500px">Sending different types of messages</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/1ac02de0a788fe0d1f0d20493fbfd081.png"/></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/512d34e2e5bdf256129b6207e46e79e1.png"/></td>
	 </tr>
</table>
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="300px">Message Liking/Reply/Quoting</th>
    <th style="text-align:center;" width="300px">Message Reply Details</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/f87f569a7b90164d3ab44ed16089d8cd.png" /></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/6d011c026f7b4d58413032da2e18b090.png" /></td>
	 </tr>
</table>
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="300px">Message Read Receipt</th>
    <th style="text-align:center;" width="300px">Message Read Receipt Details</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/223da735715f8d1563ff2dab2a9c19fe.png" /></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/b18dd054ac62d844ccbda50c1a7e0e9b.png" /></td>
	 </tr>
</table>

### TUIContact
TUIContact is responsible for contacts display and permission setting.
The UI effect is as shown below:
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="500px">Relationship Chain List</th>
    <th style="text-align:center;" width="500px">Contact Profiles and Management</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/518ead4ac8414e54cf29993acfc2835a.png"/></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/16965a64aab5e9987ac6e002fa479830.png"/></td>
	 </tr>
</table>
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="300px">List of Joined Group Chats</th>
    <th style="text-align:center;" width="300px">Blocklist</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/6f8d0873f28ae18673106edfac334366.png" /></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/0c1cf41c8924a72221299d938952ef38.png" /></td>
	 </tr>
</table>


### TUIConversation
TUIConversation is responsible for conversation list display and editing.
The UI effect is as shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/abc6168077ee5f91d109f62617ea8eee.png" style="zoom:40%;"/>


### TUIGroup
TUIGroup is responsible for managing group profiles, group members, and group permissions.
The UI effect is as shown below:
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="500px">Group Profile and Management</th>
    <th style="text-align:center;" width="500px">Group Member Management</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/fb9c2ff73c31ecb349926b22ba0e4ac2.png"/></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/ca958eb233e5ede07b03a81b25ee9975.png"/></td>
	 </tr>
</table>
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="300px">Group Joining Mode Management</th>
    <th style="text-align:center;" width="300px">Permission Management</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/dc3f86d8140d9c40de674f6b5bc820db.png" /></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/dd2bb957639ea1606f15f4c73420bb5c.png" /></td>
	 </tr>
</table>


### TUISearch
TUISearch is responsible for local search, including contacts, group chat, and chat record search.
The UI effect is as shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/b3e2916137e1e7670b71fe09e638d395.png" style="zoom:40%;"/>


### TUICallKit
TUICallKit is responsible for audio or video calls.
The one-to-one chat UI is as shown below:
<table style="text-align:center;vertical-align:middle;width:1000px">
  <tr>
    <th style="text-align:center;" width="500px">Video Call<br></th>
    <th style="text-align:center;" width="500px">Audio Call<br></th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/b412c178178c0052254f4f800559d7d4.png"  />    </td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/6b2b6878e714e77e578e3c962659e36b.jpg" />     </td>
	 </tr>
</table>

The group chat UI is as shown below:
<table style="text-align:center;vertical-align:middle;width:1000px">
  <tr>
    <th style="text-align:center;" width="500px">Video Call<br></th>
    <th style="text-align:center;" width="500px">Audio Call<br></th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/5ca955c288c0c45b74e4fcfcb0ec6ebb.png"  />    </td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/068a66d2a99a910d516e645ffb06a23a.png" />     </td>
	 </tr>
</table>

If you have integrated TUIChat, TUIContact, and TUICallKit, you can initiate an audio or video call via a TUIChat message page or TUIContact individual profile page.
The UI effect is as shown below:
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="500px">Initiating a Call via a Message Page</th>
    <th style="text-align:center;" width="500px">Initiating a Call via a Profile Page</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/b7b6aca5e1f3f3e5d775cfa3316e30f4.png" /></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/31fd1d8fb263e953825cf5531a24ffca.png" /></td>
	 </tr>
</table>


### TUIOfflinePush
TUIOfflinePush is responsible for displaying messages pushed offline.
The offline push effect is as shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/c13da6a373df9fe35a963736cdfe4e7d.png" style="zoom:40%;"/>

[](id:feedback)

