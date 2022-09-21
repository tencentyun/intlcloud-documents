## TIMUIKitCore[](id:timuikitcore)
`TIMUIKitCore` provides two static methods: `getInstance` and `getSDKInstance`.
- `getInstance`: returns a `CoreServicesImpl` instance.
- `getSDKInstance`: returns an SDK instance.

`CoreServicesImpl` is the TIMUIKit core class, which provides methods for initialization, login, logout, and getting user information.
```dart
import 'package:tim_ui_kit/tim_ui_kit.dart';

final CoreServicesImpl _coreInstance = TIMUIKitCore.getInstance();
final V2TIMManager _sdkInstance = TIMUIKitCore.getSDKInstance();

/// init
_coreInstance.init(
        sdkAppID: 0, // SDKAppID obtained from the console
        loglevel: LogLevelEnum.V2TIM_LOG_DEBUG,
        listener: V2TimSDKListener());
/// unInit
_coreInstance.unInit();

/// login
_coreInstance.login(
    userID: 0, // User ID
    userSig: "" // See the official documentation for userSig
)

/// logout
_coreInstance.logout();

/// getUsersInfo
_coreInstance.getUsersInfo(userIDList: ["123", "456"]);

/// setOfflinePushConfig
_coreInstance.setOfflinePushConfig(
    businessID: businessID, // IM console certificate ID, which does not need to be entered for TPNS integration
    token: token, // Token obtained when you register your application with the vendor platform or TPNS
    isTPNSToken: false // Whether to integrate TPNS, or whether the token is obtained from TPNS
)

/// setSelfInfo
_coreInstance.setSelfInfo(userFullInfo: userFullInfo) // Set user information

/// setTheme
_coreInstance.setTheme(TUITheme theme: theme) // Set the theme color
/*
  TUITheme(
    // Primary color of the application
    final Color? primaryColor;
    // Secondary color of the application
    final Color? secondaryColor;
    // Tip (information) color, for secondary actions or tips
    final Color? infoColor;
    // Light background color, which is lighter than the primary background color and is used to fill gaps or shadows
    final Color? weakBackgroundColor;
    // Light dividing line color, for dividing lines or borders
    final Color? weakDividerColor;
    // Light font color
    final Color? weakTextColor;
    // Dark font color
    final Color? darkTextColor;
    // Light primary color, for app bars or panels
    final Color? lightPrimaryColor;
    // Font color
    final Color? textColor;
    // Caution color, for high-risk operations
    final Color? cautionColor;
    // Group owner color
    final Color? ownerColor;
    // Group admin color
    final Color? adminColor;)
*/
```

### Static methods
- **TIMUIKitCore.getInstance()**:
Returns a `CoreServicesImpl` instance.
- **TIMUIKitCore.getSDKInstance()**:
Returns a `V2TIMManager` SDK instance. For the usage details, see [Flutter IM SDK documentation](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMManager/initSDK.html).


[](id:timuikitconversation)
## TIMUIKitConversation
`TIMUIKitConversation` is a conversation component for getting user conversation lists. It provides a set of UIs by default and allows users to customize the number of items. It also provides the corresponding `TIMUIKitConversationController`.

```dart
import 'package:tim_ui_kit/tim_ui_kit.dart';

final TIMUIKitConversationController _controller =
      TIMUIKitConversationController();
void _handleOnConvItemTaped(V2TimConversation? selectedConv) {
    /// Processing logic, from which you can redirect to the chat UI
}

List<ConversationItemSlidablePanel> _itemSlidableBuilder(
      V2TimConversation conversationItem) {
    return [
      ConversationItemSlidablePanel(
        onPressed: (context) {
          _clearHistory(conversationItem);
        },
        backgroundColor: hexToColor("006EFF"),
        foregroundColor: Colors.white,
        label: 'Clear chat',
        autoClose: true,
      ),
      ConversationItemSlidablePanel(
        onPressed: (context) {
          _pinConversation(conversationItem);
        },
        backgroundColor: hexToColor("FF9C19"),
        foregroundColor: Colors.white,
        label: conversationItem.isPinned! ? 'Unpin from top' : 'Pin to top',
      )
    ];
  }

TIMUIKitConversation(
    onTapItem: _handleOnConvItemTaped, /// Conversation item tapping callback, which can be used to redirect to the chat UI
    itemSlidableBuilder: _itemSlidableBuilder, /// Action of sliding a conversation item to the left. You can customize the action, for example, configure the action to pin a conversation to the top.
    controller: _controller, /// Conversation component controller. You can use it to get conversation data, configure conversation data, pin a conversation to the top, and so on.
    itembuilder: (conversationItem) {} /// UI for customizing conversation items. It can be used with `TIMUIKitConversationController` to implement business logic.
    conversationCollector: (conversation) {} /// Conversation collector. You can configure whether to display conversations.
)
```

[](id:timuikitconversationcontroller)
### TIMUIKitConversationController

#### Methods

- **loadData(int count)**:
Loads a conversation list. `count` specifies the number of conversations loaded each time.
- **reloadData(int count)**:
Reloads a conversation list. `count` specifies the number of conversations reloaded each time.
- **pinConversation({required String conversationID, required bool isPinned})**:
Pins a conversation to the top.
- **clearHistoryMessage({required V2TimConversation conversation})**:
Clears the messages of a specified conversation.
- **deleteConversation({required String conversationID})**:
Deletes a specified conversation.
- **setConversationListener({V2TimConversationListener? listener})**:
Adds a conversation listener.
- **dispose()**:
Termination


[](id:timuikitchat)
## TIMUIKitChat
`TIMUIKitChat` is a chat component that provides the capability to display message lists and send messages, and supports the customization of display of various custom message types. It can also be used with TIMUIKitChatController to implement the local storage and pre-rendering of messages.
Currently, `TIMUIKitChat` can be used to parse the following types of message:
- Text message
- Image message
- Video message
- Voice message
- Group message
- Combined message
- File message

```dart
import 'package:tim_ui_kit/tim_ui_kit.dart';

TIMUIKitChat(
    conversationID: "", /// Conversation ID
    conversationType: 0, /// Conversation type
    conversationShowName: "", /// Conversation display name
    appBarActions: [], /// App bar action. You can use it to redirect to the group profile page or user profile page.
    onTapAvatar: _onTapAvatar, /// Profile photo tapping callback. You can use it to redirect to the user profile page.
    showNickName: false, /// Whether to display the nickname
    messageItemBuilder: (message) {
        /// Custom message constructor. If `null` is returned, the default constructor is used.
    },
    exteraTipsActionItemBuilder: (message) {
      /// Message tap-and-hold tip customization. Configure it according to your business requirements.
    }
)
```

### TIMUIKitChatController

#### Methods
- **setMessageListener({V2TimAdvancedMsgListener? listener})**: sets an event listener for advanced messages.
- **removeMessageListener({V2TimAdvancedMsgListener? listener})**: removes an event listener for advanced messages.
- **clearHistory()**: clears the message history.
- **dispose()**: termination



[](id:timuikitprofile)
## TIMUIKitProfile

`TIMUIKitProfile` is used to display user profiles. It also allows you to customize and add actions.

```dart
TIMUIKitProfile(
    userID: "",
    controller: TIMUIKitProfileController(),  // Profile Controller
    operationListBuilder: (context, userInfo, conversation) {
        /// Custom action, such as setting the Mute Notifications option and pinning a message to the top. If no value is passed in, the default action is used by default.
    },
    bottomOperationBuilder: (context, friendInfo, conversation) {
        /// Bottom action, such as deleting a friend
    },
    handleProfileDetailCardTap: (BuildContext context, V2TimUserFullInfo? userFullInfo) {
        /// User profile tile tapping callback
    },
    canJumpToPersonalProfile: false, // Whether to redirect to the user profile page
)
```

### TIMUIKitProfileController
- **pinedConversation(bool isPined,String convID)**:
Pins a conversation to the top. `isPined` indicates whether to pin the conversation to the top. `convID` indicates the ID of the conversation to be pinned to the top.
- **addUserToBlackList(bool shouldAdd,String userID)**:
Adds a user to the blocklist. `shouldAdd` indicates whether to add the user to the blocklist. `userID` indicates the ID of the user to be added to the blocklist.
- **changeFriendVerificationMethod(int allowType)**:
Modifies the friend request verification mode. `0` means to accept all friend requests. `1` means requiring approval for friend requests. `2` means to reject all friend requests.
- **updateRemarks(String userID,String remark)**:
Updates the remarks of a friend. `userID` indicates the ID of the user whose remarks are to be updated. `remark` indicates the remarks.
- **loadData**:
Loads data.
- **dispose()**:
Termination
- **addFriend(String userID)**:
Adds a friend. `userID` indicates the ID of the friend to be added.



[](id:timuikitgroupprofile)
## TIMUIKitGroupProfile
`TIMUIKitGroupProfile` is the group management UI. It also allows you to customize and add actions.
```dart
TIMUIKitGroupProfile(
    groupID: "", // Group ID. Required
    operationListBuilder:(){}, // Action custom constructor
    bottomOperationListBuilder: () {}, // Bottom action custom constructor
)
```
`operationListBuilder` and `bottomOperationListBuilder` enable you to configure operation items. They can be used together with components as needed.

### Static methods
- **TIMUIKitGroupProfile.memberTile()**:
Group member tile, used to display group member overview and group member list, and perform operations such as deleting a group member.
- **TIMUIKitGroupProfile.groupNotification()**:
Displays and modifies group notices.
- **TIMUIKitGroupProfile.groupManage()**:
Manages a group, such as setting the admin and muting members.
- **TIMUIKitGroupProfile.groupType()**:
Displays the group type.
- **TIMUIKitGroupProfile.groupAddOpt()**:
Sets or modifies the group joining option.
- **TIMUIKitGroupProfile.nameCard()**:
Sets or modifies the group nickname.


[](id:timuikitblacklist)
## TIMUIKitBlackList
`TIMUIKitBlackList` is the blocklist component.

```dart
TIMUIKitBlackList(
    onTapItem: (_) {}, /// Item tapping callback
    emptyBuilder: () {} /// Displayed when the list is empty
    itemBuilder: () {} /// Custom item
)
```


[](id:timuikitgroup)
## TIMUIKitGroup
`TIMUIKitGroup` is the group list component.

```dart
TIMUIKitGroup(
    onTapItem: (_) {}, /// Item tapping callback
    emptyBuilder: () {} /// Displayed when the list is empty
    itemBuilder: () {} /// Custom item
)
```


[](id:timuikitcontact)
## TIMUIKitContact
`TIMUIKitContact` is the contacts component. It provides the list of contacts.

```dart
import 'package:tim_ui_kit/tim_ui_kit.dart';

TIMUIKitContact(
      topList: [
        TopListItem(name: "New contact", id: "newContact"),
        TopListItem(name: "My groups", id: "groupList"),
        TopListItem(name: "Blocklist", id: "blackList")
      ], /// Top action list
      topListItemBuilder: _topListBuilder, /// Top action list constructor
      onTapItem: (item) { }, /// Contact tapping
      emptyBuilder: (context) => const Center(
        child: Text("No contact"),
      ), /// Displayed when the contact list is empty
    );
```


[](id:timuikitnewcontact)
## TIMUIKitNewContact
`TIMUIKitNewContact` is the new contacts UI.
```dart
TIMUIKitNewContact(
    onAccept: (applicationInfo) {
        /// Friend request acceptance callback
    },
    onRefuse: (applicationInfo) {
        /// Friend request rejection callback
    },
    emptyBuilder: () {
        /// Callback when no friend request is received
    },
    itemBuilder: () {
        /// Custom friend request item constructor
    }
)
```
