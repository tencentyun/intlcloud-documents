In TUIChatController, each message is stored as a TUIMessageCellData or subclass object. When the message list is scrolled, TUIMessageCellData objects are converted to TUIMessageCell objects for display.
You can customize messages by setting the TUIChatController callback delegate to control specific TUIMessageCell instances.
![](https://main.qcloudimg.com/raw/77082a09b210baae30e41ce35e07af6b.png)
Take the custom hyperlink message in the red box as an example. As TUIKit does not implement this effect internally, you need to add two UILabels to the container of TUIMessageCell. This document guides you through the implementation process:

## Custom Messages
### Step 1: Implement a custom cellData class
Customize a `cellData` class that is inherited from `TUIMessageCellData` to store the text and link to be displayed.

```objectivec
@inerface MyCustomCellData : TUIMessageCellData
@property NSString *text;
@property NSString *link;
@end
```

TUIMessageCellData calculates the size of the content to be displayed so that TUIChatController can reserve enough space for this.

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


### Step 2: Implement a custom cell class

Customize a cell class that is inherited from TUIMessageCell.

```objectivec
@interface MyCustomCell : TUIMessageCell
@property UILabel *myTextLabel;
@property UILabel *myLinkLabel;
@end
```

You need to create the myTextLabel and myLinkLabel objects in the implementation file and add them to a container.

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
        _myLinkLabel.text = @"Learn more >>";
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


### Step 3: Register the TUIChatController callback

Register the TUIChatController callback to instruct TUIChatController how to display custom messages. Register this callback to implement the following:
- When a message arrives, convert the TIMessage object to a TUIMessageCellData object.
- Convert the TUIMessageCellData object to a TUIMessageCell object to display the final result.

```objectivec
@implement MyChatController
- (id)init
{
	self = [super init];
	// Initialize
    TIMConversation *conv = [[TIMManager sharedInstance] getConversation:TIM_C2C receiver:@"test"];
	chat = [[TUIChatController alloc] initWithConversation:conv];
    [self addChildViewController:chat]; // Add the chat interface
    chat.delegate = self;// Set the callback
    // Configure the navigation bar
    ...
    
    return self;
}
// TChatController Callback function
- (TUIMessageCellData *)chatController:(TUIChatController *)controller onNewMessage:(TIMMessage *)msg
{
    TIMElem *elem = [msg getElem:0];
    if([elem isKindOfClass:[TIMCustomElem class]]){
        MyCustomCellData *cellData = [[MyCustomCellData alloc] initWithDirection:msg.isSelf ? MsgDirectionOutgoing : MsgDirectionIncoming];
        cellData.text = @"Learn more >>";
        cellData.link = @"https://cloud.tencent.com/product/im";
        return cellData;
    }
    return nil;
}

- (TUIMessageCell *)chatController:(TUIChatController *)controller onShowMessageData:(TUIMessageCellData *)data
{
    if ([data isKindOfClass:[MyCustomCellData class]]) {
        MyCustomCell *myCell = [[MyCustomCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:@"MyCell"];
        [myCell fillWithData:(MyCustomCellData *)data];
        return myCell;
    }
    return nil;
}

@end
```


## Sending Custom Messages

TUIChatController provides APIs to send messages, and the user controls the sending operation through code. Custom messages must be inherited from TUIMessageCellData. For example, to send a text message, you need to create a TUITextMessageCellData object.
To send custom data, you need to initialize innerMessage properties. For more information, see [Custom Messages](https://cloud.tencent.com/document/product/269/9150#.E8.87.AA.E5.AE.9A.E4.B9.89.E6.B6.88.E6.81.AF.E5.8F.91.E9.80.81).

```objectivec
MyCustomCellData *cellData = [[MyCustomCellData alloc] initWithDirection:MsgDirectionOutgoing];       
cellData.innerMessage = [[TIMMessage alloc] init];
TIMCustomElem * custom_elem = [[TIMCustomElem alloc] init];
[cellData.innerMessage addElem:custom_elem];
[chatController sendMessage:cellData];
```

