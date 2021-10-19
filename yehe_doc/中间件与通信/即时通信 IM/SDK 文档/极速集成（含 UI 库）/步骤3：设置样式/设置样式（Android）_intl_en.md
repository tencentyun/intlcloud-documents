This document describes how to set styles for Android.

## Setting the Conversation List Style
The conversation list layout consists of TitleBarLayout and ConversationListLayout. Each part provides UI styles and event registration APIs that can be modified.

### Modifying the TitleBarLayout style

The title bar itself has all the features of a view. In addition, it is divided into three parts: left group, middle group, and right group.
![TitleBarLayout](https://main.qcloudimg.com/raw/b95c53bd3961372e1ee75bb65dcafbe6.png)

To make custom modifications, see [ITitleBarLayout](https://github.com/tencentyun/TIMSDK/blob/master/Android/Demo/tuikit/src/main/java/com/tencent/qcloud/tim/uikit/base/ITitleBarLayout.java).
For example, the following code hides LeftGroup, sets the title in the middle, and hides the text and image buttons on the right in ConversationLayout:

```java
// Get TitleBarLayout
TitleBarLayout titleBarLayout = mConversationLayout.findViewById(R.id.conversation_title);
// Set the title
titleBarLayout.setTitle(getResources().getString(R.string.conversation_title), TitleBarLayout.POSITION.MIDDLE);
// Hide the left group
titleBarLayout.getLeftGroup().setVisibility(View.GONE);
// Set the menu icon on the right
titleBarLayout.setRightIcon(R.drawable.conversation_more);
```

The effect is shown below:
![Title bar effect](https://main.qcloudimg.com/raw/416ad8b8050f11fad6d7c7ee869d554f.png)

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

The custom conversation list layout is inherited from RecyclerView. After the user logs in, TUIKit reads the user's conversation list from the SDK.
You can customize common features for the conversation list. For example, you can confgure the background, font size, click event, "click and hold" event, and whether the profile photo has rounded corners. The sample code is as follows:

```java
public static void customizeConversation(final ConversationLayout layout) {
    // Get the conversation list from ConversationLayout
    ConversationListLayout listLayout = layout.getConversationList();
    listLayout.setItemTopTextSize(16); // Set the font size of top text in items
    listLayout.setItemBottomTextSize(12); // Set the font size of bottom text items
    listLayout.setItemDateTextSize(10); // Set the font size of timeline text in items
    listLayout.setItemAvatarRadius(5); // Set the size of the rounded corners of the adapter item profile photo
    listLayout.disableItemUnreadDot(false); // Set whether the item displays an unread badge or not. Badge is displayed by default.
    // Click and hold to pop up the menu
    listLayout.setOnItemLongClickListener(new ConversationListLayout.OnItemLongClickListener() {
        @Override
        public void OnItemLongClick(View view, int position, ConversationInfo conversationInfo) {
            startPopShow(view, position, conversationInfo);
        }
    });
}
```

For more information, please see [ConversationLayoutSetting.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/TUIKit/TUIConversation/tuiconversation/src/main/java/com/tencent/qcloud/tuikit/tuiconversation/setting/ConversationLayoutSetting.java).


### Setting the profile photo

The IM SDK does not store profile photos, so the developer needs to have a profile photo storage API in order to get profile photo URLs. TUIKit uses a random profile photo API as an example to show how to set a profile photo.
First, you need to upload a profile photo to your personal profile page and call the API to modify the profile.

```
HashMap<String, Object> hashMap = new HashMap<>();
// The profile photo. `mIconUrl` is the URL of the uploaded profile photo. See the example of a random profile photo in Demo.
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

Get and display conversation list profile photos in `ConversationCommonHolder.java`:

```
if (!TextUtils.isEmpty(conversation.getIconUrl())) {
   List<String> urllist = new ArrayList<>();
   urllist.add(conversation.getIconUrl());
   conversationIconView.setIconUrls(urllist);
   urllist.clear();
}
```


## Setting the Chat Interface
The chat interface includes TitleBarLayout, which is the same as that of the conversation list interface. The chat interface also includes NoticeLayout, MessageLayout, and InputLayout, as shown in the following figure:
![Chat interface composition](https://main.qcloudimg.com/raw/8b6e650af731fffc4a816fbf54920970.png)

```java
/**
 * Get the notice layout in the chat interface
 * @return
 */
NoticeLayout getNoticeLayout();

/**
 * Get the message layout in the chat interface
 * @return
 */
MessageLayout getMessageLayout();

/**
 * Get the input layout in the chat interface
 * @return
 */
InputLayout getInputLayout();
```


### Modifying the NoticeLayout style

NoticeLayout consists of two TextViews, as shown in the following figure:
![NoticeLayout composition](https://main.qcloudimg.com/raw/1a34baf21414ffe9671a31a7223c6377.png)

```java
// Get NoticeLayout from ChatLayout
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
        ToastUtil.toastShortMessage("You've received a bonus");
    }
});
```

### Modifying the MessageLayout style

MessageLayout is inherited from RecyclerView. This document describes how to customize the chat background, bubbles, text, and nicknames. For more information, please see [ IMessageProperties.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/TUIKit/TUIChat/tuichat/src/main/java/com/tencent/qcloud/tuikit/tuichat/ui/interfaces/IMessageProperties.java).

#### Modifying the chat background

You can customize the settings of the chat background.

```java
// Get MessageLayout from ChatLayout
MessageLayout messageLayout = layout.getMessageLayout();
////// Set the chat background //////
messageLayout.setBackground(new ColorDrawable(0xB0E2FF00));
```


#### Modifying profile photo properties

To display a user, TUIKit reads the profile photo URL from the user profile and displays it.

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

If the user does not set a profile photo, the default profile photo is displayed. You can customize the default profile photo, whether the profile photo has rounded corners, and the profile photo size.

```java
// Get MessageLayout from ChatLayout
MessageLayout messageLayout = layout.getMessageLayout();
////// Set the profile photo //////
// Set the default profile photo. The recipient uses the same profile photo by default.
messageLayout.setAvatar(R.drawable.ic_chat_input_file);
// Set rounded corners for the profile photo. No rounded corners by default.
messageLayout.setAvatarRadius(50);
// Set the profile photo size
messageLayout.setAvatarSize(new int[]{48, 48});
```


#### Modifying bubbles
The recipient’s bubbles are on the left and your own bubbles are on the right. You can customize the bubble background for both parties.

```java
// Get MessageLayout from ChatLayout
MessageLayout messageLayout = layout.getMessageLayout();
// Set your own bubble background
messageLayout.setRightBubble(context.getResources().getDrawable(R.drawable.chat_opposite_bg));
// Set the bubble background for the recipient
messageLayout.setLeftBubble(context.getResources().getDrawable(R.drawable.chat_self_bg));
```


#### Modifying the nickname style
You can customize the nickname style, including the font size and color. The nickname styles of both parties must be the same.

```java
// Get MessageLayout from ChatLayout
MessageLayout messageLayout = layout.getMessageLayout();
////// Set the nickname style (the recipient uses the same style) //////
messageLayout.setNameFontSize(12);
messageLayout.setNameFontColor(0x8B5A2B00);
```


#### Modifying the chat content style
You can customize the font size and color for both parties, but the sender and recipient must use the same font size.

```java
// Get MessageLayout from ChatLayout
MessageLayout messageLayout = layout.getMessageLayout();
// Set the chat content font size. The sender and the recipient use the same font size.
messageLayout.setChatContextFontSize(15);
// Set your own chat content font color
messageLayout.setRightChatContentFontColor(0xA9A9A900);
// Set the chat content font color for the recipient
messageLayout.setLeftChatContentFontColor(0xA020F000);
```


#### Modifying the chat timeline style

You can customize the background, font size, and font color of the chat timeline.

```java
// Get MessageLayout from ChatLayout
MessageLayout messageLayout = layout.getMessageLayout();
// Set the background of the chat timeline
messageLayout.setChatTimeBubble(new ColorDrawable(0x8B691400));
// Set the font size of the chat timeline
messageLayout.setChatTimeFontSize(20);
// Set the font color of the chat timeline
messageLayout.setChatTimeFontColor(0xEE00EE00);
```


#### Modifying the tips message style

You can customize the background, font size, and font color of tips messages in chats.

```java
// Get MessageLayout from ChatLayout
MessageLayout messageLayout = layout.getMessageLayout();
// Set the background of tips
messageLayout.setTipsMessageBubble(new ColorDrawable(0xA020F000));
// Set the font size of tips
messageLayout.setTipsMessageFontSize(20);
// Set the font color of tips
messageLayout.setTipsMessageFontColor(0x7CFC0000);
```


### Setting InputLayout
InputLayout contains audio, text, emoji, and more (+) input options.
![InputLayout](https://main.qcloudimg.com/raw/d5dcf6b35f70714182196ea00a1c28a4.png)

#### Hiding undesired features

You can hide or show the image sharing, photo taking, video recording, and file sending features on the "+" panel.

```java
// Get InputLayout from ChatLayout
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

#### Adding custom features (method 1)
You can customize and add action units to the "+" panel to provide more features.
The following code shows how to hide the "send file" feature and add an action unit which sends a message:

```java
// Get InputLayout from ChatLayout
InputLayout inputLayout = layout.getInputLayout();
// Hide "send file"
inputLayout.disableSendFileAction(true);
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
inputLayout.addAction(unit);
```


#### Adding custom features (method 2; added in version `5.4.666`)
The final effect is the same as method 1. The sample code is as follows ([you can also refer to the implementation of the audieo and video call features](https://github.com/tencentyun/TIMSDK/blob/master/Android/Demo/tuikit-live/src/main/java/com/tencent/qcloud/tim/tuikit/live/helper/TUIKitLiveChatController.java)):
```java
class CustomChatController implements TUIChatControllerListener {
    // This method is called to add a action unit each time the "+" button is clicked
    @Override
    public List<IBaseAction> onRegisterMoreActions() {
        InputMoreActionUnit action = new InputMoreActionUnit() {
            // Method triggered upon clicks
            @Override
            public void onAction(String chatInfoId, int chatType) {
                // Create a text message
                MessageInfo info = MessageInfoUtil.buildTextMessage("Who am I");
                IBaseMessageSender messageSender = TUIKitListenerManager.getInstance().getMessageSender();
                if (messageSender != null) {
                    // Send the message
                    messageSender.sendMessage(info, null, chatInfoId,
                            chatType == V2TIMConversation.V2TIM_GROUP, false, new IUIKitCallBack() {
                                @Override
                                public void onSuccess(Object data) {
                                    Log.i("CustomChatController", "send success");
                                }

                                @Override
                                public void onError(String module, int errCode, String errMsg) {
                                    Log.i("CustomChatController", "send failed");
                                }
                            });
                }
            }
        };
        action.setTitleId(R.string.profile);
        action.setIconResId(R.drawable.default_user_icon);
        List<IBaseAction> list = new ArrayList<>();
        list.add(action);
        return list;
    }

    ......

}

// Register as soon as possible
TUIKitListenerManager.getInstance().addChatListener(new CustomChatController());
```

#### Replacing the "+" click event
You can customize features to replace the action units on the "+" panel.

```java
// Get InputLayout from ChatLayout
InputLayout inputLayout = layout.getInputLayout();
// Replace the feature entry on the "+" panel with a custom event
inputLayout.replaceMoreInput(new View.OnClickListener() {
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
// Get InputLayout from ChatLayout
InputLayout inputLayout = layout.getInputLayout();
// Use a custom fragment to replace more features
inputLayout.replaceMoreInput(new CustomInputFragment());
```

The implementation of the new panel CustomInputFragment is the same as that of a common Fragment. Inflate the view at onCreateView and set the event. The following sample code shows how to add two buttons and pop up a toast when clicked:

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


