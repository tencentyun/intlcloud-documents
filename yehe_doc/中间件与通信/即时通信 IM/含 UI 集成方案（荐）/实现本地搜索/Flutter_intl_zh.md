TUIKit 中实现了本地搜索，可支持搜索本地存储的聊天记录、联系人、群聊等。搜索可以帮助用户从纷繁的信息中快速找到目标，也可作为运营工具，增加相关内容的引导，简洁高效。

>! “本地搜索”为 IM 旗舰版功能，[购买旗舰版](https://www.tencentcloud.com/document/product/1047/34577) 后可使用，详见 [价格说明](https://www.tencentcloud.com/document/product/1047/34350?from=17175#.E5.9F.BA.E7.A1.80.E6.9C.8D.E5.8A.A1.E8.AF.A6.E6.83.85)。

## 功能展示

| 组件名                  | 组件功能              |
| ----------------------- | --------------------- |
| TIMUIKitSearch          | 全局搜索              |
| TIMUIKitSearchMsgDetail | 会话内搜索，单聊&群聊 |

全局搜索的界面分为三部分，第一部分是搜索好友，第二部分是搜索群组、群成员，第三部分是搜索消息且按照会话分组。

您可 [下载 Demo 应用](https://intl.cloud.tencent.com/document/product/1047/34279) 即刻体验。

## 接入指引

以下步骤将向您演示如何接入 TUIKit 本地搜索组件。

### 购买套餐包

请单击前往 [购买旗舰版](https://www.tencentcloud.com/document/product/1047/34577)。

### 引入本地搜索

在 全局搜索 页面的文件中引入以下内容：

```dart
/// 集成 TIMUIKitSearch 组件
import 'package:tencent_cloud_chat_uikit/ui/views/TIMUIKitSearch/tim_uikit_search.dart';
```

在 会话内搜索 页面的文件中引入以下内容：

```dart
/// 集成 TIMUIKitSearchMsgDetail 组件
import 'package:tencent_cloud_chat_uikit/ui/views/TIMUIKitSearch/tim_uikit_search_msg_detail.dart';
```

### 全局搜索 界面

TIMUIKitSearch 为全局搜索组件，搜索的结果为匹配搜索关键字的**联系人**、**群组**、**聊天记录**。
TIMUIKitSearch 的一般使用场景为在消息列表上方放置，点击进入全局搜索组件。

代码示例可见 [此文档](https://comm.qq.com/im/doc/flutter/zh/TUIKit/TIMUIKitSearch/TIMUIKitSearch-Implementation.html)。

### 会话内搜索 界面

TIMUIKitSearchMsgDetail 为搜索聊天信息的组件，搜索的结果为匹配搜索关键字的**聊天记录**。
TIMUIKitSearchMsgDetail 的使用场景多样，例如：

- 在全局搜索点击**聊天记录**时进入；
- 在用户资料页面查询**聊天记录**时进入；
- 在群组资料页面查询**聊天记录**时进入。

代码示例可见 [此文档](https://comm.qq.com/im/doc/flutter/zh/TUIKit/TIMUIKitSearch/TIMUIKitSearch-Implementation.html)。

## 常见问题

### 1、如何搜索富媒体消息

富媒体消息包含文件、图片、语音、视频消息。
对于文件消息，界面通常显示文件名，因此创建时可以设置 `fileName` 参数，作为被搜索的内容，如果 `fileName` 不设置则会从 `filePath` 提取文件名，并且都会保存到本地和服务器。
而对于图片、语音、视频消息，界面通常显示缩略图或时长，可以指定消息类型做分类搜索，但不能通过关键字搜索。

[](id:feedback)
