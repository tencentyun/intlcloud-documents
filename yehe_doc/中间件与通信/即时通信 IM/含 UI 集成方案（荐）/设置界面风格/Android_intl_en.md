This document describes how to set the UI styles for Android.

## Setting the Conversation List UI Styles
The conversation list UI consists of the title bar TitleBarLayout and list area ConversationListLayout. Each part provides UI styles and event registration APIs that can be modified.
<img src="https://qcloudimg.tencent-cloud.cn/raw/7d4c12e1246ce6b6c786114eda7b3532.png" style="zoom:50%;"/>

### Setting the title style
The title bar itself has all the features of a view. In addition, it is divided into three parts: left group (LeftGroup), middle, and right group (RightGroup).

<img src="https://qcloudimg.tencent-cloud.cn/raw/6dec8fa21bb42ea6c70d6e898634c28d.png" style="zoom:30%;"/>

To make custom modifications, see [ITitleBarLayout](https://github.com/tencentyun/TIMSDK/blob/master/Android/TUIKit/TUICore/tuicore/src/main/java/com/tencent/qcloud/tuicore/component/interfaces/ITitleBarLayout.java).
For example, the following code hides LeftGroup, sets the title in the middle, and hides the text and image buttons on the right in LeftGroup:
(See the implementation in [MainActivity](https://github.com/tencentyun/TIMSDK/blob/master/Android/Demo/app/src/main/java/com/tencent/qcloud/tim/demo/main/MainActivity.java).)
```java
mainTitleBar.setTitle(getResources().getString(R.string.conversation_title), ITitleBarLayout.Position.MIDDLE);
mainTitleBar.getLeftGroup().setVisibility(View.GONE);
mainTitleBar.getRightGroup().setVisibility(View.VISIBLE);
mainTitleBar.setRightIcon(R.drawable.more_btn);
```
The effect is shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/a89a69445edd8d4a11503e6ab708e6cd.png" style="zoom:40%;"/>

You can also customize click events:
```java
Menu menu = new Menu(this, mainTitleBar);
mainTitleBar.setOnRightClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        if (menu == null) {
            return;
        }
        if (menu.isShowing()) {
            menu.hide();
        } else {
            menu.show();
        }
    }
});
```


### Setting the conversation list style

The custom conversation list layout is inherited from RecyclerView. After the user logs in, TUIKit reads the user's conversation list from the SDK.
You can customize common features for the conversation list. For example, you can configure the background, font size, click event, long press event, and whether the profile photo has rounded corners. The following is a code sample:

```java
public static void customizeConversation(final ConversationLayout layout) {
    // Get the conversation list from ConversationLayout
    ConversationListLayout listLayout = layout.getConversationList();
    listLayout.setItemTopTextSize(16); // Set the font size of the top text of the item
    listLayout.setItemBottomTextSize(12); // Set the font size of the bottom text of the item
    listLayout.setItemDateTextSize(10); // Set the font size of the timeline text of the item
    listLayout.setItemAvatarRadius(5); // Set the size of the rounded corners of the item profile photo
    listLayout.disableItemUnreadDot(false); // Set whether to display an unread badge for the item. The badge is displayed by default.
    // Click and hold to pop up the menu
    listLayout.setOnItemLongClickListener(new ConversationListLayout.OnItemLongClickListener() {
        @Override
        public void OnItemLongClick(View view, int position, ConversationInfo conversationInfo) {
            startPopShow(view, position, conversationInfo);
        }
    });
}
```

The effects of different text font sizes and profile photos with rounded corners are as follows:
<table style="text-align:center;vertical-align:middle;width: 600px">
  <tr>
    <th style="text-align:center;" width="300px">Default Styles</th>
    <th style="text-align:center;" width="300px">Custom Styles</th>
  </tr>
  <tr>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/866f324419ee191b0b6aa72f13c9016d.png"  />    </td>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/e5558f38454d9e6600ed19ee1848c74d.png" />     </td>
	 </tr>
</table>

For more information, see [ConversationLayoutSetting.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/TUIKit/TUIConversation/tuiconversation/src/main/java/com/tencent/qcloud/tuikit/tuiconversation/setting/ConversationLayoutSetting.java).


### Setting the profile photo style

The IM SDK does not store profile photos. Therefore, the integrator needs to have a profile photo storage API to get profile photo URLs. The following shows how to use TUIKit to set a profile photo by using a random profile photo API as an example.
First, you need to upload a profile photo to your personal profile page and call the profile modification API.

```java
V2TIMUserFullInfo v2TIMUserFullInfo = new V2TIMUserFullInfo();
// Profile photo
if (!TextUtils.isEmpty(mIconUrl)) {
    v2TIMUserFullInfo.setFaceUrl(mIconUrl);
}
V2TIMManager.getInstance().setSelfInfo(v2TIMUserFullInfo, new V2TIMCallback() {
    @Override
    public void onError(int code, String desc) {
    }

    @Override
    public void onSuccess() {
    }
});
```
Conversation list profile photo, which is displayed in [ConversationCommonHolder.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/TUIKit/TUIConversation/tuiconversation/src/main/java/com/tencent/qcloud/tuikit/tuiconversation/ui/view/ConversationCommonHolder.java):
```java
conversationIconView.setConversation(conversation);
```

## Setting the Chat UI Styles
The chat UI includes the tile bar (TitleBarLayout), which is the same as that of the conversation list UI. The chat UI also includes the notice area (NoticeLayout), message area (MessageRecyclerView), and input area (InputView), as shown in the following figure:

<img src="https://qcloudimg.tencent-cloud.cn/raw/f77f84e36532a96f084b8ce7e4f8a3a8.png" style="zoom:50%;"/>

```java
/**
 * Get the input area layout in the chat UI
 *
 * @return
 */
InputView getInputLayout();
/**
 * Get the message area layout in the chat UI
 *
 * @return
 */
MessageRecyclerView getMessageLayout();

/**
 * Get the notice area layout in the chat UI
 *
 * @return
 */
NoticeLayout getNoticeLayout();
```

For more information, see [ChatLayoutSetting.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/TUIKit/TUIChat/tuichat/src/main/java/com/tencent/qcloud/tuikit/tuichat/setting/ChatLayoutSetting.java).


### Setting the notice area (NoticeLayout) style

The notice area consists of two TextViews, as shown in the following figure:
<img src="https://qcloudimg.tencent-cloud.cn/raw/157fb6c48a679a4be94299aa16c61115.png" style="zoom:30%;"/>
The effect is shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/86738ac0ff0706f902bfe0db7704db93.png" style="zoom:70%;"/>


```java
// Get NoticeLayout from ChatView
NoticeLayout noticeLayout = layout.getNoticeLayout();
// You can configure to always display the notice area
noticeLayout.alwaysShow(true);
// Set the notice title
noticeLayout.getContent().setText("This is an ad");
// Set notice text
noticeLayout.getContentExtra().setText("Click to view your gift");
// Set the click event of notice
noticeLayout.setOnNoticeClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        ToastUtil.toastShortMessage("You've received a bonus");
    }
});
```

### Setting the message area (MessageRecyclerView) style

MessageRecyclerView is inherited from RecyclerView. This document describes how to customize the chat background, bubbles, text, and nicknames. For more information, see [IMessageProperties.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/TUIKit/TUIChat/tuichat/src/main/java/com/tencent/qcloud/tuikit/tuichat/ui/interfaces/IMessageProperties.java).

<img src="https://qcloudimg.tencent-cloud.cn/raw/d73552bed43fc4686961ba179bc28ebf.png" style="zoom:90%;"/>

### Setting the chat UI background color
You can customize the chat UI background color. The following is a code sample:
```java
// Get MessageRecyclerView from ChatView
MessageRecyclerView messageRecyclerView = layout.getMessageLayout();
////// Set the chat background //////
messageRecyclerView.setBackground(new ColorDrawable(0xB0E2FF00));
```

The display effects of different chat UI background colors are as follows:
<table style="text-align:center;vertical-align:middle;width: 600px">
  <tr>
    <th style="text-align:center;" width="300px">Default Color</th>
    <th style="text-align:center;" width="300px">Custom Color</th>
  </tr>
  <tr>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/f907aabfe3761b34fc74b4c79845ef60.png"  />    </td>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/2ccf21d6aa52ec8a84d6de9d01fb77eb.png" />     </td>
	 </tr>
</table>


#### Setting the sender's profile photo style
When displaying a user, TUIKit reads the URL of the user's profile photo from the user's profile and displays the profile photo.
Sample code:

```java
// Setting a profile photo for the chat UI
if (!TextUtils.isEmpty(msg.getFaceUrl())) {
    List<Object> urllist = new ArrayList<>();
    urllist.add(msg.getFaceUrl());
    if (isForwardMode) {
        leftUserIcon.setIconUrls(urllist);
    } else {
        if (msg.isSelf()) {
            rightUserIcon.setIconUrls(urllist);
        } else {
            leftUserIcon.setIconUrls(urllist);
        }
    }
} else {
    rightUserIcon.setIconUrls(null);
    leftUserIcon.setIconUrls(null);
}
```
If the user does not set a profile photo, the default profile photo is displayed. You can customize the default profile photo, whether the profile photo has rounded corners, and the profile photo size.
Sample code:
```java
// Get MessageRecyclerView from ChatView
MessageRecyclerView messageRecyclerView = layout.getMessageLayout();
////// Set the chat background //////
messageRecyclerView.setBackground(new ColorDrawable(0xFFEFE5D4));
////// Set the profile photo //////
// Set the default profile photo. The receiver uses the same profile photo by default.
messageRecyclerView.setAvatar(R.drawable.core_default_user_icon_light);
// Set the rounded corners for the profile photo
messageRecyclerView.setAvatarRadius(50);
// Set the profile photo size
messageRecyclerView.setAvatarSize(new int[]{68, 68});
```

<table style="text-align:center;vertical-align:middle;width: 600px">
  <tr>
    <th style="text-align:center;" width="300px">Default Profile Photo Style</th>
    <th style="text-align:center;" width="300px">Custom Profile Photo Style</th>
  </tr>
  <tr>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/f3aa98a0b575b668e8f6cf86d6ab003c.png"  />    </td>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/b4f3d8aa8da9c20c8740211692bfc27e.png" />     </td>
	 </tr>
</table>

#### Setting bubble background colors
The receiver's bubbles are on the left and your own bubbles are on the right. You can customize the bubble background for both parties.
Sample code:

```java
// Get MessageRecyclerView from ChatView
MessageRecyclerView messageRecyclerView = layout.getMessageLayout();
// Set your own bubble background
messageRecyclerView.setRightBubble(context.getResources().getDrawable(R.drawable.chat_bubble_self_bg_lively));
// Set the bubble background for the receiver
messageRecyclerView.setLeftBubble(context.getResources().getDrawable(R.drawable.chat_bubble_other_bg_lively));
```

The display effects of different bubble background images are as follows:
<table style="text-align:center;vertical-align:middle;width: 600px">
  <tr>
    <th style="text-align:center;" width="300px">Default Bubble Background Image</th>
    <th style="text-align:center;" width="300px">Custom Bubble Background Image</th>
  </tr>
  <tr>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/f3aa98a0b575b668e8f6cf86d6ab003c.png"  />    </td>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/3ccba378c6f8606eef9f34bc8083ab99.png" />     </td>
	 </tr>
</table>

#### Setting the sender's nickname style
You can customize the nickname style, including the font size and color. The nickname styles of both parties must be the same.
Sample code:

```java
// Get MessageRecyclerView from ChatView
MessageRecyclerView messageRecyclerView = layout.getMessageLayout();
////// Set the nickname style (the receiver uses the same style) //////
messageRecyclerView.setNameFontSize(12);
messageRecyclerView.setNameFontColor(0x8B5A2B00);
```

The display effects of different nickname colors are as follows:
<table style="text-align:center;vertical-align:middle;width: 600px">
  <tr>
    <th style="text-align:center;" width="300px">Default Nickname Color</th>
    <th style="text-align:center;" width="300px">Custom Nickname Color</th>
  </tr>
  <tr>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/f3aa98a0b575b668e8f6cf86d6ab003c.png"  />    </td>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/8a6e500d6109a1922b879480bfd62728.png" />     </td>
	 </tr>
</table>

#### Setting the chat content style
You can customize the font size and color for both parties, but the sender and receiver must use the same font size.
Sample code:

```java
// Get MessageRecyclerView from ChatView
MessageRecyclerView messageRecyclerView = layout.getMessageLayout();
// Set the chat content font size. The sender and the receiver use the same font size.
messageRecyclerView.setChatContextFontSize(15);
// Set your own chat content font color
messageRecyclerView.setRightChatContentFontColor(0xA9A9A900);
// Set the chat content font color for the receiver
messageRecyclerView.setLeftChatContentFontColor(0xA020F000);
```

The display effects of different chat content font styles are as follows:
<table style="text-align:center;vertical-align:middle;width: 600px">
  <tr>
    <th style="text-align:center;" width="300px">Default Font Style</th>
    <th style="text-align:center;" width="300px">Custom Font Style</th>
  </tr>
  <tr>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/f3aa98a0b575b668e8f6cf86d6ab003c.png"  />    </td>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/614bacdb5c07f856eecc43d4a136b9ec.png" />     </td>
	 </tr>
</table>

#### Setting the chat timeline style

You can customize the background, font size, and font color of the chat timeline.
Sample code:

```java
// Get MessageRecyclerView from ChatView
MessageRecyclerView messageRecyclerView = layout.getMessageLayout();
// Set the background of the chat timeline
messageRecyclerView.setChatTimeBubble(new ColorDrawable(0x8B691400));
// Set the font size of the chat timeline
messageRecyclerView.setChatTimeFontSize(20);
// Set the font color of the chat timeline
messageRecyclerView.setChatTimeFontColor(0xEE00EE00);
```

The display effects of different timeline styles are as follows:
<table style="text-align:center;vertical-align:middle;width: 600px">
  <tr>
    <th style="text-align:center;" width="300px">Default Timeline Style</th>
    <th style="text-align:center;" width="300px">Custom Timeline Style</th>
  </tr>
  <tr>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/f3aa98a0b575b668e8f6cf86d6ab003c.png"  />    </td>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/5976a8c814c5215cdf14eae2d0d1690c.png" />     </td>
	 </tr>
</table>

#### Setting the tips message style

You can customize the background, font size, and font color of tips messages in chats.
Sample code:

```java
// Get MessageRecyclerView from ChatView
MessageRecyclerView messageRecyclerView = layout.getMessageLayout();
// Set the background of tips
messageRecyclerView.setTipsMessageBubble(new ColorDrawable(0xA020F000));
// Set the font size of tips
messageRecyclerView.setTipsMessageFontSize(20);
// Set the font color of tips
messageRecyclerView.setTipsMessageFontColor(0x7CFC0000);
```

The display effects of different tips messages are as follows:
<table style="text-align:center;vertical-align:middle;width: 600px">
  <tr>
    <th style="text-align:center;" width="300px">Default Tips Message Style</th>
    <th style="text-align:center;" width="300px">Custom Tips Message Style</th>
  </tr>
  <tr>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/a0652ef9215ce6f84dc76174d5d56e39.png"  />    </td>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/1ae13d10a19ff11c80377aa3534ae498.png" />     </td>
	 </tr>
</table>

### Setting the input area InputView
The input area (InputView) contains audio, text, emoji, and more (+) input options.
<img src="https://qcloudimg.tencent-cloud.cn/raw/53abac7901a717b6a58f2903339dfe0e.png" style="zoom:90%;"/>

#### Hiding undesired features

You can hide or show the image sharing, photo taking, video recording, and file sending features on the "+" panel.

```java
// Get InputLayout from ChatView
InputView inputView = layout.getInputLayout();
// Hide "take photo and send"
inputView.disableCaptureAction(true);
// Hide "send file"
inputView.disableSendFileAction(true);
// Hide "send image"
inputView.disableSendPhotoAction(true);
// Hide "record video and send"
inputView.disableVideoRecordAction(true);
```

#### Adding custom features
You can customize and add action units to the "+" panel to provide more features.

![Adding custom features](https://main.qcloudimg.com/raw/727056dd0e975dbaea86927040b385ab.gif)

The following code shows how to hide the "send file" feature and add an action unit which sends a message:

```java
// Get InputView from ChatView
InputView inputView = layout.getInputLayout();
// Hide "send file"
inputView.disableSendFileAction(true);
// Define an action unit
InputMoreActionUnit unit = new InputMoreActionUnit();
unit.setIconResId(R.drawable.default_user_icon); // Set the unit icon
unit.setTitleId(R.string.profile); // Set the text title of the unit
unit.setOnClickListener(unit.new OnActionClickListener() { // Define the click event
    @Override
    public void onClick() {
        ToastUtil.toastShortMessage("Custom more features");
        MessageInfo info = MessageInfoUtil.buildTextMessage("Who am I");
        layout.sendMessage(info, false);
    }
});
// Add the action unit to the "+" panel
inputView.addAction(unit);
```

#### Replacing the "+" click event
You can customize features to replace the action units on the "+" panel.

![Event Replacement](https://qcloudimg.tencent-cloud.cn/raw/75df00e962c34a845dbd3de0007303ca.png)

```java
// Get InputView from ChatView
InputView inputView = layout.getInputLayout();
// Replace the feature entry on the "+" panel with a custom event
inputView.replaceMoreInput(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        ToastUtil.toastShortMessage("Custom “+” button event");
        MessageInfo info = MessageInfoUtil.buildTextMessage("Custom message");
        layout.sendMessage(info, false);
    }
});
```


#### Replacing the panel displayed upon "+" clicking
You can customize the style of the "+" panel, the action units, and their features.

```java
// Get InputView from ChatView
InputView inputView = layout.getInputLayout();
// Use a custom fragment to replace more features
inputView.replaceMoreInput(new CustomInputFragment());
```

The implementation of the new panel CustomInputFragment is the same as that of an ordinary Fragment. Inflate the view at onCreateView and set the event. The following sample code shows how to add two buttons and pop up a toast when clicked:

```java
public static class CustomInputFragment extends BaseInputFragment {
    @Nullable
    @Override
    public View onCreateView(LayoutInflater inflater, @Nullable ViewGroup container, Bundle savedInstanceState) {
        View baseView = inflater.inflate(R.layout.test_chat_input_custom_fragment, container, false);
        Button btn1 = baseView.findViewById(R.id.test_send_message_btn1);
        btn1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                ToastUtil.toastShortMessage("Send a hyperlink message");
            }
        });
        Button btn2 = baseView.findViewById(R.id.test_send_message_btn2);
        btn2.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                ToastUtil.toastShortMessage("Send a message containing video and text");
            }
        });
        return baseView;
    }
}
```
The effect is shown below:

![Replacing the panel](https://main.qcloudimg.com/raw/d347f9e12358fb00d0c517e6a7aa44a6.gif)

