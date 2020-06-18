
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

When initializing the chat interface, the upper layer needs to pass the conversation information for the current chat interface, that is, TIMConversation.
The TIMConversation object is obtained using the underlying ImSDK method.

The following code creates a C2C conversation with user `abc`:

```objectivec
TIMConversation *conv = [[TIMManager sharedInstance] getConversation:TIM_C2C receiver:@"abc"];
TUIChatController *vc = [[TUIChatController alloc] initWithConversation:conv];
[self.navigationController pushViewController:vc animated:YES];
```
TUIChatController will automatically pull the user's message history and display it.



## Adding the Contacts Interface

The contacts interface does not require other dependencies. You only need to create the object and display it.

```objectivec
TUIContactController *vc = [[TUIContactController alloc] init];
[self.navigationController pushViewController:vc animated:YES];
```

