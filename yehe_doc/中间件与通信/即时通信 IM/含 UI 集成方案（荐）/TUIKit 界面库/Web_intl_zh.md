

## chat-uikit-react 介绍
chat-uikit-react 是基于腾讯云 IM SDK 的一款 UI 组件库，它提供了一些通用的 UI 组件，包含会话、聊天、关系链、群组、音视频通话等功能。
基于 UI 组件您可以像搭积木一样快速搭建起自己的业务逻辑。
chat-uikit-react 中的组件在实现 UI 功能的同时，会调用 IM SDK 相应的接口实现 IM 相关逻辑和数据的处理，因而开发者在使用 TUIKit 时只需关注自身业务或个性化扩展即可。

## chat-uikit-react 组成
chat-uikit-react 主要分为 TUIKit、TUIConversation、TUIChat、TUIManage 几个主要模块组成，每个模块负责不同的内容。

## TUIKit 功能介绍
TUIKit 为最外层的一个 Provider， 通过 Context 提供 tim、conversation、profile 等多种内容，具体可参考[开源代码](!https://github.com/TencentCloud/chat-uikit-react)。

## TUIConversation 功能介绍
TUIConversation 主要负责会话列表的展示和编辑，包含会话置顶、会话删除等功能。

## TUIChat 功能介绍
TUIChat 主要负责会话消息展示和编辑，包含消息发送、消息撤回、消息转发等功能。

## TUIManage 功能介绍
TUIManage 主要负责会话相关信息展和会话置顶、会话删除等操作。
