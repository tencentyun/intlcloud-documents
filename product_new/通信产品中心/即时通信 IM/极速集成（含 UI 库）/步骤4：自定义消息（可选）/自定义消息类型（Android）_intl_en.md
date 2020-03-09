
TUIKit renders basic messages internally, and therefore you can modify message display styles through properties, or you can create custom message styles.

## Basic Message Types
For basic message types in TUIKit, see [MessageInfo.java](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/modules/message/MessageInfo.html).
<table>
     <tr>
         <th width="20%" style="text-align:center">Message Type</th>  
         <th style="text-align:center">Display</th>  
     </tr>
	 <tr>      
         <td style="text-align:center">Text</td>   
	 <td style="text-align:center"><img src="https://main.qcloudimg.com/raw/6535b0a414d4dd51aabab464f0980ca3.png" width="320"/></td>   
     </tr> 
	 <tr>      
         <td style="text-align:center">Image</td>   
	 <td style="text-align:center"><img src="https://main.qcloudimg.com/raw/1f5330a92c688b6288bbd47f97202867.png" width="320"/></td>   
     </tr> 
	 <tr>      
         <td style="text-align:center">Audio</td>   
	 <td style="text-align:center"><img src="https://main.qcloudimg.com/raw/5387ea2450e7fe37daa59efb163e93b6.png" width="320"/></td>   
     </tr> 
	 <tr>      
         <td style="text-align:center">Video</td>   
	 <td style="text-align:center"><img src="https://main.qcloudimg.com/raw/eb50c8cefa0decf1eef1c896c44e6188.png" width="320"/></td>   
     </tr> 
	 <tr>      
         <td style="text-align:center">File</td>   
	 <td style="text-align:center"><img src="https://main.qcloudimg.com/raw/4be73ac319f7693916ee08b98f14c4c6.png" width="320"/></td>   
     </tr> 
</table>

## Custom Messages
In addition to using the basic message types, you can customize messages based on your business needs.
This document uses a hypertext that jumps to the browser as an example to guide you through the message customization process.

### Creating a custom message

The MessageInfoUtil class helps you implement various message types including custom messages. For example, you can create a custom message in a JSON string:
```java
MessageInfo info = MessageInfoUtil.buildCustomMessage("{\"text\": \"Welcome to IM! Learn more >>\",\"url\": \"https://cloud.tencent.com/product/im"}");
```

### Sending a custom message

You can send a custom message through a ChatLayout instance:
```java
chatLayout.sendMessage(info)
```


### Rendering custom messages

You can define, parse, and display custom messages based on your business needs. These messages are then passed through to the recipient by TUIKit, and TUIKit calls the callback that you implemented to render the messages. The callback normally includes the following steps:
1. Parse the custom message.
2. Create a display view based on the parsing result.
3. Add the created view to a parent container in TUIKit.
4. Implement the interaction logic of the view.

The following figure shows the process of rendering a custom message:
![](https://main.qcloudimg.com/raw/644f6a44045300f48d98440ceb150bb3.png)

TUIKit obtains the type of the custom message internally. TUIKit notifies you when this message is rendered and calls the layout and implementation logic. Therefore, you only need to pass the implemented `IOnCustomMessageDrawListener` into TUIKit.
```java
// Set the callback for custom message rendering
messageLayout.setOnCustomMessageDrawListener(new CustomMessageDraw());
```

### Sample code

The following sample code shows the full process of customizing a message. You can also [download](https://github.com/tencentyun/TIMSDK/blob/master/Android/app/src/main/java/com/tencent/qcloud/tim/demo/helper/ChatLayoutHelper.java) the complete demo.
```java
public static class CustomMessageDraw implements IOnCustomMessageDrawListener {

    /**
         * This method is called when a custom message is rendered. The method creates a custom message and implements the interaction logic.
         * @param parent Customize the parent view of the custom message. To do this, you need to add the view of the custom message to parent.
         * @param info Information in the message
         */
    @Override
    public void onDraw(ICustomMessageViewGroup parent, MessageInfo info) {
        View view = null;
        // Obtain the JSON data of the custom message
        TIMCustomElem elem = (TIMCustomElem) info.getTIMMessage().getElement(0);
        // Parse the custom JSON data into a bean instance
        final CustomMessageData customMessageData = new Gson().fromJson(new String(elem.getData()), CustomMessageData.class);
        // Create different custom message display views through types
        switch(customMessageData.type) {
            case CustomMessageData.TYPE_HYPERLINK:
                view = LayoutInflater.from(DemoApplication.instance()).inflate(R.layout.test_custom_message_layout1, null, false);
                // Add the view of the custom message to the parent container in TUIKit
                parent.addMessageContentView(view);
                break;
            case CustomMessageData.TYPE_PUSH_TEXT_VIDEO:
                view = LayoutInflater.from(DemoApplication.instance()).inflate(R.layout.test_custom_message_layout2, null, false);
                // Add the view of the custom message to the parent container in TUIKit
                parent.addMessageItemView(view);
                break;
        }

        // Implement the view of the custom message. This example displays the text and implements hyperlink redirection.
        TextView textView = view.findViewById(R.id.test_custom_message_tv);
        textView.setText(customMessageData.text);
        textView.setClickable(true);
        textView.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent();
                intent.setAction("android.intent.action.VIEW");
                Uri content_url = Uri.parse(customMessageData.url);
                intent.setData(content_url);
                intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
                DemoApplication.instance().startActivity(intent);
            }
        });
    }
}

/**
 * Define the bean entity of the custom message, which can be converted to and from the JSON format
 */
public static class CustomMessageData {
    // Hypertext, which redirects to a Webview when clicked
    final static int TYPE_HYPERLINK = 1;
    // Video + description
    final static int TYPE_PUSH_TEXT_VIDEO = 2;
    // Custom message, which can be of various types depending on business needs
    int type = TYPE_HYPERLINK;
    String text = "Welcome to IM! Learn more >>";
    String url = "https://cloud.tencent.com/document/product/269";
}
```

The following figure shows the result:
![](https://main.qcloudimg.com/raw/019fe0810738f271b61cd1d7a33c5b03.png)
