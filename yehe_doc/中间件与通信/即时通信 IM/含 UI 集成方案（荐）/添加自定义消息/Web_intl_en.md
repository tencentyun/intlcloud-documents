TUIKit implements the sending and display for basic message types such as text, image, audio, video, and file messages by default. If these message types do not meet your requirements, you can add custom message types.

## Basic Message Types
<table>
     <tr>
         <th width="20%" style="text-align:center">Message Type</th>  
         <th style="text-align:center">Renderings</th>  
     </tr>
     <tr>      
         <td style="text-align:center">Text message</td>   
     <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/9cb4ed8a616242ef1af2c95deede7d41.png" width="320"/></td>   
     </tr> 
     <tr>      
         <td style="text-align:center">Image message</td>   
     <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/f55d26506d6d5a00e0155a682d55379b.png" width="320"/></td>   
     </tr> 
     <tr>      
         <td style="text-align:center">Audio message</td>   
     <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/c391f8425e3274abc13ef22e7ab1b0bf.png" width="320"/></td>   
     </tr> 
     <tr>      
         <td style="text-align:center">Video message</td>   
     <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/5778254c16b8bbe925e1c5f2a72c22ea.png" width="320"/></td>   
     </tr> 
     <tr>      
         <td style="text-align:center">File message</td>   
     <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/3b2bfdd4135840a07359c08b4c10aaea.png" width="320"/></td>   
     </tr> 
</table>

## Customizing a Message
If the basic message types do not meet your requirements, you can customize messages as needed.
TUIKit provides several custom message styles:
<table>
     <tr>
         <th width="20%" style="text-align:center">Preset Custom Message Style</th>  
         <th style="text-align:center">Renderings</th>  
     </tr>
     <tr>      
         <td style="text-align:center">Hypertext message</td>   
     <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/ba0942914ab685b2f787c2eb9562a071.png" width="320"/></td>   
     </tr> 
     <tr>      
         <td style="text-align:center">Rating message</td>   
     <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/7a48e2fcc4b8480f7c41ff2bfbdf47a5.png" width="320"/></td>   
     </tr> 
     <tr>      
         <td style="text-align:center">Order message</td>   
     <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/2ab2d710f7b5d1fe94099942992678c6.png" width="320"/></td>   
     </tr> 
</table>
The following uses sending a custom hypertext message that can redirect to the browser as an example to help you quickly understand the implementation process.


## Displaying a Custom Message
The `cell` element of the built-in custom message of TUIKit is shown in the figure below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/d199be3f5a4ff5693d4f80b62afb262f.png" width = "500"/>
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

