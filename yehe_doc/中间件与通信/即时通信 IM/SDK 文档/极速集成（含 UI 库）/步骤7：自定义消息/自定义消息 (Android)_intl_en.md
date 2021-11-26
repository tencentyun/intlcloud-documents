
'TUIKit' has already rendered basic messages internally. You can easily adjust the message presentation style by setting attributes, or you can re-customize the message style.


## Basic Message Types


<table>
     <tr>
         <th width="20%" style="text-align:center">Message Type</th>  
         <th style="text-align:center">Renderings</th>  
     </tr>
	 <tr>      
         <td style="text-align:center">Text message</td>   
	 <td style="text-align:center"><img src="https://main.qcloudimg.com/raw/751b6975a0a786dac0f35aabc0aa90e2.png" width="320"/></td>   
     </tr> 
	 <tr>      
         <td style="text-align:center">Image message</td>   
	 <td style="text-align:center"><img src="https://main.qcloudimg.com/raw/02cff177167e31feaa447d414d2e77f4.png" width="320"/></td>   
     </tr> 
	 <tr>      
         <td style="text-align:center">Voice message</td>   
	 <td style="text-align:center"><img src="https://main.qcloudimg.com/raw/95447ed8a0c4dcf37c118758f44788e4.png" width="320"/></td>   
     </tr> 
	 <tr>      
         <td style="text-align:center">Video message</td>   
	 <td style="text-align:center"><img src="https://main.qcloudimg.com/raw/564c492d9fc621882b39a5a420436081.png" width="320"/></td>   
     </tr> 
	 <tr>      
         <td style="text-align:center">File message</td>   
	 <td style="text-align:center"><img src="https://main.qcloudimg.com/raw/32dc502005f11f9caa53937a3f1c20cf.png" width="320"/></td>   
     </tr> 
</table>


## Customizing Messages
>- If the basic message types do not meet your requirements, you can customize messages as needed.
>- This document uses sending a custom hypertext message that can redirect to the browser as an example to help you quickly understand the implementation process. **This document uses version '5.4.666' as an example, which is different from previous versions.**

### Process of implementing message customization
Message customization process
<img src="https://main.qcloudimg.com/raw/3f53c72359285be215f72d0b7f01c38d.png" width="1000"/>
As shown in the figure above, `TUIChatControllerListener` and `TUIConversationControllerListener` must be implemented for custom messages. `TUIChatControllerListener` is used to parse messages and generate the custom `MessageInfo` and create and populate the custom `ViewHolder` to be displayed on the chat page. `TUIConversationControllerListener` is used to generate the message abstract to be displayed on the conversation list.

>- `TUIKit` uses `RecyclerView` to display messages. To display custom messages, you need to create a custom message `ViewHolder` to store the `view` for displaying the content of custom messages.
>- You need to register your own `TUIChatControllerListener` and `TUIConversationControllerListener` with `TUIKitListenerManager` as soon as possible.
### Creating a custom welcome message
Customize `MessageInfo` and implement the custom message parsing method.
```java
public class HelloChatController implements TUIChatControllerListener {
    // Define that `HelloMessageInfo` is inherited from `MessageInfo`
    static class HelloMessageInfo extends MessageInfo {
        // Specify the message type ID, which cannot be repeated, including not repeated with the ID of a built-in message type. A number greater than 100002 is recommended.
        public static final int MSG_TYPE_HELLO = 100002;
    }

    // Implement the `createCommonInfoFromTimMessage` method of TUIChatControllerListener to parse messages and generate `MessageInfo`
    // If the message is customized by yourself, the custom `MessageInfo` is generated and returned. Otherwise, `null` is returned, indicating that processing cannot be performed.
    @Override
    public IBaseInfo createCommonInfoFromTimMessage(V2TIMMessage timMessage) {
        if (timMessage.getElemType() == V2TIMMessage.V2TIM_ELEM_TYPE_CUSTOM) {
            V2TIMCustomElem customElem = timMessage.getCustomElem();
            if (customElem == null || customElem.getData() == null) {
                return null;
            }
            CustomHelloMessage helloMessage = null;
            try {
                helloMessage = new Gson().fromJson(new String(customElem.getData()), CustomHelloMessage.class);
            } catch (Exception e) {
                DemoLog.w(TAG, "invalid json: " + new String(customElem.getData()) + " " + e.getMessage());
            }
            if (helloMessage != null && TextUtils.equals(helloMessage.businessID, TUIKitConstants.BUSINESS_ID_CUSTOM_HELLO)) {
                MessageInfo messageInfo = new HelloMessageInfo();
                // Set the message type ID, which is required
                messageInfo.setMsgType(HelloMessageInfo.MSG_TYPE_HELLO);
                // Settings
                MessageInfoUtil.setMessageInfoCommonAttributes(messageInfo, timMessage);
                Context context = TUIKit.getAppContext();
                if (context != null) {
                    messageInfo.setExtra(context.getString(R.string.custom_msg));
                }
                return messageInfo;
            }
        }
        return null;
    }

    ......

}
```
Register `TUIChatControllerListener` with `TUIKitListenerManager` as soon as possible.
```java
TUIKitListenerManager.getInstance().addChatListener(new HelloChatController());
```
You can create a custom message via a JSON string.
```java
Gson gson = new Gson();
CustomHelloMessage customHelloMessage = new CustomHelloMessage();
customHelloMessage.version = TUIKitConstants.version;
customHelloMessage.text = DemoApplication.instance().getString(R.string.welcome_tip);
customHelloMessage.link = "https://cloud.tencent.com/document/product/269/3794";

String data = gson.toJson(customHelloMessage); // data = {"businessID":"text_link","link":"https://cloud.tencent.com/document/product/269/3794","text":"Welcome to IM","version":4}
// Creating a custom message based on a JSON string will call the rewritten `createCommonInfoFromTimMessage` method to parse messages and generate `MessageInfo`.
MessageInfo info = MessageInfoUtil.buildCustomMessage(data);
```
### Sending a custom message

You can use the `ChatLayout` instance to send a custom message:
```java
MessageInfo info = MessageInfoUtil.buildCustomMessage(data);
chatLayout.sendMessage(info)
```
You can also use `MessageSender` to send the message.
```java
MessageInfo info = MessageInfoUtil.buildCustomMessage(data);
IBaseMessageSender messageSender = TUIKitListenerManager.getInstance().getMessageSender();
if (messageSender != null) {
    // Send the message
    messageSender.sendMessage(info, null, chatInfoId,
            chatType == V2TIMConversation.V2TIM_GROUP, false, new IUIKitCallBack() {
                @Override
                public void onSuccess(Object data) {
                    Log.i("CustomChatController", "send success");
                }

                @Override
                public void onError(String module, int errCode, String errMsg) {
                    Log.i("CustomChatController", "send failed");
                }
            });
}
```

### Displaying a custom message in the chat box

#### Creating ViewHolder
`TUIKit` uses `RecyclerView` to display messages. To display custom messages, you need to create a custom message `ViewHolder` to store the `view` for displaying the content of custom messages.
The `ViewHolder` of a custom message can be inherited from the [basic message ViewHolder](https://github.com/tencentyun/TIMSDK/tree/master/Android/Demo/tuikit/src/main/java/com/tencent/qcloud/tim/uikit/modules/chat/layout/message/holder).
```java
// Define that `HelloViewHolder` is inherited from `MessageCustomHolder`
class HelloViewHolder extends MessageCustomHolder{

    public HelloViewHolder(View itemView) {
        super(itemView);
    }
}

// Implement the `createCommonViewHolder` method of `TUIChatControllerListener` to create a ViewHolder
// Create a custom ViewHolder based on `viewType`. For a non-custom message, `null` is returned
@Override
public IBaseViewHolder createCommonViewHolder(ViewGroup parent, int viewType) {
    if (viewType != HelloMessageInfo.MSG_TYPE_HELLO) {
        return null;
    }
    if (parent == null) {
        return null;
    }
    LayoutInflater inflater = LayoutInflater.from(TUIKit.getAppContext());
    View contentView = inflater.inflate(R.layout.message_adapter_item_content, parent, false);
    return new HelloViewHolder(contentView);
}
```
#### Setting the display content for a custom message
When displaying a message, `TUIKit` calls the `bindCommonViewHolder` method to set the custom message content.
```java
// Implement the `bindCommonViewHolder` method of `TUIChatControllerListener` to populate the ViewHolder
// If the ViewHolder is a custom one, set the display content and return `true`, indicating that processing is completed. Otherwise, `false` is returned.
@Override
public boolean bindCommonViewHolder(IBaseViewHolder baseViewHolder, IBaseInfo baseInfo, int position) {
    if (baseViewHolder instanceof ICustomMessageViewGroup && baseInfo instanceof HelloMessageInfo) {
        ICustomMessageViewGroup customHolder = (ICustomMessageViewGroup) baseViewHolder;
        MessageInfo msg = (MessageInfo) baseInfo;
        new CustomMessageDraw().onDraw(customHolder, msg, position);
        return true;
    }
    return false;
}
```

### Displaying the custom message abstract in the conversion list
```java
// Define that `HelloConversationController` implements the `TUIConversationControllerListener` API
public static class HelloConversationController implements TUIConversationControllerListener {
    // Obtain the abstract string to be displayed in the conversion list. If the message is not the current user's custom message, `null` is returned, indicating no processing.
    @Override
    public CharSequence getConversationDisplayString(IBaseInfo baseInfo) {
        if (baseInfo instanceof HelloChatController.HelloMessageInfo) {
            return DemoApplication.instance().getString(R.string.welcome_tip);
        }
        return null;
    }
}
// Register `TUIConversationControllerListener` with `TUIKitListenerManager` as soon as possible so that the custom message abstract can be properly displayed in the conversion list.
TUIKitListenerManager.getInstance().addConversationListener(new HelloChatController.HelloConversationController());
```


