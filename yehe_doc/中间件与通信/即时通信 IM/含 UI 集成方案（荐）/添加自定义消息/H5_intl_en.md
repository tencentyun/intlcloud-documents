TUIKit implements the sending and display for basic message types such as text, image, audio, video, and file messages by default. If these message types do not meet your requirements, you can add custom message types.
## Basic Message Types
<table>
     <tr>
         <th width="20%" style="text-align:center">Message Type</th>  
         <th style="text-align:center">Renderings</th>  
     </tr>
     <tr>      
         <td style="text-align:center">Text message</td>   
     <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/34474d2a250de33c50051c4883278180.png" width="320"/></td>   
     </tr> 
     <tr>      
         <td style="text-align:center">Image message</td>   
     <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/c8d31941d17a8b488e9b07eb8f2066f0.png" width="320"/></td>   
     </tr> 
     <tr>      
         <td style="text-align:center">Audio message</td>   
     <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/50691750b70e407989428ed03a769832.png" width="320"/></td>   
     </tr> 
     <tr>      
         <td style="text-align:center">Video message</td>   
     <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/849714515d6dbf26ca22d39ed8447a7d.png" width="320"/></td>   
     </tr> 
     <tr>      
         <td style="text-align:center">File message</td>   
     <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/7b8b2b174c47edde21da824dd0bb7501.png" width="320"/></td>   
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
     <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/bb48f9f54920c1e9b6177e02fbec027d.png" width="320"/></td>   
     </tr> 
     <tr>      
         <td style="text-align:center">Rating message</td>   
     <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/1511274092783b6f2cad1a53e8475b33.png" width="320"/></td>   
     </tr> 
     <tr>      
         <td style="text-align:center">Order message</td>   
     <td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/ffec53acb6269ada940ffd8048d87e8d.png" width="320"/></td>   
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

