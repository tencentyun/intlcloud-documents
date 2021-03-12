## Description
TPNS provides multiple push methods. You can test message pushes in different scenarios as instructed in this document. If you don't have enough testing devices, you can use the [Cloud Phone](https://wetest.qq.com/) service provided by WeTest.

## Testing Push Features

### Push to one device

| Test target | Push to one device |
| --- | --- |
| Test purpose | This test checks whether a message can be received during message push by device token |
| Test environment | Network environment: Wi-Fi or 4G<br>Device: one or more mainstream Android devices or iOS devices, as applicable |
| Prerequisites | The SDK has been integrated and device registration has been successfully completed |
| Test steps | 1. Get the token of the mobile phone to be tested<br>2. Call the relevant API or select a token as the push target in the console to push a message |
| Expected result | The phone can receive the message |

### Push to all devices (broadcasting)

| Test target | Push to all devices |
| --- | --- |
| Test purpose | This test checks whether a message can be pushed to all devices |
| Test environment | Network environment: Wi-Fi or 4G<br>Device: one or more mainstream Android devices or iOS devices, as applicable |
| Prerequisites | The SDK has been integrated and device registration has been successfully completed |
| Test steps | Call the relevant API or select all devices as the push target in the console to push a message to all devices |
| Expected result | All devices can receive the message |

### Scheduled push

| Test target | Scheduled push |
| --- | --- |
| Test purpose | This test checks whether a message can be pushed at a specified time point |
| Test environment | Network environment: Wi-Fi or 4G<br>Device: one or more mainstream Android devices or iOS devices, as applicable |
| Prerequisites | The SDK has been integrated and device registration has been successfully completed |
| Test steps | 1. Set the push time through the relevant API or in the console<br>2. Select all devices or a tag as the push target |
| Expected result | The phones can receive the message at the specified point in time |
| Remarks | Only full push and tag push support scheduled push |

### Loop push

| Test target | Loop push |
| --- | --- |
| Test purpose | This test checks whether a message can be received when the customized looping conditions (loop push date and loop type) are met |
| Test environment | Network environment: Wi-Fi or 4G<br>Device: one or more mainstream Android devices or iOS devices, as applicable |
| Prerequisites | The SDK has been integrated and device registration has been successfully completed |
| Test steps | 1. Set the loop push time and recurrence type through the relevant API or in the console<br>2. Select all devices or a tag as the push target |
| Expected result | The phones can receive the message when the set recurrence conditions are met |
| Remarks | Only full push and tag push support this feature |

### Push to one account

| Test target | Push to one account |
| --- | --- |
| Test purpose | This test checks whether a message can be received during message push by account |
| Test environment | Network environment: Wi-Fi or 4G<br>Device: one or more mainstream Android devices or iOS devices, as applicable |
| Prerequisites | You have called the account binding API for account binding |
| Test steps | 1. Call the SDK API on the mobile app to bind the account<br>2. After the specified account has been bound to the device token, push a message to this account through the relevant API or in the console |
| Expected result | The device bound to the specified account can receive the message |
| Remarks | [Binding Account on Android](https://intl.cloud.tencent.com/document/product/1024/30715)<br>[Binding Account on iOS](https://intl.cloud.tencent.com/document/product/1024/30727) |

### Push to multiple accounts

| Test target | Push to multiple accounts |
| --- | --- |
| Test purpose | This test checks whether a message can be pushed to multiple accounts in batches through the account list |
| Test environment | Network environment: Wi-Fi or 4G<br>Device: one or more mainstream Android devices or iOS devices, as applicable |
| Prerequisites | You have called the account binding API for account binding |
| Test steps | Push a message to multiple accounts in batches through the relevant API or in the console |
| Expected result | The device bound to the specified accounts can receive the message |
| Remarks | [Binding Account on Android](https://intl.cloud.tencent.com/document/product/1024/30715)<br>[Binding Account on iOS](https://intl.cloud.tencent.com/document/product/1024/30727) |

### Push through vendor channels

| Test target | Push through multiple vendor channels |
| --- | --- |
| Test purpose | This test checks whether a message can be received after an application process is killed on a device |
| Test environment | Mi, Huawei, Meizu, OPPO, and Vivo phones are required. For FCM, Google Play must be installed |
| Prerequisites | 1. You have signed up with these vendors' push platforms and created the required apps<br>2. You have configured vendor channels on the [Configuration Management](https://console.cloud.tencent.com/tpns/app-config) page<br>3. You have integrated the SDK according to the vendors' integration methods on their official websites<br>4. You have enabled the vendor channels in the SDK |
| Test steps | 1. Install the app integrated with the vendor channel on a phone<br>2. Sign up with the vendor channel and get the vendor token <br>3. Push a message to the phone through the relevant API or in the console |
| Expected result | The message can be received after you exit the app, kill all app processes on the background, and push a message to one or all devices |
| Remarks | For Huawei phones, you need to use signed packages. For more information, please see [Connecting to Huawei Push Channel](https://intl.cloud.tencent.com/document/product/1024/30716) |


### Tag push
You can push messages to devices of the same tag in the console or through the relevant API, which supports "AND" and "OR" relationships between multiple tags.

| Test target | Tag push |
| --- | --- |
| Test purpose | You can set tags for different user groups and then send mass notifications based on tag name |
| Test environment | Network environment: Wi-Fi or 4G<br>Device: one or more mainstream Android devices or iOS devices, as applicable |
| Prerequisites | The SDK has been integrated and you have successfully set custom tags |
| Test steps | 1. Select a custom or preset tag when creating a push, set "AND" or "OR" relationship, and start the push<br>2. Call the relevant API to select one or more custom tags, set "AND" or "OR" relationship, and start the push |
| Expected result | The user groups with the set tag can receive the message |
| Remarks | [API for Setting Custom Tag on Android](https://intl.cloud.tencent.com/document/product/1024/30715)<br>[API for Setting Custom Tag on iOS](https://intl.cloud.tencent.com/document/product/1024/30727) |

### In-app message push
This refers to the message directly passed through to the Android device, which will not be actively displayed in the notification bar and will be handled by the app once received.

| Test target | In-app message push |
| --- | --- |
| Test purpose | This test checks whether a message can be directly passed through |
| Test environment | Network environment: Wi-Fi or 4G<br>Device: one or more mainstream Android devices or iOS devices, as applicable |
| Prerequisites | The SDK has been integrated and the device has successfully registered |
| Test steps | Push an in-app message in the console or through the relevant API |
| Expected result | The app can receive the in-app message |

### Rich media push
You can push multimedia (rich media) messages containing images, audios, videos, etc. to clients.

| Test target | Rich media push |
| --- | --- |
| Test purpose | This test checks whether a rich media message such as image can be pushed |
| Test environment | Network environment: Wi-Fi or 4G<br>Device: one or more mainstream Android devices or iOS devices, as applicable |
| Prerequisites | **Android:** messages with rich media will be delivered through the TPNS channel. Images in native Android systems are available in original image and thumbnail, whose display effects vary by model and ROM.<br>1. Android supports static images, audios, and videos as rich media content<br>2. The image resolution should be 430\*2303, and the rich media link can only use HTTPS<br>3. For audio/video rich media, you need to create an .xml file after integrating the SDK. For more information, please see [Instructions for Audio/Video Rich Media](https://intl.cloud.tencent.com/document/product/1024/30713) <br>**iOS:** the system supports rich media content such as image, audio, and video. For images, iOS displays the original image when the user uses Force Touch for interaction and thumbnail in other scenarios (regular image formats and GIF are supported).<br>1. Only images in JPEG, PNG, and GIF formats are supported<br>2. The size of an image must be kept below 10 MB<br>3. Only audios in AIFF, WAV, MP3, and MP4 formats are supported<br>4. The size of an audio file must be kept below 5 MB<br>5. Only videos in MPEG, MPEG2 Video, MPEG4, and AVI formats are supported<br>6. The rich media link can only use HTTPS |
| Test steps | 1. Create a push in the console or through the relevant API<br>2. Enable rich media and enter the rich media file address |
| Expected result | The app can receive the rich media message such as image, audio, or video |


### Offline message storage

| Test target | Offline message storage|
| --- | --- |
| Test purpose | This test checks whether an offline message can be stored |
| Test environment | Network environment: Wi-Fi or 4G<br>Device: one or more mainstream Android device, as applicable |
| Prerequisites | The SDK has been integrated and device registration has been successfully completed |
| Test steps | 1. Exit the app and kill all app processes on the background<br>2. Push multiple messages |
| Expected result | The messages cannot be received after the app is closed and can be received when the app is opened again and displayed in the push order |
| Remarks | This feature can be tested only through the TPNS channel. Up to 3 latest offline messages can be stored and retained for at most 72 hours. If you need to store more offline messages, please submit a ticket for assistance |

## Testing Other Features
### Message alert (custom ringtone)

| Test target | Custom ringtone |
| --- | --- |
| Test purpose | This test checks whether a custom ringtone can be set |
| Test environment | Network environment: Wi-Fi or 4G<br>Device: one or more mainstream Android devices or iOS devices, as applicable |
| Prerequisites | The SDK has been integrated and device registration has been successfully completed |
| Test steps | 1. Create a push in the console and select "Custom Ringtone" in Advanced Settings<br>2. Push a message |
| Expected result | The custom ringtone is used for the message alert |
| Remarks | Android supports customizing ringtone, vibration, and notification LED. (Note: only the TPNS channel rather than vendor channels supports this feature.)<br>iOS supports customizing ringtone |

### iOS badge settings

| Test target | iOS badge |
| --- | --- |
| Test purpose | This test checks whether an iOS badge can be set as expected |
| Test environment | Network environment: Wi-Fi or 4G<br>Device: one or more iOS devices, as applicable |
| Prerequisites | You have completed configurations as instructed in the development documentation at the official website for the "automatically increasing badge number by 1" feature |
| Test steps | 1. Create a push in the console and select "Unchanged", "Set to", or "Increase by 1" as "Badge Number"<br>2. Push a message<br>3. Receive the message and check the badge |
| Expected result | The badge display meets the settings |
| Remarks | [Implementation Method of the iOS Badge API](https://intl.cloud.tencent.com/document/product/1024/30727) |

### Push redirect

| Test target | Push redirect to the specified page |
| --- | --- |
| Test purpose | This test checks whether redirect works properly after a message is clicked on the notification bar |
| Test environment | Network environment: Wi-Fi or 4G<br>Device: one or more mainstream Android device, as applicable |
| Prerequisites | You have completed custom redirect configurations on the client as instructed in [Configuration Guide](https://intl.cloud.tencent.com/document/product/1024/32624) for the custom redirect feature |
| Test steps | 1. Create a push in the console and open Advanced Settings<br>2. Select "App", "In-App Page", "URL", or "Custom" as "Click to Open"<br>3. Push a message<br>4. Click the message on the notification bar and check whether the system redirects to the page as expected |
| Expected result | The system redirects to the page as expected after the message is clicked in the notification bar |
| Remarks | Vendor channels only support clicking to open an app or custom item (intent), while the TPNS channel supports all click actions <br>For more information on iOS push redirect, please see [Client Redirect Based on Message Content](https://intl.cloud.tencent.com/document/product/1024/38354) |
