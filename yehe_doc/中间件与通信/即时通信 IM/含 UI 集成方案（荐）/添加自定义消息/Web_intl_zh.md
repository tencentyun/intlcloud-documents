TUIKit 默认实现了文本、图片、语音、视频、文件等基本消息类型的发送和展示，如果这些消息类型满足不了您的需求，您可以新增自定义消息类型。


## 自定义消息
如果基本消息类型不能满足您的需求，您可以根据实际业务需求自定义消息。
下文以发送一条可跳转至浏览器的超文本作为自定义消息为例，帮助您快速了解实现流程。


## 展示自定义消息
自定义类消息和其他普通类型消息接收方式一致，所有类型消息都通过监听`TIM.EVENT.MESSAGE_RECEIVED`事件来获取。
收到的自定义消息根据相应的具体类型字段以不同的形式展示在消息列表中 。
下面我们讲解下如何展示自定义消息。

### 创建自定义消息展示结构
自定义消息的展示主要通过在 `messageBubble` 的内容区渲染 `messgaeCustom `实现。
您可以在路径 `src/TUIKit/TUIComponents/container/TUIChat/components/message-custom.vue` 文件下新增您需要的自定义消息展示结构样式。
以超文本类型消息展示结构为例，示例代码如下：
<dx-codeblock>
:::  html
<!-- 判断自定义消息展示类型 -->
<template v-else-if="isCustom.businessID === constant.typeTextLink">
	<div class="textLink">
		<!-- 展示文本 -->
		<p>{{isCustom.text}}</p>
		<!-- 展示超链接 -->
		<a :href="isCustom.link" target="view_window">{{$t('message.custom.查看详情>>')}}</a>
	</div>
</template>
:::
</dx-codeblock>

## 发送自定义消息
您可以通过调用路径 `src/TUIKit/TUIComponents/container/TUIChat/server.ts` 文件中的 `sendCustomMessage` 方法来发送一条自定义消息。 `sendCustomMessage` 接收一个参数 `data` ， `data` 会被作为消息 `Message` 的 `payload` 字段发送，其中参数 `data`  数据里面自定义一个 `businessID` 字段来唯一标识这条自定义消息类型。您可以通过构建不同的 data 数据项来实现发送不同类型的自定义消息。
发送超文本类自定义消息示例代码如下：
<dx-codeblock>
:::  js
const custom = {
	data: {
		// 自定义消息类型的标识字段
		businessID: constant.typeTextLink,
		// 超文本类自定义消息文字说明部分
		text: '欢迎加入腾讯云IM大家庭',
		// 超文本类自定义消息超链接部分
		link: 'https://buy.cloud.tencent.com/avc',
	},
	description: '欢迎加入腾讯云IM大家庭',
	extension: '欢迎加入腾讯云IM大家庭',
};
sendCustomMessage(custom);// 调用 sendCustomMessage 方法发送自定义消息
:::
</dx-codeblock>
