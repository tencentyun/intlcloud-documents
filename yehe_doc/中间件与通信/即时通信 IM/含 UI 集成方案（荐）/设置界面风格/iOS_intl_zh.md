本文介绍如何设置 iOS 界面风格。

## 设置头像的样式

### 设置缺省的头像图片
TUIKit 的界面在显示用户时，会从用户资料中读取头像地址并显示。如果用户没有设置头像，则显示默认头像。
您可以在 TUIKit 初始化前，自定义默认头像的图片，示例代码如下：
```objectivec
TUIConfig *config = [TUIConfig defaultConfig]; 
// 修改默认头像
config.defaultAvatarImage = [UIImage imageNamed:@"your image"];
// 修改默认群组头像
config.defaultGroupAvatarImage = [UIImage imageNamed:@"your group image"];
// 禁用群组九宫格头像
config.enableGroupGridAvatar = NO;
```

>? 群组头像默认展示九宫格头像。九宫格头像是 TUIKit 使用群成员的头像合成的，如果九宫格合成失败或群组里只有一个成员，TUIKit 会展示 `defaultGroupAvatarImage`。
>如果您不想使用九宫格头像，可以禁用九宫格头像。

### 设置头像的形状
TUIKit 提供 3 种头像类型：矩形直角头像、圆形头像和矩形圆角头像。
```objectivec
typedef NS_ENUM(NSInteger, TUIKitAvatarType) {
    TAvatarTypeNone,             /*矩形直角头像*/
    TAvatarTypeRounded,          /*圆形头像*/
    TAvatarTypeRadiusCorner,     /*圆角头像*/
};
```

您可以在 TUIKit 初始化前，选择头像类型，示例代码如下：
```objectivec
TUIConfig *config = [TUIConfig defaultConfig]; 
// 修改头像类型为圆角矩形，圆角大小为 5
config.avatarType = TAvatarTypeRadiusCorner;
config.avatarCornerRadius = 5.f;
```



## 设置聊天窗口的样式

### 设置聊天窗口的背景色
您可以在初始化聊天窗口前，自定义窗口背景色，示例代码如下：
```objectivec
[TUIChatConfig defaultConfig].backgroudColor = [UIColor greenColor];
```


### 设置聊天窗口的背景图片
您可以在初始化聊天窗口前，自定义窗口背景图片，示例代码如下：
```objectivec
[TUIChatConfig defaultConfig].backgroudImage = [UIImage imageNamed:@"your chat background image"];
```



## 设置消息气泡的样式
聊天界面消息 View 的组合方式如下图所示：
<img src="https://qcloudimg.tencent-cloud.cn/raw/7dedc729dc19b35c56f155e3961b8681.png" style="zoom:40%;"/>

### 设置消息的字体和颜色
文字消息的数据来自于 TUITextMessageCellData 类，通过它的接口可以修改文字消息的字体和颜色。
您可以在初始化聊天窗口前，自定义消息的字体和颜色，示例代码如下：
```objectivec
// 设置发送文字消息的字体和颜色
[TUITextMessageCellData setOutgoingTextFont:[UIFont systemFontOfSize:20]];
[TUITextMessageCellData setOutgoingTextColor:[UIColor blueColor]];
// 设置接收文字消息的字体和颜色
[TUITextMessageCellData setIncommingTextFont:[UIFont systemFontOfSize:20]];
[TUITextMessageCellData setIncommingTextColor:[UIColor purpleColor]];
```



### 设置气泡的背景图片
气泡 Cell 显示的图片从 TUIBubbleMessageCellData 获取，该对象提供了类方法可以设置图片。
您可以在初始化聊天窗口前，自定义气泡背景图片，示例代码如下：
```objectivec
// 设置发送气泡，包括普通状态和选中状态
[TUIBubbleMessageCellData setOutgoingBubble:[UIImage imageNamed:@"outgoing_bubble"]];
[TUIBubbleMessageCellData setOutgoingHighlightedBubble:[UIImage imageNamed:@"outgoing_bubble_highlighted"]];
// 设置接收气泡，包括普通状态和选中状态
[TUIBubbleMessageCellData setIncommingBubble:[UIImage imageNamed:@"incoming_bubble"]];
[TUIBubbleMessageCellData setIncommingHighlightedBubble:[UIImage imageNamed:@"incoming_bubble_highlighted"]];
```


###  设置气泡的边距
在 TUIKit 中，文字和声音都会用气泡显示，TUIMessageCellLayout 提供了类方法设置 bubbleInsets。
您可以在初始化聊天窗口前，自定义气泡边距，示例代码如下：
```objectivec
// 设置发送消息的气泡边距
[TUIMessageCellLayout outgoingTextMessageLayout].bubbleInsets = UIEdgeInsetsMake(20, 20, 24, 24);
// 设置接收消息的气泡边距
[TUIMessageCellLayout incommingTextMessageLayout].bubbleInsets = UIEdgeInsetsMake(20, 20, 24, 24);
```



### 设置发送者的头像样式
修改 TUIMessageCellLayout 的相关属性，可设置发送者的头像样式。
您可以在初始化聊天窗口前，自定义发送者的头像样式，示例代码如下：
```objectivec
// 设置发送者头像大小和位置
[TUIMessageCellLayout outgoingTextMessageLayout].avatarSize = CGSizeMake(80, 80);
[TUIMessageCellLayout outgoingTextMessageLayout].avatarInsets = UIEdgeInsetsMake(10, 10, 20, 20);
// 设置接收者头像大小和位置
[TUIMessageCellLayout incommingTextMessageLayout].avatarSize = CGSizeMake(80, 80);
[TUIMessageCellLayout incommingTextMessageLayout].avatarInsets = UIEdgeInsetsMake(10, 10, 20, 20);
```

> ! 其他消息类型请获取对应的 layout 实例设置头像的大小和位置。



### 设置消息的昵称样式
修改 TUIMessageCellLayout 的相关属性，可设置消息的发送方昵称字体和颜色。
您可以在初始化聊天窗口前，自定义消息的昵称样式，示例代码如下：
```objectivec
// 设置收到的消息的昵称字体及颜色
[TUIMessageCellData setIncommingNameFont:[UIFont systemFontOfSize:20]];
[TUIMessageCellData setIncommingNameColor:[UIColor blueColor]];
// 设置自己的昵称字体及颜色，默认情况下不显示自己的昵称
[TUIMessageCellData setOutgoingNameFont:[UIFont systemFontOfSize:20]];
[TUIMessageCellData setOutgoingNameColor:[UIColor purpleColor]];
```
