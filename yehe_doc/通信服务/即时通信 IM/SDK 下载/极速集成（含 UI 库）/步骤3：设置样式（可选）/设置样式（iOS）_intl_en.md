This document describes how to set styles on iOS.

## Modifying the Profile Photo

### Modifying the default profile photo

To display a user on the interface, TUIKit reads the profile photo URL from the user’s profile and displays the profile photo. If the user has not set a profile photo, the default profile photo is displayed.

You can set a custom image as the default profile photo.
```objectivec
TUIKitConfig *config = [TUIKitConfig defaultConfig]; 
// Modify the default profile photo
config.defaultAvatarImage = [UIImage imageNamed:@"Your Image"];
// Modify the default group profile photo
config.defaultGroupAvatarImage = [UIImage imageNamed:@"Your Image"];
```


### Modifying the profile photo type

There are three profile photo types available: rectangle, rounded, and rounded rectangle.

```objectivec
typedef NS_ENUM(NSInteger, TUIKitAvatarType) {
    TAvatarTypeNone,             /*Rectangle profile photo*/
    TAvatarTypeRounded,          /*Rounded profile photo*/
    TAvatarTypeRadiusCorner,     /*Rounded rectangle profile photo*/
};
```

You can modify the profile photo type in the same way you modify the default profile photo. The following is a code sample:

```objectivec
TUIKitConfig *config = [TUIKitConfig defaultConfig]; 
// Set rounded rectangle profile photo, with a corner radius of 5
config.avatarType = TAvatarTypeRadiusCorner;
config.avatarCornerRadius = 5.f;
```


## Configuring the Chat Interface

The following figure shows how different views are arranged on the chat interface:
![](https://main.qcloudimg.com/raw/391d26b927660d99eec807ec1fe84c3b.png)

### Setting the chat interface background
```objectivec
TUIChatController *vc = ...; // Get the chat interface object.
vc.messageController.view.backgroundColor = [UIColor greenColor];
```

### Configuring messages

#### Setting bubble images

The images displayed in the bubble cells are obtained from TUIBubbleMessageCellData, which provides class methods to set the images.

```objectivec
// Set the outgoing bubble, which can be in normal status or highlighted status. The incoming bubble is set in the same way.
[TUIBubbleMessageCellData setOutgoingBubble:[UIImage imageNamed:@"bubble"]];
[TUIBubbleMessageCellData setOutgoingHighlightedBubble:[UIImage imageNamed:@"bubble_highlight"]];
```


#### Setting bubble margins

In TUIKit, text and audio messages are displayed in bubbles. TUIMessageCellLayout provides class methods to set bubbleInsets.

```objectivec
// Set the margins of the outgoing bubble. The incoming bubble is set in the same way.
[TUIMessageCellLayout outgoingTextMessageLayout].bubbleInsets = UIEdgeInsetsMake(10, 10, 20, 20);
```


#### Modifying the message font and color

The data of text messages comes from the TUITextMessageCellData class, through whose APIs you can modify the font and color of text messages.

```objectivec
// Set the font and color of outgoing text messages. The incoming text messages are set in the same way.
[TUITextMessageCellData setOutgoingTextFont:[UIFont systemFontOfSize:20]];
[TUITextMessageCellData setOutgoingTextColor:[UIColor redColor]];
```


### Configuring the profile photo

A profile photo is a common element to every message. To set the size and position of the profile photo, you need to first obtain the `layout` instance of the message. Take a text message as an example:

#### Setting the profile photo size

```objectivec
// Set profile photo size for the sender. The receiver’s profile photo is set in the same way.
[TUIMessageCellLayout outgoingMessageLayout].avatarSize = CGSizeMake(100, 100);
```


#### Setting the profile photo location

```objectivec
// Set the profile photo location for the sender. The receiver’s profile photo is set in the same way.
[TUIMessageCellLayout outgoingTextMessageLayout].avatarInsets = UIEdgeInsetsMake(10, 10, 20, 20);
```

For other messages, obtain their `layout` instances to set the size and position of the profile photos.


### Configuring the nickname font and color

Set the nickname font and color by modifying related properties in TUIMessageCellLayout in the same way the profile photo location is set.

```objectivec
// Set the nickname font for the receiver. The sender’s nickname is set in the same way, but it is not displayed by default.
[TUIMessageCellData setIncommingNameFont:[UIFont systemFontOfSize:20]];
[TUIMessageCellData setIncommingNameColor:[UIColor redColor]];
```


## Configuring the More Menu

Clicking the "+" button next to the input box opens the More panel. By default, the More panel displays 4 options. You can add or delete options by modifying the moreMenus property in TUIChatController.
The following is a code sample to delete the File option:

```objectivec
TUIChatController *vc = [[TUIChatController alloc] initWithConversation:conv];
NSMutableArray *array = [NSMutableArray arrayWithArray:vc.moreMenus]; 
[array removeLastObject]; // Delete the last menu
vc.moreMenus = array; // Reset the property and apply it immediately
```


When the user clicks a button in the menu, TUIChatController notifies the upper layer with a callback event.
>?When the user clicks the default menu, you are also notified by a callback, but you do not need to process it.


