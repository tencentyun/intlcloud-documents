## Nickname and Profile Photo Update in Conversations
**Conversations do not store nicknames and profile photos**. Therefore, the SDK needs to obtain them from user profiles or group profiles saved in the local storage and use them in conversations. For a one-to-one conversation, the SDK obtains and uses the other user's nickname and profile photo. For a group conversation, the SDK obtains and uses the group name and group profile photo. To keep local user profiles and group profiles up-to-date, the latest SDK version has the following optimizations:

**Ono-to-one conversations:**
- 1. When a user actively obtains a conversation or the SDK calls back a conversation update, if the SDK detects that the local storage does not have the other user's profile, it will synchronize the user's profile from the server and save it locally.
- 2. If a friend's profile is changed, the SDK will receive a notification of the change from the backend and update the friend's profile locally. If a stranger's profile is changed, the backend will not send notifications, so the stranger's profile will not be updated locally. However, you can call the `getFriendsInfo` API to get strangers' profiles and update them locally.
- 3. When sending a message, the backend will attach the user's latest nickname and profile photo to the message body. After receiving the message, the SDK will update the nickname and profile photo locally if the user's profile already exists in the local storage.

In summary, the SDK will ensure that the nicknames and profile photos in conversations with friends are up-to-date. While with strangers, the SDK cannot guarantee that and you need to actively pull the nicknames and profile photos if needed.

**Group conversations:**
- 1. After you join a group successfully, the SDK will actively obtain the group profile and save it locally.
- 2. When the profile of a group that you have joined is modified, the backend will notify the client, which will then update the group profile locally in time.

In summary, the SDK will ensure that the nicknames and profile photos in conversations are up-to-date for groups you have joined, but not for groups that you haven't joined or have left.

>! 
>- The change of user profiles or group profiles do not trigger conversation update. Therefore, the nicknames and profile photos in a conversation will not be updated until the next conversation operation is performed (such as actively obtaining the conversation, marking the conversation as read, and sending/receiving messages).
>- There is no relationship chain between you and a stranger. If the stranger's profile is changed, the backend will not send notifications, and the stranger's local profile will not be updated. It will be updated only when you actively pull the stranger's profile.

## Nickname and Profile Photo Update in the Message List
**Messages store nicknames and profile photos**. In order to keep the nicknames and profile photos of messages up-to-date, the latest SDK version has the following optimizations:
- 1. When sending a message, the backend will attach the user's latest nickname and profile photo to the message body. After receiving the message, the SDK will update the nickname and profile photo locally if the user's profile already exists in the local storage.
- [](id:Update) 2. After a message is successfully sent and received, the nickname and profile photo stored in the message cannot be modified. In order to get the new nicknames and profile photos for historical messages, the SDK will first query local user profiles when trying to obtain the nickname and profile photo fields via messages. If local user profiles exist, local nicknames and profile photos will be returned. (According to optimization 1, local nicknames and profile photos will be updated in real time according to new messages.) If not, the nicknames and profile photos in message bodies will be returned.

In summary, the SDK will ensure that the nicknames and profile photos of new messages are up-to-date, but not those of historical messages. The nicknames and profile photos of historical messages will be updated only when the senders' profiles exist in the local storage.

## FAQs
According to the above description, the latest SDK version has a lot of optimizations regarding nickname and profile photo. If you encounter any nickname and profile photo issues, please first upgrade your SDK to the [latest version](https://intl.cloud.tencent.com/document/product/1047/33996) and check whether the issues are solved. If not, please see the following FAQs:

### Why isn't the conversation updated immediately when the nickname and profile photo are changed?
The change of nicknames and profile photos do not trigger conversation update. Therefore, the nickname and profile photo in a conversation will not be updated until the next conversation operation is performed (such as actively obtaining the conversation, marking the conversation as read, and sending/receiving messages). However, you can listen for friend or group profile update notifications to update the nicknames and profile photos in conversations.

### Why isn't the conversation updated when the stranger's nickname and profile photo are changed?
There is no relationship chain between you and a stranger. If the stranger's profile is changed, the backend will not send notifications, and the stranger's local profile will not be updated. It will be updated only when you actively pull the stranger's profile or receive a message from the stranger. The message will carry the stranger's latest nickname and profile photo, and the SDK will update them locally after receiving the message.

### Why can't the nicknames and profile photos of historical messages be updated?
Please refer to [optimization 2](#Update) in **Nickname and Profile Photo Update in the Message List**. If the local storage does not have the senders' profiles, the nicknames and profile photos of historical messages won't be updated. They will be updated only when you actively pulls the senders' profiles.

### Why doesn't the SDK actively pull user profiles when conversations are updated or messages are received?
Conversation update and message sending/receiving are both frequent events. Synchronizing user profiles every time will cause huge pressure on the client and backend, seriously affecting application performance. We don't recommend that you actively pull user profiles in both cases, because it also affects application performance. The recommended approach is to pull user profiles when users click on the profile photos of messages.
