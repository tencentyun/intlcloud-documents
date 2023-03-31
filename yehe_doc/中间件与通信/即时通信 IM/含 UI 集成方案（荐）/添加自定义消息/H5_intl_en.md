TUIKit implements the sending and display for basic message types such as text, image, audio, video, and file messages by default. If these message types do not meet your requirements, you can add custom message types.


## Customizing a Message
If the basic message types do not meet your requirements, you can customize messages as needed.
The following uses sending a custom hypertext message that can redirect to the browser as an example to help you quickly understand the implementation process.


## Displaying a Custom Message
Custom messages are received in the same way as other common messages. All types of messages are obtained by listening for the `TIM.EVENT.MESSAGE_RECEIVED` event.
The received custom messages are displayed in the message list in different forms according to the corresponding specific type field.
The following introduces how to display a custom message.

### Creating the display structure for the custom message
The display of a custom message is implemented by rendering `messgaeCustom` in the content area of `messageBubble`.
You can add the display structure style for the custom message in the `src/TUIKit/TUIComponents/container/TUIChat/components/message-custom.vue` file.
The following code sample shows how to add the display structure for a hypertext message:
<dx-codeblock>
:::  html
<!-- Determine the custom message display type -->
<template v-else-if="isCustom.businessID === constant.typeTextLink">
	<div class="textLink">
		<!-- Displayed text -->
		<p>{{isCustom.text}}</p>
		<!-- Displayed hyperlink -->
		<a :href="isCustom.link" target="view_window">{{$t('message.custom.View Details>>')}}</a>
	</div>
</template>
:::
</dx-codeblock>

## Sending a Custom Message
You can call the `sendCustomMessage` method in the `src/TUIKit/TUIComponents/container/TUIChat/server.ts` file to send a custom message. If you specify the `data` parameter, `sendCustomMessage` sends it as the `payload` field of `Message`. You can customize the `businessID` field in `data` to uniquely identify the custom message type. To send different types of custom messages, you only need to build different `data` items.
The following code sample shows how to send a hypertext custom message:
<dx-codeblock>
:::  js
const custom = {
	data: {
		// Field that specifies the custom message type
		businessID: constant.typeTextLink,
		// Text description of the hypertext custom message
		text: 'Welcome to Tencent Cloud IM group',
		// Hyperlink of the hypertext custom message
		link: 'https://buy.cloud.tencent.com/avc',
	},
	description: ''Welcome to Tencent Cloud IM group',
	extension: ''Welcome to Tencent Cloud IM group',
};
sendCustomMessage(custom);// Call the `sendCustomMessage` method to send the custom message
:::
</dx-codeblock>
