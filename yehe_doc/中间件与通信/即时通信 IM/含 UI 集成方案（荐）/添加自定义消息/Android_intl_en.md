TUIKit implements the sending and display for basic message types such as text, image, audio, video, and file messages by default. If these message types do not meet your requirements, you can add custom message types.

## Basic Message Types
<table>
     <tr>
         <th width="20%" style="text-align:center">Message Type</th>  
         <th style="text-align:center">Renderings</th>  
     </tr>
	 <tr>      
         <td style="text-align:center">Text message</td>   
	 <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/9c9806e98fdf7de1763042463f504ab0.png" width="320"/></td>   
     </tr> 
	 <tr>      
         <td style="text-align:center">Image message</td>   
	 <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/aa32a1838b2e2cf021442658f24c6c2b.png" width="320"/></td>   
     </tr> 
	 <tr>      
         <td style="text-align:center">Audio message</td>   
	 <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/cb3342026953a3294c3c24686a2a642f.png" width="320"/></td>   
     </tr> 
	 <tr>      
         <td style="text-align:center">Video message</td>   
	 <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/6eea956715e88d12f6942e57e9ba2660.png" width="320"/></td>   
     </tr> 
	 <tr>      
         <td style="text-align:center">File message</td>   
	 <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/75d71e975b0c2820cda58a293b356826.png" width="320"/></td>   
     </tr> 
</table>


## Custom Message
If the basic message types do not meet your requirements, you can customize messages as needed. The following uses sending a custom hypertext message that can redirect to the browser as an example to help you quickly understand the implementation process.
The built-in custom message style of TUIKit is shown in the figure below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/ccd1537415821a33b0c860a22d92f830.png" width = "300"/>

> ? In TUIKit 5.8.1668, a new custom message scheme was designed, which introduces many changes compared with the original scheme and is easier to implement. APIs of the original scheme are retained but are no longer maintained.
> We **strongly recommend** you to upgrade to version 5.8.1668 or later to use the new scheme to implement custom messages.


## Displaying a Custom Message
The `cell` element of the built-in custom message of TUIKit is shown in the figure below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/156b57068a297b308a4bf66fdb9daeff.png" width = "500"/>

You can receive a custom message via the `onRecvNewMessage` method in [ChatPresenter.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/TUIKit/TUIChat/tuichat/src/main/java/com/tencent/qcloud/tuikit/tuichat/presenter/ChatPresenter.java), and the received custom message will be displayed in `MessageViewHolder` mode in the message list. The data required for `MessageViewHolder` drawing is called `MessageBean`.

The following introduces how to display a custom message.

### Implement the MessageBean class for the custom message 
1. Create the `CustomLinkMessageBean.java` file in `TUIChat/tuichat/src/main/java/com/tencent/qcloud/tuikit/tuichat/bean/message/`. Inherit data from `TUIMessageBean` to the `CustomLinkMessageBean` class to store the text to display and the link to redirect.
Sample code:
<dx-codeblock>
:::  java
public class CustomLinkMessageBean extends TUIMessageBean {
    private String text;
    private String link;
   
    public String getText() {
        return text;
    }

    public String getLink() {
        return link;
    }
}
:::
</dx-codeblock>

2. Rewrite the `onProcessMessage(message)` method of `CustomLinkMessageBean` to implement custom message parsing.
Sample code:
<dx-codeblock>
:::  java
@Override
public void onProcessMessage(V2TIMMessage v2TIMMessage) {
    // Custom message view implementation. Here we configure to display only the text information and implement link redirection.
    text = TUIChatService.getAppContext().getString(R.string.no_support_msg);
    link = "";
    String data = new String(v2TIMMessage.getCustomElem().getData());
    try {
        HashMap map = new Gson().fromJson(data, HashMap.class);
        if (map != null) {
            text = (String) map.get("text");
            link = (String) map.get("link");
        }
    } catch (JsonSyntaxException e) {

    }
    setExtra(text);
}
:::
</dx-codeblock>

3. Rewrite the `onGetDisplayString()` method of `CustomLinkMessageBean` to generate the text summary in the conversation list.
The implementation effect is as follows:
<img src="https://qcloudimg.tencent-cloud.cn/raw/1555df533bc3a105b4a7f5e7676e1c83.png" width="300"/><br>

Sample code:
<dx-codeblock>
:::  java
@Override
public String onGetDisplayString() {
    return text;
}
:::
</dx-codeblock>


### Implement the MessageViewHolder class
1. Create the `CustomLinkMessageHolder.java` file in `Android/TUIChat/tuichat/src/main/java/com/tencent/qcloud/tuikit/tuichat/classicui/widget/message/viewholder/CallingMessageHolder.java`. Inherit data from `MessageContentHolder` to `CustomLinkMessageHolder` to implement the bubble style layout and click event of the custom message.
Sample code:
<dx-codeblock>
:::  java
public class CustomLinkMessageHolder extends MessageContentHolder {

    public CustomLinkMessageHolder(View itemView) {
        super(itemView);
    }
}
:::
</dx-codeblock>

2. Rewrite the `getVariableLayout` method of `CustomLinkMessageHolder` and go back to the layout of the custom message.
Sample code:
<dx-codeblock>
:::  java
@Override
public int getVariableLayout() {
    return R.layout.test_custom_message_layout1;
}
:::
</dx-codeblock>

3. Rewrite the `layoutVariableViews` method of `CustomLinkMessageHolder` to render the custom message to the layout and add the custom message click event.
Sample code:
<dx-codeblock>
:::  java
@Override
public void layoutVariableViews(TUIMessageBean msg, int position) {
    // Custom message view implementation. Here we configure to display only the text information and implement link redirection.

    TextView textView = itemView.findViewById(R.id.test_custom_message_tv);
    String text = "";
    String link = "";
    if (msg instanceof CustomLinkMessageBean) {
        text = ((CustomLinkMessageBean) msg).getText();
        link = ((CustomLinkMessageBean) msg).getLink();
    }
    textView.setText(text);
    msgContentFrame.setClickable(true);
    String finalLink = link;
    msgContentFrame.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View v) {
            Intent intent = new Intent();
            intent.setAction("android.intent.action.VIEW");
            Uri content_url = Uri.parse(finalLink);
            intent.setData(content_url);
            intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
            TUIChatService.getAppContext().startActivity(intent);
        }
    });

    msgContentFrame.setOnLongClickListener(new View.OnLongClickListener() {
        @Override
        public boolean onLongClick(View v) {
            if (onItemLongClickListener != null) {
                onItemLongClickListener.onMessageLongClick(v, position, msg);
            }
            return false;
        }
    });
}
:::
</dx-codeblock>

### Register the custom message type
In the `initMessageType` method in the `TUIChatService.java` file, call the `addCustomMessageType` method to register the custom message.
Sample code:
<dx-codeblock>
:::  java
private void initMessageType() {
    addCustomMessageType("text_link",                                       // Unique ID of the custom message (Duplicate IDs are not allowed.)
                         CustomLinkMessageBean.class);    // MessageBean type of the message, which is the MessageBean class created in step 1
}
:::
</dx-codeblock>

In the `initMessage` method in the `ClassicUIService.java` file, call the `addMessageType` method to register the mapping between the custom message type and message layout.

Sample code:
<dx-codeblock>
:::  java
public void initMessage() {
    addMessageType(CustomLinkMessageBean.class,       // MessageBean type of the message, which is the MessageBean class created in step 1
                   CustomLinkMessageHolder.class);                     // MessageViewHolder type of the message, which is the MessageViewHolder class created in step 2
}
:::
</dx-codeblock>

## Sending Custom Messages
As the figure below shows, the custom message sending button consists of a text title and an image icon.
<img src="https://qcloudimg.tencent-cloud.cn/raw/e7c26ad63941fb2bc3fb8277bf037ac4.png" width = "500"/>

1. Add code to the `customizeChatLayout` method in [ChatLayoutSetting.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/TUIKit/TUIChat/tuichat/src/main/java/com/tencent/qcloud/tuikit/tuichat/classicui/setting/ChatLayoutSetting.java) to add the custom message sending button.
Sample code:
<dx-codeblock>
:::  java
InputMoreActionUnit unit = new InputMoreActionUnit() {};
unit.setIconResId(R.drawable.custom);
unit.setTitleId(R.string.test_custom_action);
unit.setActionId(CustomHelloMessage.CUSTOM_HELLO_ACTION_ID);
unit.setPriority(10);
inputView.addAction(unit);
:::
</dx-codeblock>

2. Configure click listening for the custom message sending button. Then, when the message sending button is clicked, a custom message is created and sent.
A custom message is a piece of JSON data. You need to define the `businessID` field in JSON to uniquely identify the message type.
Sample code:
<dx-codeblock>
:::  java
unit.setOnClickListener(unit.new OnActionClickListener() {
    @Override
    public void onClick() {
        Gson gson = new Gson();
        CustomHelloMessage customHelloMessage = new CustomHelloMessage();
        customHelloMessage.businessID = "text_link";
        customHelloMessage.text = "Welcome to Tencent Cloud Chat group";
        customHelloMessage.link = "https://cloud.tencent.com/document/product/269/3794";
        String data = gson.toJson(customHelloMessage);
        TUIMessageBean info = ChatMessageBuilder.buildCustomMessage(data, customHelloMessage.text, customHelloMessage.text.getBytes());
        layout.sendMessage(info, false);
    }
});
:::
</dx-codeblock>


[](id:feedback)
