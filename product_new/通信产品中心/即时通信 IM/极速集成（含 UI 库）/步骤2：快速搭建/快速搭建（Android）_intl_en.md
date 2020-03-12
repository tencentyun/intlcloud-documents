
Instant messaging software usually consists of basic interfaces such as the chat window and conversation list. TUIKit provides a set of basic UI implementations to simplify IM SDK integration. It takes only a few lines of code to use the IM SDK to provide communication features in your project.

## Creating the Conversation List Interface

ConversationLayout of the conversation list is inherited from LinearLayout. The acquisition, synchronization, display, and interaction are all encapsulated in TUIKit. You can use the conversation list UI with the same convenience as a normal Android view.

<ol><li>Set the layout in any layout.xml:

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <com.tencent.qcloud.tim.uikit.modules.conversation.ConversationLayout
        android:id="@+id/conversation_layout"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />

</LinearLayout>
```
</li>
<li>Reference in code:

```java
// Obtain the conversation list panel from the layout file
ConversationLayout conversationLayout = findViewById(R.id.conversation_layout);
// Initialize the conversation list panel
conversationLayout.initDefault();
```
</li></ol>

## Opening the Chat UI

<ol><li>Set the layout in any layout.xml:

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <com.tencent.qcloud.tim.uikit.modules.chat.ChatLayout
        android:id="@+id/chat_layout"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>

</LinearLayout>
```

</li>
<li>Reference in code:

<pre>
// Obtain the chat panel from the layout file
ChatLayout chatLayout = findViewById(R.id.chat_layout);
// Initialize the default UI and interaction of the one-to-one chat panel
chatLayout.initDefault();
// Passes in a ChatInfo instance. This instance must contain required chat information and is usually input by the caller.
// To construct mChatInfo, see the startConversation method of <a href="https://github.com/tencentyun/TIMSDK/blob/master/Android/app/src/main/java/com/tencent/qcloud/tim/demo/menu/StartC2CChatActivity.java">StartC2CChatActivity.java</a>.
chatLayout.setChatInfo(mChatInfo);
</pre>
</li></ol>

## Adding the Contact UI

<ol><li>Set the layout in any layout.xml:
    
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <com.tencent.qcloud.tim.uikit.modules.contact.ContactLayout
        android:id="@+id/contact_layout"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />

</LinearLayout>
```

</li>
<li>Reference in code:

```java
// Obtain the contact panel from the layout file
ContactLayout contactLayout = findViewById(R.id.contact_layout);
// Initialize the default UI and interaction of the contact panel
contactLayout.initDefault();
```
</li></ol>
