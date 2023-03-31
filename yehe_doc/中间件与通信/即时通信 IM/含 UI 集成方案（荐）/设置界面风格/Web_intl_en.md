This document describes how to set the UI styles for web. 
## Setting the Conversation List UI Styles
 TUIConversation provides the conversation list feature. The conversation list consists mainly of the conversation list area, which provides UI styles that can be modified.


### Setting the conversation list style

After a user logs in, TUIKit reads the user's conversation list from the SDK based on the user's username. You can customize common features for the conversation list. For example, you can configure the profile photo style, background, font size, click event, and long press event for the conversation list.
You can configure the display of list items for the conversation list in `src/TUIKit/TUIComponents/container/TUIConversation/components/list-item/index.vue`.
Sample code:
<dx-codeblock>
:::  html
<!-- Display of the list items of single conversations on the conversation list -->
<li ref="content">
	<div class="TUI-conversation-item">
		<aside class="left">
			<!-- Profile photo -->
			<img class="avatar" :src="handleConversation?.avator(conversation)">
			<!-- Unread count/Badge -->
			<span class="num" v-if="conversation.unreadCount>0 && conversation.messageRemindType !== 'AcceptNotNotify'">
				{{conversation.unreadCount > 99 ? '99+' : conversation.unreadCount}}
			</span>
			<span class="num-notify" v-if="conversation.unreadCount>0 && conversation.messageRemindType === 'AcceptNotNotify'"></span>
		</aside>
		<div class="content">
			<div class="content-header">
				<!-- Conversation name -->
				<label>
					<p class="name">{{handleConversation?.name(conversation)}}</p>
				</label>
				<!-- Display the conversation's latest message/@ tip -->
				<div class="middle-box">
					<span class="middle-box-at"  v-if="conversation.type === 'GROUP' && conversation.groupAtInfoList.length > 0">{{handleConversation?.showAt(conversation)}}</span>
					<p>{{handleConversation?.showMessage(conversation)}}</p>
				</div>
			</div>
			<div class="content-footer">
				<!-- Time of the conversation's latest message -->
				<span class="time">{{handleConversation?.time(conversation.lastMessage.lastTime)}}</span>
				<!-- Whether to set Mute Notifications for the conversation -->
				<img v-if="conversation.messageRemindType === 'AcceptNotNotify'" class="mute-icon" src="../../../../assets/icon/mute.svg">
				<i></i>
			</div>
		</div>
	</div>
	<!-- Conversation menu bar -->
	<div class="dialog dialog-item"  v-if="toggle" ref="dialog">...</div>
</li>
:::
</dx-codeblock>
You can set the list item styles for the conversation list in `src/TUIKit/TUIComponents/container/TUIConversation/components/list-item/style/web.scss`.
The following sample code shows how to set the profile photo style for the conversation list:
<dx-codeblock>
:::  scss
.TUI-conversation {
	&-item {
		.left {
			.avatar {
				width: 30px;// Set the profile photo width
				height: 30px;// Set the profile photo height
				border-radius: 5px;// Set rounded corners for the profile photo
			}
		}
	}
}
:::
</dx-codeblock>

## Setting the Chat UI Styles
TUIChat provides the chat UI. The chat UI includes three areas: title bar area, message area, and input area. 

The chat UI can be configured in the `src/TUIKit/TUIComponents/container/TUIChat/index.vue` file.

### Setting the title bar area style
The title bar consists of two areas (left and right), as shown in the figure below: 
<img src="https://qcloudimg.tencent-cloud.cn/raw/5d319461a85c2b4283b83ae58742ef00.png" style="zoom:30%;"/> 
Code related to the title bar of the chat UI is in the `src/TUIKit/TUIComponents/container/TUIChat/index.vue` file. You can custom some common features for the title bar area of the chat UI, such as the background, font size, button icon, click event, and feature switch.
Sample code:
<dx-codeblock>
:::  html
<header class="TUIChat-header">
	<!-- Chat UI name/"Typing..." status prompt -->
	<typing-header
		:needTyping="needTyping"// "Typing..." status prompt switch. To disable the prompt, pass in `false`.
		...
	/>
	<!-- Group chat settings (only for the group chat UI) -->
	<aside class="setting">
		<Manage v-if="conversation.groupProfile" :conversation="conversation" :userInfo="userInfo" :isH5="env.isH5" />
	</aside>
</header>
:::
</dx-codeblock>
You can set the title bar area style for the chat UI in the `src/TUIKit/TUIComponents/container/TUIChat/style/web.scss` file.
The following code sample shows how to set the font size and background color for the title bar area of the chat UI:
<dx-codeblock>
:::  scss
.TUIChat {
	&-header {
		background-color: #147AFF;// Set the background color for the title bar area of the chat UI
		h1 {
			font-size: 16px;// Set the font size for the title bar area of the chat UI
		}
	}
}
:::
</dx-codeblock>

### Setting the message area style

#### Setting the chat UI background
You can customize the background color or image for the chat UI in the `src/TUIKit/TUIComponents/container/TUIChat/style/web.scss` file.
The following code sample shows how to set the background color for the message area in the chat UI:
<dx-codeblock>
:::  scss
.TUI-message-list {
	background-color: #006EFF;// Set the background color of the message area in the chat UI
}
:::
</dx-codeblock>
The following code sample shows how to set the background image for the message area in the chat UI:
<dx-codeblock>
:::  scss
.TUI-message-list {
	// Set the background image for the message area in the chat UI
	background-image: url(https://qcloudimg.tencent-cloud.cn/raw/176cddbfb778a4bb26a5d423056efe1d.png); 
}
:::
</dx-codeblock>

#### Setting the sender's profile photo style
Profile photo related code for the message area is in the `src/TUIKit/TUIComponents/container/TUIChat/components/message-bubble.vue`. If you do not set a profile photo, the default profile photo is displayed. You can customize the default profile photo and the shape (whether to use rounded corners) and size of the profile photo.
The following code sample shows how to set the default profile photo:
<dx-codeblock>
:::  html
<!-- Set the default profile photo path to `https://web.sdk.qcloud.com/component/TUIKit/assets/avatar_21.png`  -->
<img
	class="avatar"
	:src="message?.avatar || 'https://web.sdk.qcloud.com/component/TUIKit/assets/avatar_21.png'"
	onerror="this.src='https://web.sdk.qcloud.com/component/TUIKit/assets/avatar_21.png'"
/>
:::
</dx-codeblock>
The following code sample shows how to set the profile photo shape and size:
<dx-codeblock>
:::  scss
.avatar {
	width: 36px;// Set the profile photo width
	height: 36px;// Set the profile photo height
	border-radius: 5px; // Set rounded corners for the profile photo
}
:::
</dx-codeblock>

#### Setting bubble background colors
In the message area, each message consists of three parts: `avatar` (profile photo), `messageArea` (content area), and `messageLabel` (label area). The detailed structure is as follows: 
<img src="https://qcloudimg.tencent-cloud.cn/raw/ca91179dcfec41166e0960d1991cc94f.png" style="zoom:30%;"/> 
In the message area of the chat window, the receiver's bubbles are on the left and your own bubbles are on the right. You can customize the bubble background for both parties in the `src/TUIKit/TUIComponents/container/TUIChat/components/message-bubble.vue` file.
The following sample code shows how to set message bubble colors:
<dx-codeblock>
:::  scss
.message-area {
	.content {
		&-in {
			background: #fbfbfb;// Set the color for the recipient's bubbles on the left
			border-radius: 0px 10px 10px 10px;
		}
		&-out {
			background: #dceafd;// Set the color for your own bubbles on the right
			border-radius: 10px 0px 10px 10px;
		}
	}
}
:::
</dx-codeblock>

#### Setting the sender's nickname style
You can customize the sender's nickname style, including the font size and color in the `src/TUIKit/TUIComponents/container/TUIChat/components/message-bubble.vue` file.
The following sample code shows how to set the sender's nickname style:
<dx-codeblock>
:::  scss
.message-area {
	.name {
		font-weight: 400;// Set the sender's nickname font weight
		font-size: 0.8rem; // Set the sender's nickname font size
		color: #999999;// Set the sender's nickname font color
	}
}
:::
</dx-codeblock>

#### Setting the chat content style
You can customize the chat content style, including the font size, font color, and emoji size for both parties in the `src/TUIKit/TUIComponents/container/TUIChat/components/message-text.vue` file.
The following code sample shows how to set the chat content style:
<dx-codeblock>
:::  scss
.text-img {
	width: 20px;// Set the emoji width in chat content
	height: 20px;// Set the emoji height in chat content
}
.text-box {
	white-space: pre-wrap;
	font-size: 14px;// Set the font size in chat content
	color: #999999;// Set the font color in chat content
}
:::
</dx-codeblock>

#### Setting the tips message style
You can customize the tips message style, including the background, font size, and font color in the `src/TUIKit/TUIComponents/container/TUIChat/components/message-tip.vue` file.
Sample code:
<dx-codeblock>
:::  scss
.message-tip {
	margin: 0 auto;
	color: #999999;// Set the tips message font color
	font-size: 14px;// Set the tips message font size
	background: red;// Set the tips message background color
}
:::
</dx-codeblock>


### Setting the input area InputView
The input area provides various features, including the input of text and emojis and the sending of images, videos, files, ratings, and commonly used expressions. 


#### Hiding unnecessary features
You can customize to hide features, such as image, file, and rating sending, of the feature module of the input area.
This feature module loads features by getting the feature module registered in the `src/TUIKit/TUIComponents/container/TUIChat/index.ts` file of sendComponents. You can delete unwanted features from the file.
Sample code:
<dx-codeblock>
:::  ts
let sendComponents: any = {
	Face,// Emoji sending feature
	Image,// Image sending feature
	Video,// Video sending feature
	File,// File sending feature
	Evaluate,// Rating sending feature
	Words,// Commonly used expression sending feature
};
:::
</dx-codeblock>
