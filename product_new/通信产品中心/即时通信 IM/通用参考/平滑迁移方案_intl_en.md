Tencent Cloud Instant Messaging (IM) has rich experience in high-concurrency and reliable operation. For app developers who are using their own or third-party instant messaging services and want to connect to IM, they need to consider the migration problem. IM provides migration solutions tailored to different scenarios.

## Terminology

This document uses the following terms:

- **Old system:** indicates the instant messaging service previously used by the app.
- **New system:** indicates Tencent Cloud Instant Messaging (IM).
- **App 1.0:** indicates the app that implements instant messaging features based on the old system.
- **App 2.0:** indicates the app that implements instant messaging features based on the new system.
- **Message routing (message callback) service:** after receiving messages, a third-party communication service provider forwards a copy of the messages to the app backend, similar to the [callback after sending one-to-one chat messages](https://intl.cloud.tencent.com/document/product/1047/34365) in IM.

The migration process essentially switches the instant messaging service from the old system to the new system and upgrades app 1.0 to app 2.0.

## Migration Methods

IM provides the following two migration options, which have different migration effects and implementation difficulty levels. Therefore, consider the existing instant messaging implementation scenarios of the app to determine an appropriate migration solution.

### Forcible upgrade method

The forcible upgrade policy forces the app to upgrade from version 1.0 to 2.0 after IM data synchronization is completed. This method is simple to implement and does not need to handle compatibility issues between the new app and the old app. The following figure illustrates this migration method:

![](https://main.qcloudimg.com/raw/e37a5686c81c73827c20312169c3ecc0.png)

The detailed process is as follows:

1. Import historical data to IM, including:
   - Accounts
   - User profiles
   - User relationship chains
   - One-to-one chat history
   - Group data
   - Group chat history
2. Force to upgrade from app 1.0 to app 2.0.
3. Deprecate the old system and migrate all user communications to the new system.

### Compatible migration method

The new app and the old app can coexist and exchange messages between them. Before app 1.0 is deactivated, the app backend needs to maintain real-time two-way synchronization between the old and new systems. This solution is more complicated but provides a better end-user experience. The following figure illustrates this migration method:

![](https://main.qcloudimg.com/raw/3b19fed85458fa96ae7110fea8cb8e41.png)

The detailed process is as follows:

1. Import historical data to IM, including:
   - Accounts
   - User profiles
   - User relationship chains
   - One-to-one chat history
   - Group data
   - Group chat history
2. Implement two-way data synchronization between the new and old systems, including:
   - Synchronize one-to-one chat messages in real time
   - Synchronize group data and group chat messages in real time
3. The new and old systems can coexist and exchange messages until the old app is deprecated.

## Migration Procedure

### Importing accounts

Accounts must be imported before other data can be imported.
The app backend needs to call the [RESTful API for batch importing accounts](https://intl.cloud.tencent.com/document/product/1047/34954) to import all accounts to IM. If you also need to import user nicknames and profile photos when importing accounts, call the [RESTful API for importing a single account](https://intl.cloud.tencent.com/document/product/1047/34953).

### Importing user profiles

Call the [RESTful API for setting profiles](https://intl.cloud.tencent.com/document/product/1047/34916) to import existing user profiles to IM.

### Importing user relationship chains

Call the [RESTful API for adding friends](https://intl.cloud.tencent.com/document/product/1047/34902) to import existing relationship chains to IM.

### Importing the one-to-one chat history

Call the [RESTful API for importing one-to-one chat messages](https://intl.cloud.tencent.com/document/product/1047/35014) to import existing one-to-one chat messages to IM.

### Importing group data and the group chat history

Follow these steps to import group data and the group chat history:

1. Call the [RESTful API for importing basic group information](https://intl.cloud.tencent.com/document/product/1047/34967) to create groups. You can specify initial group members when calling this API.
2. If group members are not imported when importing groups, call the [RESTful API for importing group members](https://intl.cloud.tencent.com/document/product/1047/34969).
3. Call the [RESTful API for importing group messages](https://intl.cloud.tencent.com/document/product/1047/34968) to import the group chat history.
4. To correct the unread count of group members, call the [RESTful API for setting the unread count for members](https://intl.cloud.tencent.com/document/product/1047/34909).

One-to-one chat messages, group data, and group messages need to be managed on the new system. When the the incremental data of these information is generated, use IM callbacks to sync the incremental data to the old system. Similarly, new data that is generated in the old system also needs to be synchronized to the new system.

### Synchronizing one-to-one chat messages

Synchronize incremental messages in the old system to IM by calling the [RESTful API for sending a one-to-one chat message](https://intl.cloud.tencent.com/document/product/1047/34919), and synchronize incremental messages in IM to the old system by calling the [callback after sending one-to-one chat messages](https://intl.cloud.tencent.com/document/product/1047/34365).

### Synchronizing group data and group messages

**Synchronizing group profiles**

1. Synchronize the changes to group basic information in the old system in real time by calling the [RESTful API for modifying basic group information](https://intl.cloud.tencent.com/document/product/1047/34962).
2. Synchronize the changes to group basic information in IM to the old system by calling the [callback after creating a group](https://intl.cloud.tencent.com/document/product/1047/34369), [callback after dismissing a group](https://intl.cloud.tencent.com/document/product/1047/34377), and [callback after modifying the group profile](https://intl.cloud.tencent.com/document/product/1047/34378).

**Synchronizing group member information**

1. Synchronize the friends added to and deleted from the old system to IM by calling the [RESTful API for adding group members](https://intl.cloud.tencent.com/document/product/1047/34921) and [RESTful API for deleting group members](https://intl.cloud.tencent.com/document/product/1047/34949).
2. Synchronize group joining and quitting information in IM to the old system through the [callback after a new member joins the group](https://intl.cloud.tencent.com/document/product/1047/34372) and the [callback after a member quits the group](https://intl.cloud.tencent.com/document/product/1047/34373).

**Synchronizing group messages**

1. Synchronize incremental group messages in the old system to IM by calling the [RESTful API for sending common messages in a group](https://intl.cloud.tencent.com/document/product/1047/34959).
2. Synchronize incremental group messages in IM to the old system by calling the [callback after sending messages in a group](https://intl.cloud.tencent.com/document/product/1047/34375).

>If some of the current instant messaging services of your app are not covered by the preceding solutions, you can contact our customer service or consult your sales representative for an appropriate migration solution.
