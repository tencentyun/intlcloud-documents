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
> You can disable the display of the 3 x 3 grid consisting of group members' profile photos as needed.

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

The display effects of round profile photos are as follows:
<table style="text-align:center;vertical-align:middle;width: 600px">
  <tr>
    <th style="text-align:center;" width="300px">Conversation List</th>
    <th style="text-align:center;" width="300px">Message</th>
  </tr>
  <tr>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/c03049d9f8e4df5f78d8f0d26f629e11.jpg"  />    </td>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/20ad8d1dc817e7d2f7f8d50ce5b602e6.jpg" />     </td>
	 </tr>
</table>

The display effects of profile photos being rectangles with rounded corners are as follows:
<table style="text-align:center;vertical-align:middle;width: 600px">
  <tr>
    <th style="text-align:center;" width="300px">Conversation List</th>
    <th style="text-align:center;" width="300px">Message</th>
  </tr>
  <tr>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/087a637bc8a8f0d6da4d3254b53fc6d8.jpg"  />    </td>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/4774c0c89b66d6b3d370271f98865e07.jpg" />     </td>
	 </tr>
</table>

## Setting the Chat UI Styles

### Setting the chat UI background color
You can customize chat UI background color before TUIKit initialization. The following is a code sample:
```objectivec
[TUIChatConfig defaultConfig].backgroudColor = [UIColor greenColor];
```
The display effects of different chat UI background colors are as follows:
<table style="text-align:center;vertical-align:middle;width: 600px">
  <tr>
    <th style="text-align:center;" width="300px">Default Color</th>
    <th style="text-align:center;" width="300px">Custom Color</th>
  </tr>
  <tr>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/05bbfe937a5761c64155a3770a715470.jpg"  />    </td>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/4625f25ed5b2994517f698524b2bf905.jpg" />     </td>
	 </tr>
</table>

### Setting the chat UI background image
You can customize chat UI background image before TUIKit initialization. The following is a code sample:
```objectivec
[TUIChatConfig defaultConfig].backgroudImage = [UIImage imageNamed:@"your chat background image"];
```
The display effects of different chat UI background images are as follows:
<table style="text-align:center;vertical-align:middle;width: 600px">
  <tr>
    <th style="text-align:center;" width="300px">Default Background</th>
    <th style="text-align:center;" width="300px">Custom Background</th>
  </tr>
  <tr>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/05bbfe937a5761c64155a3770a715470.jpg"  />    </td>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/69339461044cccfc4c51b6663032b245.jpg" />     </td>
	 </tr>
</table>



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
The display effects of different message fonts and colors are as follows:
<table style="text-align:center;vertical-align:middle;width: 600px">
  <tr>
    <th style="text-align:center;" width="300px">Default Fonts and Colors</th>
    <th style="text-align:center;" width="300px">Custom Fonts and Colors</th>
  </tr>
  <tr>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/b34575d82aab9fb6e9a2f11732b2e55f.jpg"  />    </td>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/15865f75a5bf49f3aa298272439c52c5.jpg" />     </td>
	 </tr>
</table>


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
The display effects of different bubble background images are as follows:
<table style="text-align:center;vertical-align:middle;width: 600px">
  <tr>
    <th style="text-align:center;" width="300px">Default Image</th>
    <th style="text-align:center;" width="300px">Custom Image</th>
  </tr>
  <tr>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/970feb804e27d62b0d0605716f04b5cf.jpg"  />    </td>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/06208b5236c7574a10a48d5ac3c924ae.jpg" />     </td>
	 </tr>
</table>

### Setting bubble margins
In TUIKit, text and voice messages are displayed in bubbles. TUIMessageCellLayout provides a class method bubbleInsets to set bubble margins.
You can customize bubble margins before chat UI initialization. The following is a code sample:
```objectivec
// Set the margins for sent-message bubbles
[TUIMessageCellLayout outgoingTextMessageLayout].bubbleInsets = UIEdgeInsetsMake(20, 20, 24, 24);
// Set the margins for received-message bubbles
[TUIMessageCellLayout incommingTextMessageLayout].bubbleInsets = UIEdgeInsetsMake(20, 20, 24, 24);
```

The display effects of different bubble margins are as follows:
<table style="text-align:center;vertical-align:middle;width: 600px">
  <tr>
    <th style="text-align:center;" width="300px">Default Margins</th>
    <th style="text-align:center;" width="300px">Extended Margins</th>
  </tr>
  <tr>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/b34575d82aab9fb6e9a2f11732b2e55f.jpg"  />    </td>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/c84497cd77803883aa652c53eab91ca9.jpg" />     </td>
	 </tr>
</table>


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

The display effects of different sender profile photos are as follows:
<table style="text-align:center;vertical-align:middle;width: 600px">
  <tr>
    <th style="text-align:center;" width="300px">Default Profile Photo insets</th>
    <th style="text-align:center;" width="300px">Custom Profile Photo insets</th>
  </tr>
  <tr>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/c71fb217070342316289c6a41ec41b9a.jpg"  />    </td>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/2cbef1dd982d5fc07486d75d2c5bb847.jpg" />     </td>
	 </tr>
</table>

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

The display effects of different nickname styles for messages are as follows:
<table style="text-align:center;vertical-align:middle;width: 600px">
  <tr>
    <th style="text-align:center;" width="300px">Default Styles</th>
    <th style="text-align:center;" width="300px">Custom Styles</th>
  </tr>
  <tr>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/91badb4d77b9cbe243148735e1d86f2d.jpg"  />    </td>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/54a86c9e41b285c43adcbf1b9c455f0e.jpg" />     </td>
	 </tr>
</table>


