
## TUIConversationListController

TUIConversationListController can display recent conversations, internally monitor conversation change notifications, and sort them by time.

| API | Description |
| --- | --- |
| [delegate](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/TUIKit/Classes/TUIConversationListController.html) | Delegates callback to externally process selected events. |
| [viewMode](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/TUIKit/Classes/TUIConversationListController.html) | Indicates the data source of the controller. |

## Chat Interface

The chat interface consists of the chat controller and input controller.

### TUIChatController

TUIChatController combines the two major components of the chat interface and exports APIs externally to facilitate message customization.

| API | Description |
| --- | --- |
| [messageController](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/TUIKit/Classes/TUIChatController.html) | Implements the main chat TableView. |
| [inputController](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/TUIKit/Classes/TUIChatController.html) | Indicates the input controller. |
| [delegate](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/TUIKit/Classes/TUIChatController.html) | Delegates callback for UI events and custom cells. |
| [moreMenus](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/TUIKit/Classes/TUIChatController.html) | Provides more menu item data. |
| [sendMessage:](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/TUIKit/Classes/TUIChatController.html) | Sends custom messages. |
| [saveDraft](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/TUIKit/Classes/TUIChatController.html) | Saves drafts. |

### TUIMessageCell

TUIMessageCell is the basic class for each message. All UI elements of messages can be accessed through TUIMessageCell.

| API | Description |
| --- | --- |
| [avatarView](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/TUIKit/Classes/TUIMessageCell.html) | Indicates the profile photo. |
| [nameLabel](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/TUIKit/Classes/TUIMessageCell.html) | Indicates the nickname label. |
| [container](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/TUIKit/Classes/TUIMessageCell.html) | Indicates the main message content container. |
| [indicator](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/TUIKit/Classes/TUIMessageCell.html) | Indicates the indicator for loading activities. |
| [retryView](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/TUIKit/Classes/TUIMessageCell.html) | Indicates the retry view. |
| [messageData](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/TUIKit/Classes/TUIMessageCell.html) | Indicates the message data source. |
| [delegate](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/TUIKit/Classes/TUIMessageCell.html) | Delegates message UI events. |
| [fillWithData:](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/TUIKit/Classes/TUIMessageCell.html) | Updates data sources. |

### TUIMessageCellData

When iOS TableView is scrolled, TableViewCell will be reused, and all message data is stored in TUIMessageCellData instead of Cell. During display, fillWithData will be internally invoked to refresh the interface.

| API | Description |
| --- | --- |
| [identifier](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/TUIKit/Classes/TUIMessageCellData.html) | Indicates the message sender ID. |
| [avatarUrl](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/TUIKit/Classes/TUIMessageCellData.html) | Indicates the URL of the profile photo. |
| [avatarImage](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/TUIKit/Classes/TUIMessageCellData.html) | Indicates the profile photo image. |
| [name](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/TUIKit/Classes/TUIMessageCellData.html) | Indicates the nickname. |
| [showName](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/TUIKit/Classes/TUIMessageCellData.html) | Indicates whether to display the nickname. |
| [direction](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/TUIKit/Classes/TUIMessageCellData.html) | Indicates the messaging direction, which is receiving or sending. |
| [status](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/TUIKit/Classes/TUIMessageCellData.html) | Indicates the message status. |
| [innerMessage](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/TUIKit/Classes/TUIMessageCellData.html) | Indicates the message object used by the IM SDK. |
| [nameFont](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/TUIKit/Classes/TUIMessageCellData.html) | Indicates the font of the nickname. |
| [nameColor](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/TUIKit/Classes/TUIMessageCellData.html) | Indicates the color of the nickname. |
| [cellLayout](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/TUIKit/Classes/TUIMessageCellData.html) | Indicates the message layout, which controls the profile photo, nickname, bubble, and other positions. |
| [contentSize](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/TUIKit/Classes/TUIMessageCellData.html) | Indicates the message content size. |


