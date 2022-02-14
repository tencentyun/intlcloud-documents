This document describes how to set the UI styles for iOS.

## Setting profile photo styles

### Setting the default profile photo

When displaying a user, TUIKit reads the URL of the user's profile photo from the user's profile and displays the profile photo. If the user does not set a profile photo, the default profile photo is displayed.

You can customize the default profile photo.
```objectivec
TUIConfig *config = [TUIConfig defaultConfig]; 
// Modify the default profile photo
config.defaultAvatarImage = [UIImage imageNamed:@"Your Image"];
// Modify the default group profile photo
config.defaultGroupAvatarImage = [UIImage imageNamed:@"Your Image"];
```


### Setting the edge shape of the profile photo

Three types of profile photo edge shapes are available: rectangle with right-angle corners, round, and rectangle with rounded corners.

```objectivec
typedef NS_ENUM(NSInteger, TUIKitAvatarType) {
    TAvatarTypeNone,             /*Rectangle with right-angle corners*/
    TAvatarTypeRounded,          /*Round*/
    TAvatarTypeRadiusCorner,     /*Rectangle with rounded corners*/
};
```

You can modify the profile photo type in the way similar to that of modifying the default profile photo. The following is a code sample:

```objectivec
TUIConfig *config = [TUIConfig defaultConfig]; 
// Change the profile photo type to a rectangle with rounded corners of 5 degrees
config.avatarType = TAvatarTypeRadiusCorner;
config.avatarCornerRadius = 5.f;
```


## Setting the Chat UI Styles

#### Setting the chat UI background color
```objectivec
TUIC2CChatViewController *vc = ...; // Get the C2C chat UI object
vc.messageController.view.backgroundColor = [UIColor greenColor];
```

## Setting the Message Bubble Style
The following figure shows how message views are combined in the chat UI:
<img src="https://qcloudimg.tencent-cloud.cn/raw/e1337894a65e353387da86329fbb7786.png" width = "800"/>

### Setting message fonts and colors

Text message data comes from the TUITextMessageCellData class, whose API allows you to modify the fonts and colors of text messages.

```objectivec
// Set the font and color of sent text messages. The setting method for received text messages is similar.
[TUITextMessageCellData setOutgoingTextFont:[UIFont systemFontOfSize:20]];
[TUITextMessageCellData setOutgoingTextColor:[UIColor redColor]];
```

### Setting bubble background images

The image displayed in the bubble cell is obtained from TUIBubbleMessageCellData. The object provides a class method to set bubble background images.

```objectivec
// Set sent-message bubbles, including the common and selected states. The setting method for received-message bubbles is similar.
[TUIBubbleMessageCellData setOutgoingBubble:[UIImage imageNamed:@"bubble"]];
[TUIBubbleMessageCellData setOutgoingHighlightedBubble:[UIImage imageNamed:@"bubble_highlight"]];
```


### Setting bubble margins

In TUIKit, text and voice messages are displayed in bubbles. TUIMessageCellLayout provides a class method bubbleInsets to set bubble margins.

```objectivec
// Set the margins for sent-message bubbles. The setting method for received-message bubbles is similar.
[TUIMessageCellLayout outgoingTextMessageLayout].bubbleInsets = UIEdgeInsetsMake(10, 10, 20, 20);
```

### Setting the sender's profile photo style

```objectivec
// Set the size of the sender's profile photo. The setting method for the recipient's profile photo is similar.
[TUIMessageCellLayout outgoingTextMessageLayout].avatarSize = CGSizeMake(100, 100);
```

```objectivec
// Set the position of the sender's profile photo. The setting method for the recipient's profile photo is similar.
[TUIMessageCellLayout outgoingTextMessageLayout].avatarInsets = UIEdgeInsetsMake(10, 10, 20, 20);
```

For other message types, obtain the corresponding layout instances to set the profile photo sizes and positions.

### Setting the sender's nickname style

Setting the nickname font and color is similar to setting the profile photo position, that is, modifying the related properties of TUIMessageCellLayout.

```objectivec
// Set the nickname font for received messages. The setting method for sent messages is similar. However, the sender's nickname is not displayed by default.
[TUIMessageCellData setIncommingNameFont:[UIFont systemFontOfSize:20]];
[TUIMessageCellData setIncommingNameColor:[UIColor redColor]];
```




