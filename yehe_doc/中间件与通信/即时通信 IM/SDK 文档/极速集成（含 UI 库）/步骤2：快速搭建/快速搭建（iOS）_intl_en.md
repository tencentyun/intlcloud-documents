
Instant messaging software usually consists of several basic UIs such as the chat window and conversation list. TUIKit provides a set of basic UI implementations to simplify IM SDK integration. It only takes a few lines of code to use the IM SDK to provide communication in your project.
## Creating the Conversation List Interface

To create a conversation list, you only need to create a TUIConversationListController object. The conversation list reads recent contacts from the database. When a user clicks a contact, TUIConversationListController calls back the event to the upper layer.


```objectivec
// Configure conversation listening
[[TUIKitListenerManager sharedInstance] addConversationListControllerListener:self];
// Create a conversation list
TUIConversationListController *vc = [[TUIConversationListController alloc] init];
[self.navigationController pushViewController:vc animated:YES];


- (void)conversationListController:(TUIConversationListController *)conversationController didSelectConversation:(TUIConversationCell *)conversation
{
    // Conversation list click event, typically, openning the chat interface
}
```


## Opening the Chat Interface

During chat interface initialization, the upper layer needs to pass in the conversation information of the current chat interface. The sample code is as follows:

```objectivec
TUIConversationCellData *data = [[TUIConversationCellData alloc] init];
data.groupID = @"groupID";  // For a group conversation, pass in the corresponding group ID
data.userID = @"userID";    // For a one-to-one conversation, pass in the peer user ID
TUIChatController *vc = [[TUIChatController alloc] initWithConversation:data];
[self.navigationController pushViewController:vc animated:YES];
```
TUIChatController will automatically pull and display the historical messages of the user.



## Adding the Contacts Interface

The contacts interface does not require other dependencies. You only need to create the object and display it.

```objectivec
TUIContactController *vc = [[TUIContactController alloc] init];
[self.navigationController pushViewController:vc animated:YES];
```

