TUIKit implements the sending and display for basic message types such as text, image, voice, video, and file messages by default. If these message types do not meet your requirements, you can add custom message types.

## Basic Message Types
<table>
     <tr>
         <th width="20%" style="text-align:center">Message Type</th>  
         <th style="text-align:center">Renderings</th>  
     </tr>
     <tr>      
         <td style="text-align:center">Text message</td>   
     <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/9c9806e98fdf7de1763042463f504ab0.png" width="320"/></td>   
     </tr> 
     <tr>      
         <td style="text-align:center">Image message</td>   
     <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/aa32a1838b2e2cf021442658f24c6c2b.png" width="320"/></td>   
     </tr> 
     <tr>      
         <td style="text-align:center">Voice message</td>   
     <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/cb3342026953a3294c3c24686a2a642f.png" width="320"/></td>   
     </tr> 
     <tr>      
         <td style="text-align:center">Video message</td>   
     <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/6eea956715e88d12f6942e57e9ba2660.png" width="320"/></td>   
     </tr> 
     <tr>      
         <td style="text-align:center">File message</td>   
     <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/75d71e975b0c2820cda58a293b356826.png" width="320"/></td>   
     </tr> 
</table>


## Custom Message
- If the basic message types do not meet your requirements, you can customize messages as needed.
- This document uses sending a custom hypertext message that can redirect to the browser as an example to help you quickly understand the implementation process. **In this document, version 5.8.1668 is used as an example, which is different from previous versions.**
![](https://qcloudimg.tencent-cloud.cn/raw/ccd1537415821a33b0c860a22d92f830.png)
 The figure above shows a custom message that can be clicked to redirect to a specified linked address. The following describes the implementation details.

## How to Receive and Display a Custom Message
<img src="https://qcloudimg.tencent-cloud.cn/raw/156b57068a297b308a4bf66fdb9daeff.png" width = "500"/>

You can receive a custom message via the `onRecvNewMessage` function in [TUIMessageDataProvider.m](https://github.com/tencentyun/TIMSDK/blob/master/iOS/TUIKit/TUIChat/DataProvider/TUIMessageDataProvider.m), and the received custom message will be displayed in `Cell` mode in the message list. The data required for `Cell` drawing is called `CellData`. The following introduces how to display a custom message.

### Step 1. Create custom CellData
1. Create the [TUILinkCellData.h](https://github.com/tencentyun/TIMSDK/blob/master/iOS/TUIKit/TUIChat/Cell/CellData/Custom/TUILinkCellData.h) and [TUILinkCellData.m](https://github.com/tencentyun/TIMSDK/blob/master/iOS/TUIKit/TUIChat/Cell/CellData/Custom/TUILinkCellData.m) files in `TUIChat -> Cell -> CellData -> Custom`. Inherit data from `TUIMessageCellData` to `CellData` to store the text to display and the link to redirect.
```java
@interface TUILinkCellData : TUIMessageCellData
@property NSString *text;
@property NSString *link;
@end
```
2. Rewrite the `getCellData:` method of the parent class to convert `V2TIMMessage` to the drawing data `TUILinkCellData` of the message list `Cell`.
```java
@implementation TUILinkCellData
+ (TUIMessageCellData *)getCellData:(V2TIMMessage *)message{
    NSDictionary *param = [NSJSONSerialization JSONObjectWithData:message.customElem.data options:NSJSONReadingAllowFragments error:nil];
    TUILinkCellData *cellData = [[TUILinkCellData alloc] initWithDirection:message.isSelf ? MsgDirectionOutgoing : MsgDirectionIncoming];
    cellData.innerMessage = message;
    cellData.msgID = message.msgID;
    cellData.text = param[@"text"];
    cellData.link = param[@"link"];
    cellData.avatarUrl = [NSURL URLWithString:message.faceURL];
    return cellData;
}
@end
```
3. Rewrite the `getDisplayString:` method of the parent class to convert `V2TIMMessage` to the `lastMsg` display text information of the conversation list.
![](https://qcloudimg.tencent-cloud.cn/raw/1555df533bc3a105b4a7f5e7676e1c83.png)
```java
@implementation TUILinkCellData
+ (NSString *)getDisplayString:(V2TIMMessage *)message {
    NSDictionary *param = [NSJSONSerialization JSONObjectWithData:message.customElem.data options:NSJSONReadingAllowFragments error:nil];
    return param[@"text"];
}
@end
```
4. Rewrite the `contentSize:` method of the parent class to calculate the size of the drawing area occupied by the `cellData` content.
```java
- (CGSize)contentSize
{
    CGRect rect = [self.text boundingRectWithSize:CGSizeMake(300, MAXFLOAT) options:NSStringDrawingUsesLineFragmentOrigin | NSStringDrawingUsesFontLeading attributes:@{ NSFontAttributeName : [UIFont systemFontOfSize:15] } context:nil];
    CGSize size = CGSizeMake(ceilf(rect.size.width)+1, ceilf(rect.size.height));
    // Add bubble margins
    size.height += 60;
    size.width += 20;
    return size;
}
```

### Step 2. Create custom Cell
1. Create the [TUILinkCell.h](https://github.com/tencentyun/TIMSDK/blob/master/iOS/TUIKit/TUIChat/Cell/CellUI/Custom/TUILinkCell.h) and [TUILinkCell.m](https://github.com/tencentyun/TIMSDK/blob/master/iOS/TUIKit/TUIChat/Cell/CellUI/Custom/TUILinkCell.m) files in `TUIChat -> Cell -> CellUI -> Custom`. Inherit data from `TUIMessageCell` to `Cell` to draw `TUILinkCellData` data.
```java
@interface TUILinkCell : TUIMessageCell
@property UILabel *myTextLabel;  // Display text
@property UILabel *myLinkLabel;  // Link redirection text
- (void)fillWithData:(TUILinkCellData *)data; // Draw UI
@end
```
2. Rewrite the `initWithStyle:` method of the parent class to create the `myTextLabel` and `myLinkLabel` text display objects and add them to `container`.
```java
@implementation TUILinkCell
// Initialize the control
- (instancetype)initWithStyle:(UITableViewCellStyle)style reuseIdentifier:(NSString *)reuseIdentifier
{
    self = [super initWithStyle:style reuseIdentifier:reuseIdentifier];
    if (self) {
        self.myTextLabel = [[UILabel alloc] init];
        [self.container addSubview:self.myTextLabel];
        self.myLinkLabel = [[UILabel alloc] init];
        self.myLinkLabel.text = @"View details>>";
        [self.container addSubview:_myLinkLabel];
    }
    return self;
}
@end
```
3. Rewrite the `fillWithData:` method of the parent class to custom `TUILinkCellData` data display in `TUILinkCell`.
```java
@implementation TUILinkCell
// Draw the cell based on `cellData`
- (void)fillWithData:(TUILinkCellData *)data;
{
    [super fillWithData:data];
    self.myTextLabel.text = data.text;
}
@end
```
4. Rewrite the `layoutSubviews` method of the parent class to custom the control coordinates.
```java
// Set the control coordinates
- (void)layoutSubviews
{
    [super layoutSubviews];
    self.myTextLabel.mm_top(10).mm_left(10).mm_flexToRight(10).mm_flexToBottom(50);
    self.myLinkLabel.mm_sizeToFit().mm_left(10).mm_bottom(10);
}
@end
```

### Step 3. Register the custom Cell and CellData
After `cell` and `cellData` are created, you need to register the `cell` and `cellData` information in the `load` function in [TUIMessageDataProvider.m](https://github.com/tencentyun/TIMSDK/blob/master/iOS/TUIKit/TUIChat/DataProvider/TUIMessageDataProvider.m). After the registration is completed, when a message is received, the message list automatically finds the corresponding `cellData` to process message data based on `businessID`. When refreshing the UI, the message list will also automatically create the corresponding `Cell` to draw `cellData` data based on `businessID`.
```java
@implementation TUIMessageDataProvider
+ (void)load {
    // You need to implement the following code yourself
    customMessageInfo = @[@{@"businessID" : @"custom_message_link",  // Unique ID of the custom message (Duplicated IDs are not allowed.)
                            @"cell_name" :  @"TUILinkCell"           // cell class name
                            @"cell_data_name" : @"TUILinkCellData"   // cellData class name
                          },
                          // If you need more custom message types, you can continue to add custom message information below
                          @{@"businessID" : @"custom_message_link2",
                            @"cell_name" : @"TUILinkCell2"          
                            @"cell_data_name" : @"TUILinkCellData2"
                          }];
}
@end
```

## How to Send a Custom Message
 <img src="https://qcloudimg.tencent-cloud.cn/raw/e7c26ad63941fb2bc3fb8277bf037ac4.png" width = "500"/>
	
As the figure above shows, the custom message sending button consists of the text `title` and image `image`. You can register the button using the `load` function in [TUIChatDataProvider.m](https://github.com/tencentyun/TIMSDK/blob/master/iOS/TUIKit/TUIChat/DataProvider/TUIChatDataProvider.m).

```java
@implementation TUIChatDataProvider
+ (void)load {
    // You need to implement the following code yourself
    customButtonInfo = @[@{@"SendBtn_Key" : @"custom_link_btn",  // Unique ID of the button
                           @"SendBtn_Title" :  @"Custom"          // Text information of the button
                           @"SendBtn_ImageName" : @"custom_link_image"   // Image name of the button
                          }];
}
@end
```

You can create a custom message to be sent when the button is clicked by calling the [createCustomMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a7a38c42f63a4e0c9e89f6c56dd0da316) API in the `didSelectMoreCell` callback in [TUIC2CChatViewController.m](https://github.com/tencentyun/TIMSDK/blob/master/iOS/TUIKit/TUIChat/UI/Chat/TUIC2CChatViewController.m). In the configuration, the `data` parameter can be comprised of `json` data. You can define a `businessID` field in the `json` data to uniquely identify the message.

```java
@implementation TUIMessageController
- (void)inputController:(TUIInputController *)inputController didSelectMoreCell:(TUIInputMoreCell *)cell
{
    if ([cell.data.key isEqualToString:@"custom_link_btn"]) { 
        // Create the custom message and set the message `businessID`, display text, and redirection link (you need to implement the following code yourself)
        NSString *businessID = @"custom_message_link";
        NSString *text = @"Welcome to Tencent Cloud IM group";
        NSString *link = @"https://cloud.tencent.com/document/product/269/3794";
        NSDictionary *param = @{@"businessID": businessID, @"text":text, @"link":link};
        NSData *data = [NSJSONSerialization dataWithJSONObject:param options:0 error:&error];
        V2TIMMessage *message = [[V2TIMManager sharedInstance] createCustomMessage:data];
        [self sendMessage:message];
    }
}
@end
```
