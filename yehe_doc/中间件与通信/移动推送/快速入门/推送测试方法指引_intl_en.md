## Actions
Tencent Push Notification Service provides multiple push methods. You can test message pushes in different scenarios as instructed in this document. If you don't have enough testing devices, you can use the [Cloud Phone](https://wetest.qq.com/) service provided by WeTest.

##  Testing Basic Features

###  Push to all devices (broadcasting)

| Tested Feature | Push to all devices |
| --- | --- |
| Test Objective | To verify that a message can be pushed to all devices. |
| Test Environment | Network environment: Wi-Fi or 4G<br>Device: one or more mainstream Android or iOS devices, as applicable |
| Prerequisites | The Tencent Push Notification Service SDK has been integrated, and device registration has been successfully completed. |
| Procedure | Call the relevant API or select all devices as the push target in the console to push a message to all devices. |
| Expected Result | All the devices receive the message. |

###  Push to a single device

| Tested Feature | Push to a single device |
| --- | --- |
| Test Objective | To verify that a message can be pushed to a single device based on the device token. |
| Test Environment | Network environment: Wi-Fi or 4G<br>Device: one or more mainstream Android or iOS devices, as applicable |
| Prerequisites | The Tencent Push Notification Service SDK has been integrated, and device registration has been successfully completed. |
| Procedure | 1. Obtain the token information of the device to be tested. <br>2. Call the relevant API or select a token as the push target in the console to push a message. |
| Expected Result | The phone receives the message. |

### Push to a single account

| Tested Feature | Push to a single account |
| --- | --- |
| Test Objective | To verify that a message can be pushed to a single account. |
| Test Environment | Network environment: Wi-Fi or 4G<br>Device: one or more mainstream Android or iOS devices, as applicable  |
| Prerequisites | - |
| Procedure | 1. Call the SDK API on the mobile app to bind the account. <br>2. After the specified account has been bound to the device token, push a message to this account through the relevant API or in the console. |
| Expected Result | The device bound to the account receives the message. |
| Remarks | [Binding an account on Android](https://www.tencentcloud.com/document/product/1024/30715#binding-an-account)<br>[Binding an account on iOS](https://www.tencentcloud.com/document/product/1024/30727#.E8.B4.A6.E5.8F.B7.E5.8A.9F.E8.83.BD) |

###  Push to a list of accounts

| Tested Feature | Push to a list of accounts |
| --- | --- |
| Test Objective | To verify that a message can be pushed to a list of accounts. |
| Test Environment | Network environment: Wi-Fi or 4G<br>Device: one or more mainstream Android or iOS devices, as applicable  |
| Prerequisites | - |
| Procedure | Call the relevant API or use the console to push messages to the bound accounts. |
| Expected Result |  The devices bound with the accounts receive the message. |
| Remarks | [Binding an account on Android](https://www.tencentcloud.com/document/product/1024/30715#binding-an-account)<br>[Binding an account on iOS](https://www.tencentcloud.com/document/product/1024/30727#.E8.B4.A6.E5.8F.B7.E5.8A.9F.E8.83.BD) |

###  Push to devices with specified tags
You can use the console or relevant API to push messages to devices with specified tags, and the API allows you to set "AND" and "OR" relationships for multiple tags.

| Tested Feature | Push to devices with specified tags |
| --- | --- |
| Test Objective | To verify that you can set tags for different user groups and then push messages to the user groups by tag names. |
| Test Environment |  Network environment: Wi-Fi or 4G<br>Device: one or more mainstream Android or iOS devices, as applicable |
| Prerequisites |  The Tencent Push Notification Service SDK has been integrated, and you have successfully set custom tags. |
| Procedure | 1. When creating a push task in the console, select one or more custom or system preset tags, set the "AND" or "OR" relationship, and start the push.<br>2. Call the relevant API to select one or more custom tags, set the "AND" or "OR" relationship, and start the push. |
| Expected Result | The user groups with the specified tags received the messages. |
| Remarks | [API for setting custom tags (Android)](https://www.tencentcloud.com/document/product/1024/30715#setting-custom-tags)<br>[API for setting custom tags (iOS)](https://www.tencentcloud.com/document/product/1024/30727#.E6.A0.87.E7.AD.BE.E5.8A.9F.E8.83.BD)  |

## Advanced Feature Tests

### Push through multiple vendor channels

| Tested Feature | Push through multiple vendor channels |
| --- | --- |
| Test Objective | To verify that a message can be received after the application process is ended on a device. |
| Test Environment | Mi, Huawei, Meizu, OPPO, and vivo models are required. For FCM, Google Play must be installed. |
| Prerequisites | 1. You have signed up with these vendors' push platforms and created the required application.<br>2. You have configured vendor channels on the [Configuration Management](https://console.cloud.tencent.com/tpns/app-config) page.<br>3. You have integrated the SDK according to the integration methods for different vendor channels provided on the official website.<br>4. You have enabled the vendor channels in the SDK. |
| Procedure | 1. Install the app integrated with the vendor channel on a phone.<br>2. Sign up with the vendor channel and get the vendor token.<br>3. Push a message to the phone through the relevant API or in the console. |
| Expected Result | The message can be successfully pushed to a single device or all devices after the Tencent Push Notification Service application runs in the background and all application processes are ended. |
| Remarks | For Huawei Push, you need to use a signed package. For more information, see [here](https://www.tencentcloud.com/document/product/1024).   |

###  Scheduled push

| Tested Feature | Scheduled push |
| --- | --- |
| Test Objective | To verify that a message can be successfully pushed at a specified time point. |
| Test Environment | Network environment: Wi-Fi or 4G<br>Device: one or more mainstream Android or iOS devices, as applicable |
| Prerequisites | The Tencent Push Notification Service SDK has been integrated, and device registration has been successfully completed. |
| Procedure | 1. Set the push time through the relevant API or in the console.<br>2. Select all devices or a tag as the push target. |
| Expected Result | The tested phones receive the messages at the specified time. |
| Remarks | Scheduled push is supported only by push to all devices and push to devices with specified tags. |

###  Loop push

| Tested Feature | Loop push |
| --- | --- |
| Test Objective | To verify that a message can be received when the customized looping conditions (loop push date and loop type) are met. |
| Test Environment | Network environment: Wi-Fi or 4G<br>Device: one or more mainstream Android or iOS devices, as applicable |
| Prerequisites | The Tencent Push Notification Service SDK has been integrated, and device registration has been successfully completed. |
| Procedure | 1. Set the loop push time and loop type through the relevant API or in the console.<br>2. Select all devices or a tag as the push target. |
| Expected Result | When the loop conditions are met, the tested phones receive the message. |
| Remarks | Loop push is supported only by push to all devices and push to devices with specified tags. |

###  In-app message push
Messages directly passed through to Android devices are not displayed on the notification bar. They will be handled by the Tencent Push Notification Service application after being received.

| Tested Feature | In-app message push |
| --- | --- |
| Test Objective | To verify in-app message push. |
| Test Environment | Network environment: Wi-Fi or 4G<br>Device: one or more mainstream Android or iOS devices, as applicable   |
| Prerequisites | The Tencent Push Notification Service SDK has been integrated, and device registration has been successfully completed. |
| Procedure | Push an in-app message in the console or through the relevant API. |
| Expected Result | The application can receive the in-app message. |

###  Rich media push
You can push multimedia (rich media) messages containing information such as images, audio, and videos to clients.

| Tested Feature | Rich media push |
| --- | --- |
| Test Objective | To verify that a rich media message such as an image can be successfully pushed. |
| Test Environment | Network environment: Wi-Fi or 4G<br>Device: one or more mainstream Android or iOS devices, as applicable  |
| Prerequisites | **Android**: messages with rich media will be delivered only through the Tencent Push Notification Service channel. Images in native Android systems are available in big images and thumbnails, whose display effects vary by model and custom system.<br>1. Android supports static images, audio, and videos as rich media content.<br>2. The image resolution should be 430\*2303, and the rich media link can only use HTTPS.<br>3. For audio/video rich media, you need to create an .xml file after integrating the SDK. For more information, please see [Instructions for Audio/Video Rich Media](https://www.tencentcloud.com/document/product/1024/30713). <br>**iOS**: the system supports rich media content such as image, audio, and video. For images, iOS displays the big images when the user uses Force Touch for interaction and thumbnails in other scenarios (regular image formats and GIF are supported).<br>1. Only images in JPEG, PNG, and GIF formats are supported.<br>2. The size of an image must be kept below 10 MB.<br>3. Only audio files in AIFF, WAV, MP3, and MP4 formats are supported.<br>4. The size of an audio file must be kept below 5 MB<br>5. Only videos in MPEG, MPEG2 Video, MPEG4, and AVI formats are supported<br>6. The rich media link can only use HTTPS. |
| Procedure | 1.Create a push task in the console or through the relevant API.<br>2. Enable rich media and enter the rich media file address. |
| Expected Result | The application can receive the rich media message. |


###  Offline message retaining

| Tested Feature | Offline message retaining |
| --- | --- |
| Test Objective | To verify that messages can be retained offline. |
| Test Environment |  Network environment: Wi-Fi or 4G<br>Terminal: Android devices from mainstream vendors |
| Prerequisites | The Tencent Push Notification Service SDK has been integrated, and device registration has been successfully completed. |
| Procedure | 1. Make the Tencent Push Notification Service application run in the background and end all application processes. <br>2. Push multiple messages. |
| Expected Result | When the application runs in the background, the tested devices cannot receive the messages. When the application is started again, the tested devices receive the messages, and the messages are displayed in the push order. |
| Remarks | This feature can be tested only through the Tencent Push Notification Service channel. Offline messages can be retained for up to 72 hours, and the latest three messages can be retained. If you need to retain more messages, please contact the customer service.  |



### Message reminder (custom ringtone)

| Tested Feature | Message reminder (custom ringtone) |
| --- | --- |
| Test Objective | To verify that you can set a custom ringtone. |
| Test Environment |  Network environment: Wi-Fi or 4G<br>Device: one or more mainstream Android or iOS devices, as applicable |
| Prerequisites | The Tencent Push Notification Service SDK has been integrated, and device registration has been successfully completed. |
| Procedure | 1. In the console, create a push task and select a custom ringtone in **Advanced Settings**.<br>2. Push a message. |
| Expected Result | The message reminder is the custom ringtone. |
| Remarks | Android supports customizing a ringtone, vibration, and notification LED (note: only the Tencent Push Notification Service channel supports this feature).<br>iOS supports customizing a ringtone. |

### iOS badge setting

| Tested Feature | iOS badge setting |
| --- | --- |
| Test Objective | To verify that you can set an iOS badge. |
| Test Environment | Network environment: Wi-Fi or 4G<br>Terminal: iOS device |
| Prerequisites | You have completed configurations as instructed in the development documentation at the official website for the "automatically increasing the badge number by 1" feature. |
| Procedure | 1. Create a push task in the console and set **Badge Number** to **Unchanged**, **Set to**, or **Auto increased by 1**.<br>2. Push a message.<br>3. Receive the message and check the badge number. |
| Expected Result | The badge display meets the settings. |
| Remarks | [Implementation method of the iOS badge API](https://www.tencentcloud.com/document/product/1024/30727#.E8.A7.92.E6.A0.87.E5.8A.9F.E8.83.BD) |

### Push redirection

| Tested Feature | Redirect push to a specified page |
| --- | --- |
| Test Objective | To verify that redirection works properly after a message is clicked on the notification bar. |
| Test Environment | Network environment: Wi-Fi or 4G<br>Terminal: Android devices from mainstream vendors |
| Prerequisites |  You have completed custom redirection configuration on the client as instructed in [here](https://www.tencentcloud.com/document/product/1024/38354). |
| Procedure | 1. Create a push task in the console. Expand the **Advanced Settings** area.<br>2. Set **Click to Open** to **Application**, **Custom Intent(Recommended)**, **URL**, or **In-App Activity**. <br>3. Push a message.<br>4. Click the message on the notification bar and check whether the system redirects to the specified page as expected. |
| Expected Result | The system redirects to the page as expected after the message is clicked in the notification bar. |
| Remarks | Vendor channels only support clicking to open an app or custom item (intent), while the Tencent Push Notification Service channel supports all click actions. <br>For more information on iOS push redirection, please see [here](https://www.tencentcloud.com/document/product/1024/38354). |





