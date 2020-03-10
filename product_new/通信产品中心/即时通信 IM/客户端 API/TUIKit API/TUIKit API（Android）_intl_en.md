## ConversationLayout

ConversationLayout consists of TitleBarLayout and ConversationListLayout. Each component provides UI styles and event registration APIs for customization.

| API | Description |
| --- | --- |
| [getConversationList](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/conversation/interfaces/IConversationLayout.html#getconversationlist) | Obtains the conversation list. |
| [setConversationTop](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/conversation/interfaces/IConversationLayout.html#setconversationtop) | Pins a conversation on top. |
| [deleteConversation](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/conversation/interfaces/IConversationLayout.html#deleteconversation) | Deletes a conversation. |


## ChatLayout

ChatLayout provides features such as message display and sending. Its user interface consists of the following four components, listed from the top down, and each component provides various methods to meet customization requirements.
- TitleBarLayout
- NoticeLayout
- MessageLayout
- InputLayout

| API | Description |
| --- | --- |
| [getInputLayout](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IChatLayout.html#getinputlayout) | Obtains the layout of the input area (InputLayout). |
| [getMessageLayout](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IChatLayout.html#getmessagelayout) | Obtains the layout of the message area (MessageLayout). |
| [getNoticeLayout](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IChatLayout.html#getnoticelayout) | Obtains the layout of the message area in the chat window (NoticeLayout). |
| [setChatInfo](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IChatLayout.html#setchatinfo) | Sets the current conversation ID, based on which the conversation panel loads relevant information required for the conversation, such as message records and user (group) information. |
| [exitChat](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IChatLayout.html#exitchat) | Quits a chat and releases relevant resources (this API is often invoked when an activity is finished.) |
| [initDefault](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IChatLayout.html#initdefault) | Initializes parameters. |
| [loadMessages](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IChatLayout.html#loadmessages) | Loads chat messages. |
| [sendMessage](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IChatLayout.html#sendmessage) | Sends messages. |


### NoticeLayout

NoticeLayout has a fixed position and is either displayed or hidden. When you scroll through chat content, its position remains unchanged. NoticeLayout can display group messages or broadcasts to be processed. Its layout is divided into two parts, which can be used to display the content topic and the auxiliary topic, respectively. You can set click events to respond to user operations.

| API | Description |
| --- | --- |
| [getContent](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/base/INoticeLayout.html#getcontent) | Obtains the topic information of a notice. |
| [getContentExtra](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/base/INoticeLayout.html#getcontentextra) | Obtains the further operations of a notice. |
| [setOnNoticeClickListener](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/base/INoticeLayout.html#setonnoticeclicklistener) | Sets click events for a notice. |
| [alwaysShow](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/base/INoticeLayout.html#alwaysshow) | Sets whether NoticeLayout is constantly displayed. |


### MessageLayout

MessageLayout is inherited from RecyclerView and displays messages. It provides many methods to meet customization requirements, such as appearance settings, click events, and custom message display.

#### Setting the profile photo
| API | Description |
| --- | --- |
| [setAvatar](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#setavatar) | Sets the default profile photo. By default, profile photos on the left and right are the same. |
| [getAvatar](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#getavatar) | Obtains the default profile photo. |
| [setAvatarRadius](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#setavatarradius) | Sets the border-radius of the profile photo. |
| [getAvatarRadius](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#getavatarradius) | Obtains the border-radius of the profile photo. |
| [setAvatarSize](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#setavatarsize) | Sets the profile photo size. |
| [getAvatarSize](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#getavatarsize) | Obtains the profile photo size. |


#### Setting the nickname style
| API | Description |
| --- | --- |
| [setNameFontSize](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#setnamefontsize) | Sets the nickname font size. |
| [getNameFontSize](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#getnamefontsize) | Obtains the nickname font size. |
| [setNameFontColor](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#setnamefontcolor) | Sets the nickname font color. |
| [getNameFontColor](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#getnamefontcolor) | Obtains the nickname font color. |
| [setLeftNameVisibility](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#setleftnamevisibility) | Sets whether to display the left nickname. |
| [getLeftNameVisibility](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#getleftnamevisibility) | Obtains the display status of the left nickname. |
| [setRightNameVisibility](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#setrightnamevisibility) | Sets whether to display the right nickname. |
| [getRightNameVisibility](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#getrightnamevisibility) | Obtains the display status of the right nickname. |


#### Setting bubbles
| API | Description |
| --- | --- |
| [setRightBubble](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#setrightbubble) | Sets the background of the right chat bubble. |
| [getRightBubble](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#getrightbubble) | Obtains the background of the right chat bubble. |
| [setLeftBubble](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#setleftbubble) | Sets the background of the left chat bubble. |
| [getLeftBubble](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#getleftbubble) | Obtains the background of the left chat bubble. |


#### Setting chat content
| API | Description |
| --- | --- |
| [setChatContextFontSize](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#setchatcontextfontsize) | Sets the font size of chat content. |
| [getChatContextFontSize](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#getchatcontextfontsize) | Obtains the font size of chat content. |
| [setRightChatContentFontColor](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#setrightchatcontentfontcolor) | Sets the font color of right chat content. |
| [getRightChatContentFontColor](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#getrightchatcontentfontcolor) | Obtains the font color of right chat content. |
| [getLeftChatContentFontColor](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#getleftchatcontentfontcolor) | Obtains the font color of left chat content. |
| [setLeftChatContentFontColor](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#setleftchatcontentfontcolor) | Sets the font color of left chat content. |


#### Setting the chat time
| API | Description |
| --- | --- |
| [setChatTimeBubble](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#setchattimebubble) | Sets the background for the chat time. |
| [getChatTimeBubble](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#getchattimebubble) | Obtains the background for the chat time. |
| [setChatTimeFontSize](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#setchattimefontsize) | Sets the font size of the chat time. |
| [getChatTimeFontSize](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#getchattimefontsize) | Obtains the font size of the chat time. |
| [setChatTimeFontColor](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#setchattimefontcolor) | Sets the font color of the chat time. |
| [getChatTimeFontColor](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#getchattimefontcolor) | Obtains the font color of the chat time. |


#### Setting chat prompts
| API | Description |
| --- | --- |
| [setTipsMessageBubble](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#settipsmessagebubble) | Sets the background of chat prompts. |
| [getTipsMessageBubble](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#gettipsmessagebubble) | Obtains the background of chat prompts. |
| [setTipsMessageFontSize](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#settipsmessagefontsize) | Sets the font size of chat prompts. |
| [getTipsMessageFontSize](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#gettipsmessagefontsize) | Obtains the font size of chat prompts. |
| [setTipsMessageFontColor](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#settipsmessagefontcolor) | Sets the font color of chat prompts. |
| [getTipsMessageFontColor](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html#gettipsmessagefontcolor) | Obtains the font color of chat prompts. |


#### Setting other information
| API | Description |
| --- | --- |
| [setAdapter](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageLayout.html#setadapter) | Sets the message list adapter (MessageListAdapter). |
| [setOnItemClickListener](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageLayout.html#setonitemclicklistener) | Sets the event listener for the message list (MessageLayout.OnItemClickListener). |
| [getOnItemClickListener](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageLayout.html#getonitemclicklistener) | Obtains click events for the message list. |
| [getPopActions](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageLayout.html#getpopactions) | Obtains the PopMenu action list. |
| [addPopAction](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageLayout.html#addpopaction) | Adds a custom action to PopMenu. |
| [setOnCustomMessageDrawListener](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageLayout.html#setoncustommessagedrawlistener) | Sets the callback for custom messages during rendering. When TUIKit refreshes a custom message, it invokes this callback. |


### InputLayout

InputLayout enables the input of common messages, including text, emojis, images, audio, videos, and files. In conjunction with MessageLayout.setOnCustomMessageDrawListener, it can send and display custom messages. In addition, you can hide, replace, or add InputLayout feature entries based on your actual business requirements.

| API | Description |
| --- | --- |
| [disableAudioInput](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IInputLayout.html#disableaudioinput) | Hides the button after audio input is disabled. |
| [disableEmojiInput](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IInputLayout.html#disableemojiinput) | Hides the button after emoji input is disabled. |
| [disableMoreInput](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IInputLayout.html#disablemoreinput) | Hides the button after the More feature is disabled. |
| [replaceMoreInput](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IInputLayout.html#replacemoreinput) | Replaces the panel that appears after you click "+". |
| [replaceMoreInput](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IInputLayout.html#replacemoreinput2) | Replaces the response event after you click "+". |
| [disableSendPhotoAction](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IInputLayout.html#disablesendphotoaction) | Hides the button on the More panel after image sending is disabled. |
| [disableCaptureAction](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IInputLayout.html#disablecaptureaction) | Hides the button on the More panel after photo taking is disabled. |
| [disableVideoRecordAction](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IInputLayout.html#disablevideorecordaction) | Hides the button on the More panel after video recording is disabled. |
| [disableSendFileAction](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IInputLayout.html#disablesendfileaction) | Hides the button on the More panel after file sending is disabled. |
| [addAction](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IInputLayout.html#addaction) | Adds an event unit on the More panel. |


## TitleBarLayout

ConversationLayout, ChatLayout, and other areas all have a title bar. The title bar is divided into the left, middle, and right parts. Images and text are allowed in the left and right parts, whereas only text is allowed in the middle part. These parts return standard Android views. You can interact with these views based on your actual business requirements.

| API | Description |
| --- | --- |
| [setLeftIcon](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/base/ITitleBarLayout.html#setlefticon) | Sets the icon of the left title. |
| [setRightIcon](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/base/ITitleBarLayout.html#setrighticon) | Sets the icon of the right title. |
| [setOnLeftClickListener](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/base/ITitleBarLayout.html#setonleftclicklistener) | Sets the click event for the left title. |
| [setOnRightClickListener](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/base/ITitleBarLayout.html#setonrightclicklistener) | Sets the click event for the right title. |
| [setTitle](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/base/ITitleBarLayout.html#settitle) | Sets the text title. The `position` parameter specifies the text position. |
| [getLeftGroup](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/base/ITitleBarLayout.html#getleftgroup) | Returns the left title section. |
| [getRightGroup](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/base/ITitleBarLayout.html#getrightgroup) | Returns the right title section. |
| [getLeftIcon](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/base/ITitleBarLayout.html#getlefticon) | Returns the icon of the left title. |
| [getRightIcon](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/base/ITitleBarLayout.html#getrighticon) | Returns the icon of the right title. |
| [getLeftTitle](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/base/ITitleBarLayout.html#getlefttitle) | Returns the text of the left title. |
| [getMiddleTitle](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/base/ITitleBarLayout.html#getmiddletitle) | Returns the text of the middle title. |
| [getRightTitle](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/base/ITitleBarLayout.html#getrighttitle) | Returns the text of the right title. |

