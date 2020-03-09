
## Setting the Conversation List
The conversation list layout consists of TitleBarLayout and ConversationListLayout. Each component provides UI styles and event registration APIs that can be modified for customization purposes.
![Conversation list](https://main.qcloudimg.com/raw/8adef6cec9f943958bbcbd0959130ce6.png)

### Modifying the TitleBarLayout style

The title bar has all the features of a view. In addition, it is divided into three parts: left group, middle group, and right group, as shown in the following figure:
![Title bar structure](https://main.qcloudimg.com/raw/832fd209cbc6061b47ff5434740b210c.png)

To make custom modifications, see [ITitleBarLayout](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/base/ITitleBarLayout.html).
For example, in ConversationLayout, the following code hides LeftGroup, sets the title in the middle, and hides the text and image buttons on the right:

```java
// Obtain TitleBarLayout
TitleBarLayout titleBarLayout = mConversationLayout.findViewById(R.id.conversation_title);
// Set the title
titleBarLayout.setTitle(getResources().getString(R.string.conversation_title), TitleBarLayout.POSITION.MIDDLE);
// Hide the left group
titleBarLayout.getLeftGroup().setVisibility(View.GONE);
// Set the menu icon on the right
titleBarLayout.setRightIcon(R.drawable.conversation_more);
```

The following figure shows the result:
![Title bar display](https://main.qcloudimg.com/raw/b4d5c63dac1fa602830574ea4096c89f.png)

You can also customize click events:

```java
// Menu class
mMenu = new Menu(getActivity(), titleBarLayout, Menu.MENU_TYPE_CONVERSATION);
// Click event that responds to a menu button
titleBarLayout.setOnRightClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View view) {
        if (mMenu.isShowing()) {
            mMenu.hide();
        } else {
            mMenu.show();
        }
    }
});
```

 
### Modifying the ConversationListLayout style

The custom conversation list layout inherits from RecyclerView. After a user logs in, TUIKit reads the user’s conversation list from the SDK.
You can customize the common features of the conversation list, such as whether the profile photo has rounded corners, the background, font size, click event, and long-press event. The sample code is as follows:

```java
public static void customizeConversation(final ConversationLayout layout) {
    // Obtain the conversation list from ConversationLayout
    ConversationListLayout listLayout = layout.getConversationList();
    listLayout.setItemTopTextSize(16); // Set the top text size in item
    listLayout.setItemBottomTextSize(12);// Set the bottom text size in item
    listLayout.setItemDateTextSize(10);// Set the timeline text size in item
    listLayout.enableItemRoundIcon(true);// Set whether the profile photo of item has rounded corners. The default is the standard square.
    listLayout.disableItemUnreadDot(false);// Set whether item displays an unread badge or not. The default is to display the badge.
    // Long press to display the menu
    listLayout.setOnItemLongClickListener(new ConversationListLayout.OnItemLongClickListener() {
        @Override
        public void OnItemLongClick(View view, int position, ConversationInfo conversationInfo) {
            startPopShow(view, position, conversationInfo);
        }
    });
}
```

For more information, see [ConversationLayoutHelper.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/app/src/main/java/com/tencent/qcloud/tim/demo/helper/ConversationLayoutHelper.java).


### Setting the profile photo

The IM SDK does not store profile photos, and therefore a profile photo storage API must be available for obtaining profile photo URLs. In the following example, TUIKit uses a random profile photo API to show how to set a profile photo.
First, upload a profile photo to your personal profile page and call the API to modify the profile.

```
HashMap<String, Object> hashMap = new HashMap<>();
// Profile photo. mIconUrl indicates the URL of the uploaded profile photo. See the example of a random profile photo in the demo.
if (!TextUtils.isEmpty(mIconUrl)) {
   hashMap.put(TIMUserProfile.TIM_PROFILE_TYPE_KEY_FACEURL, mIconUrl);
}
TIMFriendshipManager.getInstance().modifySelfProfile(hashMap, new TIMCallBack() {
   @Override
   public void onError(int i, String s) {
       DemoLog.e(TAG, "modifySelfProfile err code = " + i + ", desc = " + s);
       ToastUtil.toastShortMessage("Error code = " + i + ", desc = " + s);
   }
   @Override
   public void onSuccess() {
       DemoLog.i(TAG, "modifySelfProfile success");
   }
});
```

Obtain and display conversation list profile photos in ConversationCommonHolder.java:

```
if (!TextUtils.isEmpty(conversation.getIconUrl())) {
   List<String> urllist = new ArrayList<>();
   urllist.add(conversation.getIconUrl());
   conversationIconView.setIconUrls(urllist);
   urllist.clear();
}
```


## Setting the Chat Interface
The chat interface includes TitleBarLayout, which can be used in the same way as that of the conversation list interface. The chat interface also includes NoticeLayout, MessageLayout, and InputLayout, as shown in the following figure:
![Chat interface components](https://main.qcloudimg.com/raw/8b6e650af731fffc4a816fbf54920970.png)
The following figure shows the result:
![Chat interface with more features](https://main.qcloudimg.com/raw/5953198d2a5249d1b18f218b319cdd2c.png)

```java
/**
 * Obtain the notice layout in the chat interface
 * @return
 */
NoticeLayout getNoticeLayout();

/**
 * Obtain the message layout in the chat interface
 * @return
 */
MessageLayout getMessageLayout();

/**
 * Obtain the input layout in the chat interface
 * @return
 */
InputLayout getInputLayout();
```


### Modifying the NoticeLayout style

NoticeLayout consists of two TextViews, as shown in the following figure:
![NoticeLayout components](https://main.qcloudimg.com/raw/1a34baf21414ffe9671a31a7223c6377.png)
The following figure shows the result:
![Notice display](https://main.qcloudimg.com/raw/406ce089eccc51524e559e0a9f69c1f6.png)

```java
// Obtain NoticeLayout from ChatLayout
NoticeLayout noticeLayout = layout.getNoticeLayout();
// You can always display the notice area
noticeLayout.alwaysShow(true);
// Set the notice title
noticeLayout.getContent().setText("This is an ad");
// Set notice text
noticeLayout.getContentExtra().setText("Click to view your gift");
// Set the click event of notice
noticeLayout.setOnNoticeClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        ToastUtil.toastShortMessage("You have received a bonus");
    }
});
```

### Modifying the MessageLayout style

MessageLayout is inherited from RecyclerView. This document describes how to customize the chat background, bubbles, text, and nicknames. For more information, see [IMessageProperties](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/chat/interfaces/IMessageProperties.html).
![MessageLayout](https://main.qcloudimg.com/raw/063933c9ace8f762695af5a75a70c4b8.png)

#### Modifying the chat background

You can customize the chat background.
![Modifying the chat background](https://main.qcloudimg.com/raw/fbab3a9bc355b4ba47ee2d864c7a8bf5.png)

```java
// Obtain MessageLayout from ChatLayout
MessageLayout messageLayout = layout.getMessageLayout();
////// Set the chat background //////
messageLayout.setBackground(new ColorDrawable(0xB0E2FF00));
```


#### Modifying profile photo properties

To display a user, TUIKit reads the profile photo URL from the user profile and displays it.
![Modifying the profile photo](https://main.qcloudimg.com/raw/16ba2fdf5bd410efc19ad88f056f9022.png)

```
// Set the profile photo and nickname on the chat interface
TIMUserProfile profile = TIMFriendshipManager.getInstance().queryUserProfile(msg.getFromUser());
  if (profile == null) {
      usernameText.setText(msg.getFromUser());
  } else {
      usernameText.setText(!TextUtils.isEmpty(profile.getNickName()) ? profile.getNickName() : msg.getFromUser());
  if (!TextUtils.isEmpty(profile.getFaceUrl()) && !msg.isSelf()) {
      List<String> urllist = new ArrayList<>();
      urllist.add(profile.getFaceUrl());
      leftUserIcon.setIconUrls(urllist);
      urllist.clear();
  }
}
TIMUserProfile selfInfo = TIMFriendshipManager.getInstance().queryUserProfile(TIMManager.getInstance().getLoginUser());
  if (profile != null && msg.isSelf()) {
       if (!TextUtils.isEmpty(selfInfo.getFaceUrl())) {
       List<String> urllist = new ArrayList<>();
       urllist.add(profile.getFaceUrl());
       rightUserIcon.setIconUrls(urllist);
       urllist.clear();
  }
}
```

If the user does not set the profile photo, the default profile photo is displayed. You can customize the default profile photo, whether the profile photo has rounded corners, and the profile photo size.

```java
// Obtain MessageLayout from ChatLayout
MessageLayout messageLayout = layout.getMessageLayout();
////// Set the profile photo //////
// Set the default profile photo. The peer uses the same profile photo by default.
messageLayout.setAvatar(R.drawable.ic_chat_input_file);
// Set rounded corners for the profile photo. The default is no rounded corners.
messageLayout.setAvatarRadius(50);
// Set the profile photo size
messageLayout.setAvatarSize(new int[]{48, 48});
```


#### Modifying bubbles
Peer bubbles are located on the left and sender bubbles are on the right. You can customize the bubble background for both parties.
![Modifying bubbles](https://main.qcloudimg.com/raw/670e40297978817012d9cd81524e73e7.png)

```java
// Obtain MessageLayout from ChatLayout
MessageLayout messageLayout = layout.getMessageLayout();
// Set your own bubble background
messageLayout.setRightBubble(context.getResources().getDrawable(R.drawable.chat_opposite_bg));
// Set the bubble background for the peer
messageLayout.setLeftBubble(context.getResources().getDrawable(R.drawable.chat_self_bg));
```


#### Modifying the nickname style
You can customize the nickname style, including the font size and color. The nickname styles of both parties must be the same.
![Modifying the nickname](https://main.qcloudimg.com/raw/df0ab81eccc1c2f65804c20964b76419.png)

```java
// Obtain MessageLayout from ChatLayout
MessageLayout messageLayout = layout.getMessageLayout();
////// Set the nickname style (which is the same for the peer) //////
messageLayout.setNameFontSize(12);
messageLayout.setNameFontColor(0x8B5A2B00);
```


#### Modifying the chat content style
You can customize the font size and color of chat content for both parties, but they must use the same font size.
![Modifying chat content](https://main.qcloudimg.com/raw/6b86269ecef12ba43762d917f596a51c.png)

```java
// Obtain MessageLayout from ChatLayout
MessageLayout messageLayout = layout.getMessageLayout();
// Set the font size of chat content. Both parties use the same font size.
messageLayout.setChatContextFontSize(15);
// Set your own font color of chat content
messageLayout.setRightChatContentFontColor(0xA9A9A900);
// Set the font color of chat content for the peer
messageLayout.setLeftChatContentFontColor(0xA020F000);
```


#### Modifying the chat timeline style

You can customize the background, font size, and font color of the chat timeline.
![Modifying the timeline style](https://main.qcloudimg.com/raw/278f58e24d1cf05601d789a45b840fc0.png)

```java
// Obtain MessageLayout from ChatLayout
MessageLayout messageLayout = layout.getMessageLayout();
// Set the background of the chat timeline
messageLayout.setChatTimeBubble(new ColorDrawable(0x8B691400));
// Set the font size of the chat timeline
messageLayout.setChatTimeFontSize(20);
// Set the font color of the chat timeline
messageLayout.setChatTimeFontColor(0xEE00EE00);
```


#### Modifying the prompt message style

You can customize the background, font size, and font color of prompt messages.
![Modifying the prompt message style](https://main.qcloudimg.com/raw/a59d9b24ec12abea73c78996d912976e.png)

```java
// Obtain MessageLayout from ChatLayout
MessageLayout messageLayout = layout.getMessageLayout();
// Set the background of prompt messages
messageLayout.setTipsMessageBubble(new ColorDrawable(0xA020F000));
// Set the font size of prompt messages
messageLayout.setTipsMessageFontSize(20);
// Set the font color of tips
messageLayout.setTipsMessageFontColor(0x7CFC0000);
```


### Setting InputLayout
InputLayout includes the audio, text, emoji, and more (+) input options.
![InputLayout](https://main.qcloudimg.com/raw/262f09005c939b5004e437df58112056.png)

#### Hiding undesired features

You can hide or show the image sharing, photo taking, video recording, and file sharing features on the "+" panel.

```java
// Obtain InputLayout from ChatLayout
InputLayout inputLayout = layout.getInputLayout();
// Hide "take photo and send"
inputLayout.disableCaptureAction(true);
// Hide "send file"
inputLayout.disableSendFileAction(true);
// Hide "send image"
inputLayout.disableSendPhotoAction(true);
// Hide "record video and send"
inputLayout.disableVideoRecordAction(true);
```

#### Adding custom features
You can customize and add action units to the "+" panel to provide more features.
![Adding custom features](https://main.qcloudimg.com/raw/727056dd0e975dbaea86927040b385ab.gif)
The following code shows how to hide the "send file" feature and add an action unit that sends a message:

```java
// Obtain InputLayout from ChatLayout
InputLayout inputLayout = layout.getInputLayout();
// Hide "send file"
inputLayout.disableSendFileAction(true);
// Define an action unit
InputMoreActionUnit unit = new InputMoreActionUnit();
unit.setIconResId(R.drawable.default_user_icon); // Set the icon of the unit
unit.setTitleId(R.string.profile); // Set the text title of the unit
unit.setOnClickListener(new View.OnClickListener() { // Define the click event
    @Override
    public void onClick(View v) {
        ToastUtil.toastShortMessage("More custom features");
        MessageInfo info = MessageInfoUtil.buildTextMessage("Who am I");
        layout.sendMessage(info, false);
    }
});
// Add the action unit to the "+" panel
inputLayout.addAction(unit);
```


#### Replacing the click "+" event
You can customize features to replace action units on the "+" panel.
![Replacement event](https://main.qcloudimg.com/raw/5acf471b7a36cd8be511b1b44c0abdbf.gif)

```java
// Obtain InputLayout from ChatLayout
InputLayout inputLayout = layout.getInputLayout();
// Replace a feature entry on the "+" panel with a custom event
inputLayout.replaceMoreInput(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        ToastUtil.toastShortMessage("Button event of more custom features");
        MessageInfo info = MessageInfoUtil.buildTextMessage("Custom message");
        layout.sendMessage(info, false);
    }
});
```


#### Replacing the panel displayed by clicking "+"
You can customize the style of the "+" panel as well as action units and their features.

```java
// Obtain InputLayout from ChatLayout
InputLayout inputLayout = layout.getInputLayout();
// Use a custom fragment to replace more features
inputLayout.replaceMoreInput(new CustomInputFragment());
```

The implementation of the new panel CustomInputFragment is the same as a common Fragment. To do this, inflate the view during onCreateView and set the event. The following sample code shows how to add two buttons and displays a toast when clicking the buttons:

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
                ToastUtil.toastShortMessage("Send a video-and-text message");
            }
        });
        return baseView;
    }
}
```
The following figure shows the result:
![Replacing the panel](https://main.qcloudimg.com/raw/d347f9e12358fb00d0c517e6a7aa44a6.gif)
