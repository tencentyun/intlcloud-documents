
## Modifying the Profile Photo

### Modifying the default profile photo

To display a user, TUIKit reads the profile photo URL from the user profile and displays if. If the user does not set the profile photo, the default profile photo is displayed.

You can use a custom image as the default profile photo.
```objectivec
TUIKitConfig *config = [TUIKitConfig defaultConfig]; 
// Modify the default profile photo
config.defaultAvatarImage = [UIImage imageNamed:@"Your Image"];
// Modify the default group profile photo
config.defaultGroupAvatarImage = [UIImage imageNamed:@"Your Image"];
```


### Modifying the profile photo type

Three types of profile photos are available: rectangle, round, and rounded rectangle.

```objectivec
typedef NS_ENUM(NSInteger, TUIKitAvatarType) {
    TAvatarTypeNone,             /*Rectangle profile photo*/
    TAvatarTypeRounded,          /*Round profile photo*/
    TAvatarTypeRadiusCorner,     /*Rounded rectangle profile photo*/
};
```

You can modify the profile photo type in the same way as modifying the profile photo. The sample code is as follows:

```objectivec
TUIKitConfig *config = [TUIKitConfig defaultConfig]; 
// Set the profile photo type to rounded rectangle, with a corner radius of 5
config.avatarType = TAvatarTypeRadiusCorner;
config.avatarCornerRadius = 5.f;
```


## Configuring the Chat Interface

The chat interface has the following views:
![](https://main.qcloudimg.com/raw/391d26b927660d99eec807ec1fe84c3b.png)

```objectivec
TUIChatController *vc = ...; // Obtain the chat interface object
vc.messageController.view.backgroundColor = [UIColor greenColor];
```



### Configuring messages

#### Setting the bubble image

The image displayed in the bubble cell is obtained from TUIBubbleMessageCellData, which provides class methods to set images.

```objectivec
// Set the sender bubble, which can be in the normal or highlighted state. The receiver bubble can be set in the same way.
[TUIBubbleMessageCellData setOutgoingBubble:[UIImage imageNamed:@"bubble"]];
[TUIBubbleMessageCellData setOutgoingHighlightedBubble:[UIImage imageNamed:@"bubble_highlight"]];
```


#### Setting bubble margins

In TUIKit, text and audio messages are displayed in bubbles. TUIMessageCellLayout provides class methods to set bubbleInsets.

```objectivec
// Set the margins of the sender bubble. The recipient bubble can be set in the same way.
[TUIMessageCellLayout outgoingTextMessageLayout].bubbleInsets = UIEdgeInsetsMake(10, 10, 20, 20);
```


#### Modifying the message font and color

The data of text messages comes from the TUITextMessageCellData class, which provides APIs to modify the font and color of text messages.

```objectivec
// Set the font and color of text messages for the sender. The recipient’s text messages can be set in the same way.
[TUITextMessageCellData setOutgoingTextFont:[UIFont systemFontOfSize:20]];
[TUITextMessageCellData setOutgoingTextColor:[UIColor redColor]];
```


### Configuring the profile photo

A profile photo is a common element to each message and is also part of layout configuration. You can change the profile photo style for all messages by modifying TUIMessageCellLayout.

#### Setting the profile photo size

```objectivec
// Set the profile photo size for the sender. The recipient’s profile photo can be set in the same way.
[TUIMessageCellLayout outgoingMessageLayout].avatarSize = CGSizeMake(100, 100);
```


#### Setting the profile photo location

```objectivec
// Set the profile photo location for the sender. The recipient’s profile photo location can be set in the same way.
[TUIMessageCellLayout outgoingMessageLayout].avatarInsets = UIEdgeInsetsMake(10, 10, 20, 20);
```


### Setting the nickname font and color

Set the nickname font and color by modifying TUIMessageCellLayout properties in the same way as setting the profile photo location.

```objectivec
// Set the nickname font for incoming messages. You can set the nickname font for outgoing messages in the same way, but it is not displayed by default.
[TUIMessageCellData setIncommingNameFont:[UIFont systemFontOfSize:20]];
[TUIMessageCellData setOutgoingTextColor:[UIColor redColor]];
```


## Configuring the More Menu

Clicking the "+" button in the input area opens the More menu. By default, the More menu displays 4 options. You can configure the More menu through the moreMenus property of TUIChatController.
The sample code for deleting the File option is as follows:

```objectivec
TUIChatController *vc = [[TUIChatController alloc] initWithConversation:conv];
NSMutableArray *array = [NSMutableArray arrayWithArray:vc.moreMenus]; 
[array removeLastObject]; // Delete the last option
vc.moreMenus = array; // Reset the property, and the change takes effect immediately
```


When the user clicks a button in the menu, TUIChatController notifies the upper layer of this through a callback event.
>When the user clicks the default menu, a callback notification will be sent, and you can ignore it.


