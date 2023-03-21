TUIKit 默认实现了文本、图片、语音、视频、文件等基本消息类型的发送和展示，如果这些消息类型满足不了您的需求，您可以新增自定义消息类型。

## 基本消息类型
<table>
     <tr>
         <th width="20%" style="text-align:center">消息类型</th>  
         <th style="text-align:center">显示效果图</th>  
     </tr>
	 <tr>      
         <td style="text-align:center">文本类消息</td>   
	 <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/9c9806e98fdf7de1763042463f504ab0.png" width="320"/></td>   
     </tr> 
	 <tr>      
         <td style="text-align:center">图片类消息</td>   
	 <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/aa32a1838b2e2cf021442658f24c6c2b.png" width="320"/></td>   
     </tr> 
	 <tr>      
         <td style="text-align:center">语音类消息</td>   
	 <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/cb3342026953a3294c3c24686a2a642f.png" width="320"/></td>   
     </tr> 
	 <tr>      
         <td style="text-align:center">视频类消息</td>   
	 <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/6eea956715e88d12f6942e57e9ba2660.png" width="320"/></td>   
     </tr> 
	 <tr>      
         <td style="text-align:center">文件类消息</td>   
	 <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/75d71e975b0c2820cda58a293b356826.png" width="320"/></td>   
     </tr> 
</table>


## 自定义消息
如果基本消息类型不能满足您的需求，您可以根据实际业务需求自定义消息。下文以发送一条可跳转至浏览器的超文本作为自定义消息为例，帮助您快速了解实现流程。
TUIKit 内置的自定义消息样式如下图所示：
<img src="https://qcloudimg.tencent-cloud.cn/raw/ccd1537415821a33b0c860a22d92f830.png" width = "300"/>

> ? TUIKit 在 5.8.1668 版本重新设计了一套自定义消息方案，新方案较旧方案有很大的改动，实现起来更简单快捷。旧方案 API 继续保留，但不再维护。
> 我们**强烈建议**您升级到 5.8.1668 及以上版本，使用新方案实现自定义消息。


## 展示自定义消息
TUIKit 内置的自定义消息 cell 元素如下图所示：
<img src="https://qcloudimg.tencent-cloud.cn/raw/156b57068a297b308a4bf66fdb9daeff.png" width = "500"/>

您可以在 [ChatPresenter.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/TUIKit/TUIChat/tuichat/src/main/java/com/tencent/qcloud/tuikit/tuichat/presenter/ChatPresenter.java) 的 `onRecvNewMessage` 方法中接收自定义消息。收到的自定义消息最终会以 `MessageViewHolder` 的形式展示在消息列表中，`MessageViewHolder` 绘制所需的数据我们称之为 `MessageBean`。

下面我们分步骤讲解下如何展示自定义消息。

### 实现自定义消息 MessageBean 类 
1. 在 `TUIChat/tuichat/src/main/java/com/tencent/qcloud/tuikit/tuichat/bean/message/` 文件夹下新建 `CustomLinkMessageBean.java` 文件，`CustomLinkMessageBean` 类继承自 `TUIMessageBean`，用于存储显示的文字和要跳转的链接。
示例代码如下：
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

1. 重写 `CustomLinkMessageBean` 的 `onProcessMessage(message)` 方法，用于实现对自定义消息的解析。
示例代码如下：
<dx-codeblock>
:::  java
@Override
public void onProcessMessage(V2TIMMessage v2TIMMessage) {
    // 自定义消息view的实现，这里仅仅展示文本信息，并且实现超链接跳转
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

3. 重写 `CustomLinkMessageBean` 的 `onGetDisplayString()` 方法，用于生成在会话列表中的文字摘要。
实现后的效果如下：
<img src="https://qcloudimg.tencent-cloud.cn/raw/1555df533bc3a105b4a7f5e7676e1c83.png" width="300"/><br>

示例代码如下：
<dx-codeblock>
:::  java
@Override
public String onGetDisplayString() {
    return text;
}
:::
</dx-codeblock>


### 实现 MessageViewHolder 类
1. 在 `Android/TUIChat/tuichat/src/main/java/com/tencent/qcloud/tuikit/tuichat/classicui/widget/message/viewholder/CallingMessageHolder.java` 文件夹下新建 `CustomLinkMessageHolder.java` 文件，`CustomLinkMessageHolder` 继承自 `MessageContentHolder` ，用于实现自定义消息气泡的样式布局和点击事件。
示例代码如下：
<dx-codeblock>
:::  java
public class CustomLinkMessageHolder extends MessageContentHolder {

    public CustomLinkMessageHolder(View itemView) {
        super(itemView);
    }
}
:::
</dx-codeblock>

2. 重写 `CustomLinkMessageHolder` 的 `getVariableLayout` 方法，返回展示自定义消息的布局。
示例代码如下：
<dx-codeblock>
:::  java
@Override
public int getVariableLayout() {
    return R.layout.test_custom_message_layout1;
}
:::
</dx-codeblock>

3. 重写 `CustomLinkMessageHolder` 的 `layoutVariableViews` 方法，用于把自定义消息渲染到布局上，并添加自定义消息的点击事件。
示例代码如下：
<dx-codeblock>
:::  java
@Override
public void layoutVariableViews(TUIMessageBean msg, int position) {
    // 自定义消息view的实现，这里仅仅展示文本信息，并且实现超链接跳转

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

### 注册自定义消息类型
在 `TUIChatService.java` 文件的 `initMessageType` 方法中，调用 `addCustomMessageType` 方法注册自定义消息。
示例代码如下：
<dx-codeblock>
:::  java
private void initMessageType() {
    addCustomMessageType("text_link",                     // 自定义消息唯一标识（注意不能重复）
                         CustomLinkMessageBean.class);    // 消息 MessageBean 类型，步骤一中创建的 MessageBean 类
}
:::
</dx-codeblock>

在 `ClassicUIService.java` 文件的 `initMessage` 方法中，调用 `addMessageType` 方法注册自定义消息类型与消息布局的映射关系。

示例代码如下：
<dx-codeblock>
:::  java
public void initMessage() {
    addMessageType(CustomLinkMessageBean.class,       // 消息 MessageBean 类型，步骤一中创建的 MessageBean 类
                   CustomLinkMessageHolder.class);    // 消息 MessageViewHolder 类型，步骤二中创建的 MessageViewHolder 类
}
:::
</dx-codeblock>

## 发送自定义消息
如下图所示，自定义消息发送按钮主要由文本 `title` 和图片 `icon` 组成：
<img src="https://qcloudimg.tencent-cloud.cn/raw/e7c26ad63941fb2bc3fb8277bf037ac4.png" width = "500"/>

1. 在 [ChatLayoutSetting.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/TUIKit/TUIChat/tuichat/src/main/java/com/tencent/qcloud/tuikit/tuichat/classicui/setting/ChatLayoutSetting.java) 的 `customizeChatLayout` 方法中添加代码，添加自定义消息发送按钮。
示例代码如下：
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

2. 为上面步骤创建的自定义消息发送按钮设置点击监听，点击消息发送按钮后就可以创建一条自定义消息发送。
自定义消息是一段 JSON 数据，在 JSON 中定义 `businessID` 字段来唯一标识这条消息类型。
示例代码如下：
<dx-codeblock>
:::  java
unit.setOnClickListener(unit.new OnActionClickListener() {
    @Override
    public void onClick() {
        Gson gson = new Gson();
        CustomHelloMessage customHelloMessage = new CustomHelloMessage();
        customHelloMessage.businessID = "text_link";
        customHelloMessage.text = "欢迎加入云通信IM大家庭！";
        customHelloMessage.link = "https://cloud.tencent.com/document/product/269/3794";
        String data = gson.toJson(customHelloMessage);
        TUIMessageBean info = ChatMessageBuilder.buildCustomMessage(data, customHelloMessage.text, customHelloMessage.text.getBytes());
        layout.sendMessage(info, false);
    }
});
:::
</dx-codeblock>


[](id:feedback)
