## Conversation

In the IM SDK, there are three types of [conversation](https://web.sdk.qcloud.com/im/doc/en/Conversation.html) objects:
- One-to-one (C2C): A one-to-one conversation between only two users.
- GROUP: A group conversation among group members.
- @TIM#SYSTEM (system notification conversation).

You can use the conversation class APIs to display/update the conversation list, update the unread count, pin a conversation to the top, and mute message notifications.

## Conversation Storage Policy

By default, the client can pull 100 recent conversations from the cloud. If you upgrade to the Ultimate edition, up to 500 recent conversations can be pulled from the cloud. The retention period of a conversation is the same as that of the last message, which is seven days by default.