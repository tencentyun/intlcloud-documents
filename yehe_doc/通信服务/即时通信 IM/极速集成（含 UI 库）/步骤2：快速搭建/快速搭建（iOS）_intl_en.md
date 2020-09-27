
Instant messaging software usually consists of several basic interfaces such as the chat window and conversation list. TUIKit provides a set of basic UI implementations to simplify IM SDK integration. It only takes a few lines of code to use the IM SDK to provide communication in your project.

## Creating the Conversation List Interface

To create a conversation list, you only need to create a TUIConversationListController object. The conversation list reads recent contacts from the database. When a user clicks a contact, TUIConversationListController calls back the event to the upper layer.


```objectivec
// Create a conversation list.
TUIConversationListController *vc = [[TUIConversationListController alloc] init];
vc.delegate = self;
[self.navigationController pushViewController:vc animated:YES];


- (void)conversationListController:(TUIConversationListController *)conversationController didSelectConversation:(TUIConversationCell *)conversation
{
	// Conversation list click event. Typically, the chat interface is opened.
}
```


## Opening the Chat Interface

When the chat interface is initializing, the UI layer needs to pass in the conversation information for the current chat interface. The sample code is as follows:
```objectivec
TUIConversationCellData *data = [[TUIConversationCellData alloc] init];
data.groupID = @"groupID";  // Pass in the group ID for group chats
data.userID = @"userID";    // Pass in the user ID for one-to-one chats
TUIChatController *vc = [[TUIChatController alloc] initWithConversation:data];
[self.navigationController pushViewController:vc animated:YES];
```
TUIChatController will automatically pull and display the user's message history.



## Adding the Contacts Interface

The contacts interface does not require other dependencies. You only need to create the object and display it.

```objectivec
TUIContactController *vc = [[TUIContactController alloc] init];
[self.navigationController pushViewController:vc animated:YES];
```

