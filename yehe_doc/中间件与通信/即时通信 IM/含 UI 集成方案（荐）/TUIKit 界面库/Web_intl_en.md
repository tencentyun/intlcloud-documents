
## chat-uikit-react Overview
chat-uikit-react is a UI component library based on Tencent Cloud IM SDK. It provides universal UI components to offer features such as conversation, chat, relationship chain, group, and audio/video call features.
With these UI components, you can quickly build your own business logic.
When implementing UI features, components in chat-uikit-react will also call the corresponding APIs of the IM SDK to implement IM-related logic and data processing, allowing developers to focus on their own business needs or custom extensions.

## chat-uikit-react Components
chat-uikit-react provides the following UI components for different purposes: TUIKit, TUIConversation, TUIChat, and TUIManage.

## TUIKit
TUIKit is the outermost provider. It provides TIM, conversation, profile, and other types of content through contexts. For more information, see the [open source code](!https://github.com/TencentCloud/chat-uikit-react).

## TUIConversation
TUIConversation is responsible for conversation list display and editing. It allows you to pin a conversation to the top, delete conversations, etc.

## TUIChat
TUIChat is responsible for message display and editing. It allows you to send, recall, and forward messages, etc.

## TUIManage
TUIManage is responsible for conversation display and editing. It allows you to pin a conversation to the top, delete conversations, etc.
