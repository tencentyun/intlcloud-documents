TUIKit 默认实现了文本、图片、语音、视频、文件等基本消息类型的发送和展示，如果这些消息类型满足不了您的需求，您可以新增自定义消息类型。

## 基本消息类型
<table>
     <tr>
         <th width="20%" style="text-align:center">消息类型</th>  
         <th style="text-align:center">显示效果图</th>  
     </tr>
     <tr>      
         <td style="text-align:center">文本类消息</td>   
     <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/9c9806e98fdf7de1763042463f504ab0.png" width="320"/></td>   
     </tr> 
     <tr>      
         <td style="text-align:center">图片类消息</td>   
     <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/aa32a1838b2e2cf021442658f24c6c2b.png" width="320"/></td>   
     </tr> 
     <tr>      
         <td style="text-align:center">语音类消息</td>   
     <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/cb3342026953a3294c3c24686a2a642f.png" width="320"/></td>   
     </tr> 
     <tr>      
         <td style="text-align:center">视频类消息</td>   
     <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/6eea956715e88d12f6942e57e9ba2660.png" width="320"/></td>   
     </tr> 
     <tr>      
         <td style="text-align:center">文件类消息</td>   
     <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/75d71e975b0c2820cda58a293b356826.png" width="320"/></td>   
     </tr> 
</table>


## 自定义消息
- 如果基本消息类型不能满足您的需求，您可以根据实际业务需求自定义消息。
- 本文以发送一条可跳转至浏览器的超文本作为自定义消息为例，帮助您快速了解实现流程。**本文以5.8.1668版本为例，与之前版本有所不同。**
![](https://qcloudimg.tencent-cloud.cn/raw/ccd1537415821a33b0c860a22d92f830.png)
 上图自定义消息类型可以实现点击后跳转到指定链接地址，具体实现请参考后文。

## 如何接收和展示自定义消息
<img src="https://qcloudimg.tencent-cloud.cn/raw/156b57068a297b308a4bf66fdb9daeff.png" width = "500"/>

您可以在 [TUIMessageDataProvider.m](https://github.com/tencentyun/TIMSDK/blob/master/iOS/TUIKit/TUIChat/DataProvider/TUIMessageDataProvider.m) 的 `onRecvNewMessage` 函数内接收自定义消息，收到的自定义消息最终会以 `Cell` 的形式展示在消息列表中，`Cell` 绘制所需的数据我们称之为 `CellData` ，下面我们分步骤讲解下如何展示自定义消息。

### 步骤一：创建自定义 CellData
1. 在 `TUIChat -> Cell -> CellData -> Custom` 文件夹下新建  [TUILinkCellData.h](https://github.com/tencentyun/TIMSDK/blob/master/iOS/TUIKit/TUIChat/Cell/CellData/Custom/TUILinkCellData.h) 和 [TUILinkCellData.m](https://github.com/tencentyun/TIMSDK/blob/master/iOS/TUIKit/TUIChat/Cell/CellData/Custom/TUILinkCellData.m) 文件，继承自`TUIMessageCellData` ，用于存储显示的文字和跳转的链接。
```java
@interface TUILinkCellData : TUIMessageCellData
@property NSString *text;
@property NSString *link;
@end
```
2. 重写父类的 `getCellData:` 方法，用于把 `V2TIMMessage` 转换成消息列表 `Cell` 的绘制数据 `TUILinkCellData`。
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
3. 重写父类的 `getDisplayString：` 方法，用于把 `V2TIMMessage` 转换成会话列表 `lastMsg` 的展示文本信息。
![](https://qcloudimg.tencent-cloud.cn/raw/1555df533bc3a105b4a7f5e7676e1c83.png)
```java
@implementation TUILinkCellData
+ (NSString *)getDisplayString:(V2TIMMessage *)message {
    NSDictionary *param = [NSJSONSerialization JSONObjectWithData:message.customElem.data options:NSJSONReadingAllowFragments error:nil];
    return param[@"text"];
}
@end
```
4. 重写父类的 `contentSize：` 方法，用于计算 `cellData` 内容所占绘制区域的大小。
```java
- (CGSize)contentSize
{
    CGRect rect = [self.text boundingRectWithSize:CGSizeMake(300, MAXFLOAT) options:NSStringDrawingUsesLineFragmentOrigin | NSStringDrawingUsesFontLeading attributes:@{ NSFontAttributeName : [UIFont systemFontOfSize:15] } context:nil];
    CGSize size = CGSizeMake(ceilf(rect.size.width)+1, ceilf(rect.size.height));
    // 加上气泡边距
    size.height += 60;
    size.width += 20;
    return size;
}
```

### 步骤二：创建自定义 Cell
1. 在 `TUIChat -> Cell -> CellUI -> Custom` 文件夹下新建 [TUILinkCell.h](https://github.com/tencentyun/TIMSDK/blob/master/iOS/TUIKit/TUIChat/Cell/CellUI/Custom/TUILinkCell.h) 和 [TUILinkCell.m](https://github.com/tencentyun/TIMSDK/blob/master/iOS/TUIKit/TUIChat/Cell/CellUI/Custom/TUILinkCell.m) 文件，继承自 `TUIMessageCell` ，用于绘制 `TUILinkCellData` 数据。
```java
@interface TUILinkCell : TUIMessageCell
@property UILabel *myTextLabel;  // 展示文本
@property UILabel *myLinkLabel;  // 链接跳转文本
- (void)fillWithData:(TUILinkCellData *)data; // 绘制 UI
@end
```
2. 重写父类 `initWithStyle:` 方法，创建 `myTextLabel` 和 `myLinkLabel` 文本展示对象，并添加至 `container` 容器。
```java
@implementation TUILinkCell
// 初始化控件
- (instancetype)initWithStyle:(UITableViewCellStyle)style reuseIdentifier:(NSString *)reuseIdentifier
{
    self = [super initWithStyle:style reuseIdentifier:reuseIdentifier];
    if (self) {
        self.myTextLabel = [[UILabel alloc] init];
        [self.container addSubview:self.myTextLabel];
        self.myLinkLabel = [[UILabel alloc] init];
        self.myLinkLabel.text = @"查看详情>>";
        [self.container addSubview:_myLinkLabel];
    }
    return self;
}
@end
```
3. 重写父类 `fillWithData:` 方法，在 `TUILinkCell` 中自定义展示 `TUILinkCellData` 数据。
```java
@implementation TUILinkCell
// 根据 cellData 绘制 cell
- (void)fillWithData:(TUILinkCellData *)data;
{
    [super fillWithData:data];
    self.myTextLabel.text = data.text;
}
@end
```
4. 重写父类 `layoutSubviews` 方法，自定义控件的坐标。
```java
// 设置控件坐标
- (void)layoutSubviews
{
    [super layoutSubviews];
    self.myTextLabel.mm_top(10).mm_left(10).mm_flexToRight(10).mm_flexToBottom(50);
    self.myLinkLabel.mm_sizeToFit().mm_left(10).mm_bottom(10);
}
@end
```

### 步骤三：注册自定义 Cell  和 CellData
当 `cell` 和 `cellData` 创建完成后，需要您在 [TUIMessageDataProvider.m](https://github.com/tencentyun/TIMSDK/blob/master/iOS/TUIKit/TUIChat/DataProvider/TUIMessageDataProvider.m) 的 `load` 函数里主动注册 `cell` 和 `cellData` 信息，注册完成后，消息列表在收到消息时会根据 `businessID` 自动找到对应的 `cellData` 处理消息数据，消息列表在刷新 UI 的时候，也会根据 `businessID` 自动创建对应 `Cell` 绘制 `cellData` 数据。
```java
@implementation TUIMessageDataProvider
+ (void)load {
    // 以下代码需要您自己实现
    customMessageInfo = @[@{@"businessID" : @"custom_message_link",  // 自定义消息唯一标识（注意不要重复）
                            @"cell_name" :  @"TUILinkCell"           // cell 的类名
                            @"cell_data_name" : @"TUILinkCellData"   // cellData 的类名
                          },
                          // 如果您需要多种类型的自定义消息，可以在下面继续添加自定义消息信息
                          @{@"businessID" : @"custom_message_link2",
                            @"cell_name" : @"TUILinkCell2"          
                            @"cell_data_name" : @"TUILinkCellData2"
                          }];
}
@end
```

## 如何发送自定义消息
 <img src="https://qcloudimg.tencent-cloud.cn/raw/e7c26ad63941fb2bc3fb8277bf037ac4.png" width = "500"/>
	
如上图所示，自定义消息发送按钮主要由文本 `title` 和图片 `image` 组成，您可以在 [TUIChatDataProvider.m](https://github.com/tencentyun/TIMSDK/blob/master/iOS/TUIKit/TUIChat/DataProvider/TUIChatDataProvider.m) 的 `load` 函数注册发送按钮信息。
```java
@implementation TUIChatDataProvider
+ (void)load {
    // 以下代码需要您自己实现
    customButtonInfo = @[@{@"SendBtn_Key" : @"custom_link_btn",  // 按钮唯一标识
                           @"SendBtn_Title" :  @"自定义"          // 按钮文本信息
                           @"SendBtn_ImageName" : @"custom_link_image"   // 按钮图片名称
                          }];
}
@end
```

当按钮被点击后，可以在 [TUIC2CChatViewController.m](https://github.com/tencentyun/TIMSDK/blob/master/iOS/TUIKit/TUIChat/UI/Chat/TUIC2CChatViewController.m) 的 `didSelectMoreCell` 回调通过 [createCustomMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a7a38c42f63a4e0c9e89f6c56dd0da316) 接口创建一条自定义消息，其中参数 `data` 可以由 `json` 数据组成， 可以在 `json` 数据里面自定义一个 `businessID` 字段来唯一标识这条消息。

```java
@implementation TUIMessageController
- (void)inputController:(TUIInputController *)inputController didSelectMoreCell:(TUIInputMoreCell *)cell
{
    if ([cell.data.key isEqualToString:@"custom_link_btn"]) { 
        // 创建自定义消息，设置消息的 businessID、展示文本、跳转链接（以下代码需要您自己实现）
        NSString *businessID = @"custom_message_link";
        NSString *text = @"欢迎加入腾讯·云通信大家庭！";
        NSString *link = @"https://cloud.tencent.com/document/product/269/3794";
        NSDictionary *param = @{@"businessID": businessID, @"text":text, @"link":link};
        NSData *data = [NSJSONSerialization dataWithJSONObject:param options:0 error:&error];
        V2TIMMessage *message = [[V2TIMManager sharedInstance] createCustomMessage:data];
        [self sendMessage:message];
    }
}
@end
```
