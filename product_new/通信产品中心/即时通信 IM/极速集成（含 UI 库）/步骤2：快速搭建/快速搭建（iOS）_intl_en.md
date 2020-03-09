
Instant messaging software usually consists of basic interfaces such as the chat window and conversation list. TUIKit provides a set of basic UI implementations to simplify IM SDK integration. It takes only a few lines of code to use the IM SDK to provide communication features in your project.

## Creating the Conversation List UI

To create a conversation list, you only need to create a TUIConversationListController object. The conversation list reads recent contacts from the database. When a user clicks a contact, TUIConversationListController calls this event back to the upper layer.

Set the layout in any layout.xml:
```objectivec
// Create a conversation list
TUIConversationListController *vc = [[TUIConversationListController alloc] init];
vc.delegate = self;
[self.navigationController pushViewController:vc animated:YES];


- (void)conversationListController:(TUIConversationListController *)conversationController didSelectConversation:(TUIConversationCell *)conversation
{
	// Conversation list click event, which usually opens the chat UI
}
```


## Opening the Chat UI

When initializing the chat UI, the upper layer needs to pass in the conversation information for the current chat UI, that is, TIMConversation.
The TIMConversation object is obtained through the underlying ImSDK method.

Take creating a C2C conversation with user `abc` as an example. The sample code is as follows:

```objectivec
TIMConversation *conv = [[TIMManager sharedInstance] getConversation:TIM_C2C receiver:@"abc"];
TUIChatController *vc = [[TUIChatController alloc] initWithConversation:conv];
[self.navigationController pushViewController:vc animated:YES];
```
TUIChatController will automatically pull and display the user’s historical messages.



## Adding the Contact UI

The contact UI does not require other dependencies. Instead, you only need to create an object and display it.

```objectivec
TUIContactController *vc = [[TUIContactController alloc] init];
[self.navigationController pushViewController:vc animated:YES];
```

