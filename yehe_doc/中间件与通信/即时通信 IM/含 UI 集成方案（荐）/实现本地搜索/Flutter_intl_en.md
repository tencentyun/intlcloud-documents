Local search is implemented in TUIKit. It allows users to quickly find the expected information from massive amounts of complex data, such as the chat history, contacts, and group chats. It can also be used as an operations tool to easily and efficiently navigate to extensive content.

>! The local search feature is only available on the IM Ultimate edition. To use it, [purchase the Ultimate edition](https://intl.cloud.tencent.com/document/product/1047/34577). For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).


## Feature Demonstration
| Component               | Description           |
| -------------------- | ------------------ |
| TIMUIKitSearch       | Global search           |
| TIMUIKitSearchMsgDetail  | In-conversation search, including searches in one-to-one chats and group chats.           |

The global search UI consists of three parts: the first part is for friend search, the second part is for group and group member search, and the third part is for message search, where messages are classified by conversation.

[Download and try out the application demo](https://intl.cloud.tencent.com/document/product/1047/34279).
![](https://qcloudimg.tencent-cloud.cn/raw/11fadc4fdf8ff39b60f07009c23132d0.gif)

## Integration Guide
The following introduces how to integrate the local components of TUIKit.

### Purchasing the package
[Purchase the Ultimate edition](https://intl.cloud.tencent.com/document/product/1047/34577).

### Integrating local search

Import the following content to the global search page file:
```dart
/// Integrate the TIMUIKitSearch component
import 'package:tim_ui_kit/ui/views/TIMUIKitSearch/tim_uikit_search.dart';             
```

Import the following content to the in-conversation search page file:
```dart
/// Integrate the TIMUIKitSearchMsgDetail component
import 'package:tim_ui_kit/ui/views/TIMUIKitSearch/tim_uikit_search_msg_detail.dart';           
```

### Global search page
TIMUIKitSearch is a global search component. In this component, search results are **contacts**, **groups**, and **chat records** that match search keywords.
TIMUIKitSearch is usually placed above the message list. You can click it to open the global search component.
<img src="https://qcloudimg.tencent-cloud.cn/raw/1e9aab6e5e1f33704e67bcc545c88785.png" style="zoom:50%;"/>


See the sample code [here](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitSearch/).

### In-conversation search page
TIMUIKitSearchMsgDetail is a chat information search component. In this component, search results are **chat records** that match search keywords.
TIMUIKitSearchMsgDetail can be accessed via various entries, including:
- **Chat History** on the global search page
- **Search Chat History** on a user profile page
- **Search Chat History** on a group profile page

<img src="https://qcloudimg.tencent-cloud.cn/raw/4923c2696d491ceafb1fd6cd234a0e3a.png" style="zoom:50%;"/>

See the sample code [here](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitSearch/).

## FAQs
### 1. How do I search for rich media messages?
Rich media messages include file, image, audio, and video messages.
For a file message, the filename is usually displayed on the UI. Therefore, you can set the `fileName` parameter as the searched content when creating a file message. If `fileName` is not set, the system gets the filename from `filePath` and saves it to both the local device and the server.
For an image, audio, or video message, the thumbnail or duration is usually displayed on the UI. In this case, you can specify the message type for search but cannot specify keywords for search.

[](id:feedback)


