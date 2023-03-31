## TUIKit Overview
TUIKit is a UI component library based on Tencent Cloud IM SDK. It provides universal UI components to offer features such as conversation, chat, relationship chain, group, and audio/video call features.
With these UI components, you can quickly build your own business logic.
When implementing UI features, components in TUIKit will also call the corresponding APIs of the IM SDK to implement IM-related logic and data processing, allowing developers to focus on their own business needs or custom extensions.


## TUIKit Components
TUIKit provides the following modules for different purposes: TUIChat, TUIConversation, TUIProfile, and TUIManage modules. For details, see [the open source code here](https://github.com/TencentCloud/chat-uikit-react).
The TUIKit web UI effect is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/14ed827eecc218306abc82d46c57252d.png)


## TUIChat
TUIChat is responsible for message UI display. You can use it to directly send different types of messages, including text, emoji, image, video, and custom messages. TUIChat also supports message forward/recall/quote/query and message read receipts.
The TUIChat web UI effect is as follows:

<table style="text-align:center;vertical-align:middle;width:1000px">
  <tr>
	  <th style="text-align:center;" width="500px">Message UI/Message Quoting/Recalling/Forwarding<br></th>
    <th style="text-align:center;" width="500px">Message Navigation/Read Receipt<br></th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/b2ab2f7ed4efd5408258b35d521ad824.png"  />    </td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/f7509dada2d528877e699f104c041eb4.png" />     </td>
	 </tr>
</table>

## TUIConversation
TUIConversation is responsible for conversation list display and editing. It allows you to pin a conversation to the top, delete conversations, etc.
The TUIConversation web UI effect is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/287e9baa546282ddf8aa71c498847ae7.png)


## TUIManage
TUIManage displays conversation related information and allows you to pin a conversation to the top, delete a conversation, and perform group related operations.
The TUIManage web UI effect is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/455a7db0203f89b3319c11121607a708.png)

## TUIContact
TUIContact displays relationship chains and allows you to create conversations and more.
The TUIContact web UI effect is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/3e768928e923f8e04ef25bca71d85176.png)

## TUIProfile
TUIProfile is responsible for user profile management.
The TUIProfile web UI effect is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/7b870dc35e7b4b0625755228e2dd5d5c.png)
