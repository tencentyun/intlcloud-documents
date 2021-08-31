In TUIChatController, every message is internally stored as TUIMessageCellData or a subclass object. When a user scrolls down the message list, the TUIMessageCellData is converted into TUIMessageCell for display.
You can set the delegate callback of TUIChatController to control specific TUIMessageCell instances to achieve message customization.
The hyperlink custom message in the above red box is an example. As TUIKit does not internally implement this effect, you only need to add two UILabels in container of TUIMessageCell to quickly implement this display effect. This document describes the realization process in detail.

## Customizing Messages
### Step 1: implement a custom `cellData` class
Customize a `cellData` class inherited from `TUIMessageCellData`, to be used for storing displayed texts and links.

```objectivec
@inerface MyCustomCellData : TUIMessageCellData
@property NSString *text;
@property NSString *link;
@end
```

TUIMessageCellData needs to calculate the size of the displayed content, so that TUIChatController can reserve sufficient space to display the message.

```objectivec
@implement MyCustomCellData : TMessageCellData
- (CGSize)contentSize
{
    CGRect rect = [self.text boundingRectWithSize:CGSizeMake(300, MAXFLOAT) options:NSStringDrawingUsesLineFragmentOrigin | NSStringDrawingUsesFontLeading attributes:@{ NSFontAttributeName : [UIFont systemFontOfSize:15] } context:nil];
    CGSize size = CGSizeMake(ceilf(rect.size.width)+1, ceilf(rect.size.height));
    
    // Add bubble margins
    size.height += 60;
    size.width += 20;
    
    return size;
}
@end
```


### Step 2: implement a custom cell class

Customize a cell class inherited from TUIMessageCell.

```objectivec
@interface MyCustomCell : TUIMessageCell
@property UILabel *myTextLabel;
@property UILabel *myLinkLabel;
@end
```

In the implementation file, you need to create the myTextLabel and myLinkLabel objects and add them to the container.

```objectivec
@implementation MyCustomCell

- (instancetype)initWithStyle:(UITableViewCellStyle)style reuseIdentifier:(NSString *)reuseIdentifier
{
    self = [super initWithStyle:style reuseIdentifier:reuseIdentifier];
    if (self) {
        _myTextLabel = [[UILabel alloc] init];
        _myTextLabel.numberOfLines = 0;
        _myTextLabel.font = [UIFont systemFontOfSize:15];
        [self.container addSubview:_myTextLabel];
        
        _myLinkLabel = [[UILabel alloc] initWithFrame:CGRectZero];
        _myLinkLabel.text = @"View details>>";
        _myLinkLabel.font = [UIFont systemFontOfSize:15];
        _myLinkLabel.textColor = [UIColor blueColor];
        [self.container addSubview:_myLinkLabel];
        
        self.container.backgroundColor = [UIColor whiteColor];
        [self.container.layer setMasksToBounds:YES];
        [self.container.layer setBorderColor:[UIColor lightGrayColor].CGColor];
        [self.container.layer setBorderWidth:1];
        [self.container.layer setCornerRadius:5];
    }
    return self;
}

- (void)fillWithData:(MyCustomCellData *)data;
{
    [super fillWithData:data];
    self.customData = data;
    self.myTextLabel.text = data.text;
}

- (void)layoutSubviews
{
    [super layoutSubviews];
    self.myTextLabel.mm_top(10).mm_left(10).mm_flexToRight(10).mm_flexToBottom(50);
    self.myLinkLabel.mm_sizeToFit().mm_left(10).mm_bottom(10);
}
@end
```


### Step 3: register the TUIChatController callback

The purpose of registering the TUIChatController callback is to notify TUIChatController of how to display custom messages. Registering this callback needs to implement the following callbacks:
- When receiving a message, convert V2TIMMessage into TUIMessageCellData objects.
- Before display, convert TUIMessageCellData into TUIMessageCell objects to be used for ultimate display.

```objectivec
@implement MyChatController
- (id)init
{
	self = [super init];
	// Add a listener
	[[TUIKitListenerManager sharedInstance] addChatControllerListener:self];
	// Initialize
	chat = [[TUIChatController alloc] initWithConversation:conversationData]; // conversationData is the current conversation data, including groupID, userID, and so on, which can be obtained from the conversation list
 [self addChildViewController:chat]; // Add the chat interface internally
 // Configure the navigation bar
 ...
    
    return self;
}
// TChatController callback function
- (TUIMessageCellData *)chatController:(TUIChatController *)controller onNewMessage:(V2TIMMessage *)msg
{
    if (msg.elemType == V2TIM_ELEM_TYPE_CUSTOM) {
        MyCustomCellData *cellData = [[MyCustomCellData alloc] initWithDirection:msg.isSelf ? MsgDirectionOutgoing : MsgDirectionIncoming];
        cellData.text = @"View details>>";
        cellData.link = @"https://cloud.tencent.com/product/im";
        return cellData;
    }
    return nil
}

- (TUIMessageCell *)chatController:(TUIChatController *)controller onShowMessageData:(TUIMessageCellData *)data
{
    if ([data isKindOfClass:[MyCustomCellData class]]) {
        MyCustomCell *myCell = [[MyCustomCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:@"MyCell"];
        [myCell fillWithData:(MyCustomCellData *)data];
        return myCell;
    }
    return nil
}

@end
```


## Sending Custom Messages

TUIChatController provides an API for sending messages. Users can use code to control message sending. The type of a custom message must be inherited from TUIMessageCellData. For example, to send a text message, you can create a TUITextMessageCellData object.
To send custom data, you need to initialize the innerMessage attribute. Please refer to the following code:

```objectivec
MyCustomCellData *cellData = [[MyCustomCellData alloc] initWithDirection:MsgDirectionOutgoing];       
cellData.innerMessage = [[V2TIMManager sharedInstance] createCustomMessage:data]; // Data is custom binary data
[chatController sendMessage:cellData];
```


