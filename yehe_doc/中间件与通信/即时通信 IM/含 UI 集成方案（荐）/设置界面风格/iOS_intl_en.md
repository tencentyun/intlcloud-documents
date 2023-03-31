This document describes how to set the UI styles for iOS.

## Setting profile photo styles

### Setting the default profile photo
When displaying a user, TUIKit reads the URL of the user's profile photo from the user's profile and displays the profile photo. If the user does not set a profile photo, the default profile photo is displayed.
You can customize the default profile photo before TUIKit initialization. The following is a code sample:
```objectivec
TUIConfig *config = [TUIConfig defaultConfig]; 
// Modify the default profile photo
config.defaultAvatarImage = [UIImage imageNamed:@"your image"];
// Modify the default group profile photo
config.defaultGroupAvatarImage = [UIImage imageNamed:@"your group image"];
// Display the 3x3 grid display of group profile photos
config.enableGroupGridAvatar = NO;
```

>? The default profile photo of a group is a 3 x 3 grid consisting of group members' profile photos. If the 3 x 3 grid fails to be generated or the group contains only one member, TUIKit displays `defaultGroupAvatarImage` as the group profile photo.
>You can disable the display of the 3 x 3 grid consisting of group members' profile photos as needed.

### Setting the profile photo shape
TUIKit provides three types of profile photo shapes: rectangle with right-angle corners, round, and rectangle with rounded corners.
```objectivec
typedef NS_ENUM(NSInteger, TUIKitAvatarType) {
    TAvatarTypeNone,             /*Rectangle with right-angle corners*/
    TAvatarTypeRounded,          /*Round*/
    TAvatarTypeRadiusCorner,     /*Rectangle with rounded corners*/
};
```

You can customize the profile photo shape before TUIKit initialization. The following is a code sample:
```objectivec
TUIConfig *config = [TUIConfig defaultConfig]; 
// Change the profile photo type to a rectangle with rounded corners of 5 degrees
config.avatarType = TAvatarTypeRadiusCorner;
config.avatarCornerRadius = 5.f;
```


## Setting the Chat UI Styles

### Setting the chat UI background color
You can customize chat UI background color before TUIKit initialization. The following is a code sample:
```objectivec
[TUIChatConfig defaultConfig].backgroudColor = [UIColor greenColor];
```


### Setting the chat UI background image
You can customize chat UI background image before TUIKit initialization. The following is a code sample:
```objectivec
[TUIChatConfig defaultConfig].backgroudImage = [UIImage imageNamed:@"your chat background image"];
```



## Setting the Message Bubble Style
The following figure shows how message views are combined in the chat UI:
<img src="https://qcloudimg.tencent-cloud.cn/raw/7dedc729dc19b35c56f155e3961b8681.png" style="zoom:40%;"/>

### Setting message fonts and colors
Text message data comes from the TUITextMessageCellData class, whose API allows you to modify the fonts and colors of text messages.
You can customize message fonts and colors before TUIKit initialization. The following is a code sample:
```objectivec
// Set the font and color of sent text messages
[TUITextMessageCellData setOutgoingTextFont:[UIFont systemFontOfSize:20]];
[TUITextMessageCellData setOutgoingTextColor:[UIColor blueColor]];
// Set the font and color of received text messages
[TUITextMessageCellData setIncommingTextFont:[UIFont systemFontOfSize:20]];
[TUITextMessageCellData setIncommingTextColor:[UIColor purpleColor]];
```



### Setting bubble background images
The image displayed in the bubble cell is obtained from TUIBubbleMessageCellData. The object provides a class method to set bubble background images.
You can customize bubble background images before chat UI initialization. The following is a code sample:
```objectivec
// Set sent-message bubbles, including the common and selected states
[TUIBubbleMessageCellData setOutgoingBubble:[UIImage imageNamed:@"outgoing_bubble"]];
[TUIBubbleMessageCellData setOutgoingHighlightedBubble:[UIImage imageNamed:@"outgoing_bubble_highlighted"]];
// Set received-message bubbles, including the common and selected states
[TUIBubbleMessageCellData setIncommingBubble:[UIImage imageNamed:@"incoming_bubble"]];
[TUIBubbleMessageCellData setIncommingHighlightedBubble:[UIImage imageNamed:@"incoming_bubble_highlighted"]];
```


### Setting bubble margins
In TUIKit, text and voice messages are displayed in bubbles. TUIMessageCellLayout provides a class method bubbleInsets to set bubble margins.
You can customize bubble margins before chat UI initialization. The following is a code sample:
```objectivec
// Set the margins for sent-message bubbles
[TUIMessageCellLayout outgoingTextMessageLayout].bubbleInsets = UIEdgeInsetsMake(20, 20, 24, 24);
// Set the margins for received-message bubbles
[TUIMessageCellLayout incommingTextMessageLayout].bubbleInsets = UIEdgeInsetsMake(20, 20, 24, 24);
```



### Setting the sender's profile photo style
To set the sender's profile photo style, you can modify related properties of TUIMessageCellLayout.
You can customize the profile photo style before chat UI initialization. The following is a code sample:
```objectivec
// Set the sender's profile photo size and position
[TUIMessageCellLayout outgoingTextMessageLayout].avatarSize = CGSizeMake(80, 80);
[TUIMessageCellLayout outgoingTextMessageLayout].avatarInsets = UIEdgeInsetsMake(10, 10, 20, 20);
// Set the receiver's profile photo size and position
[TUIMessageCellLayout incommingTextMessageLayout].avatarSize = CGSizeMake(80, 80);
[TUIMessageCellLayout incommingTextMessageLayout].avatarInsets = UIEdgeInsetsMake(10, 10, 20, 20);
```

> ! For other message types, obtain the corresponding layout instances to set the profile photo sizes and positions.



### Setting the Message Nickname Style
To set the sender's nickname font and color, you can modify related properties of TUIMessageCellLayout.
You can customize the message nickname style before chat UI initialization. The following is a code sample:
```objectivec
// Set the sender's nickname font and color for received messages
[TUIMessageCellData setIncommingNameFont:[UIFont systemFontOfSize:20]];
[TUIMessageCellData setIncommingNameColor:[UIColor blueColor]];
// Set your own nickname font and color. By default, your own nickname is not displayed.
[TUIMessageCellData setOutgoingNameFont:[UIFont systemFontOfSize:20]];
[TUIMessageCellData setOutgoingNameColor:[UIColor purpleColor]];
```
