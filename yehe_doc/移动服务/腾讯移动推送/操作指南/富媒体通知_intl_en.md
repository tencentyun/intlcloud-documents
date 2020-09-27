## Operation Scenarios

Rich media push allows you to push rich media contents such as image, audio, and video in addition to text, which can effectively increase the notification click rate. You can use this feature to push a wider variety of contents such as news, coupons, and event information, satisfying your personalized push needs.

## Scope of Application

Currently, the rich media push feature of TPNS supports the following types of rich media contents:

- Android: image and audio.
- iOS: image, audio, and video (the application needs to integrate with the [notification service extension plugin](https://intl.cloud.tencent.com/document/product/1024/30730)).

The supported types of rich media and use requirements for each push channel are as detailed below:

| Push Channel | Supported Type          | Use Requirements                                                     |
| -------- | ----------------- | ------------------------------------------------------------ |
| Huawei | Thumbnail | <li>Only HTTPS URLs are supported<li>Format requirements:<br>1. `PNG/JPG/JPEG` format<br>2. 120 x120 px in dimensions. If this limit is exceeded, the image will be automatically adjusted.<br>3. Below 200 KB in size |
| Mi     | Big image              | <li>Only HTTPS URLs are supported <li>Format requirements: <br>1. `PNG`, `JPG`, or `JPEG` format <br>2. Fixed at 876x324 px in dimensions <br>3. Below 1 MB in size <li> Note: to use the big image notification feature of the Mi channel, you need to first call the image upload API of Mi to upload the image file, get the image address `pic_url` specified by Mi, and enter it in the corresponding TPNS push parameter `xg_media_resources`. For more information, please see the big image upload API description in [Mi Push Rich Media Message](https://dev.mi.com/console/doc/detail?pId=1163#_10_0) |
| TPNS     | Big image + thumbnail + audio | <li>Only HTTPS URLs are supported <li> Image format requirements: <br>1. `JPEG`, `JPG`, or `PNG` format <br>2. The image height cannot exceed 256 px, and the width is adaptive <li>Audio/Video file format requirements: <br>1. The audio file cannot exceed 5 MB in size |
| APNs     | Thumbnail + audio/video     | <li>Only HTTPS URLs are supported <li>Image format requirements: <br>1. `JPEG`, `PNG`, or `GIF` format <br>2. Below 10 MB in size <li>Audio/Video file format requirements: <br>1. `MPEG`, `MPEG-2 Video`, `MPEG-4`, or `AVI` format <br>2. Below 5 MB in size <li>Note: image and audio/video in notification cannot be enabled at the same time |

## Directions

### Console

1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns) and select **Push Management** > **Push Task** on the left sidebar to enter the push task page.
2. Click **Create Push** > **Advanced Settings**.
	 ![](https://main.qcloudimg.com/raw/cf75c4752a715bc241cee8a0273f10aa.png)
3. Enable **Notification Image** or **Notification Audio/Video** and enter the rich media message URL. The specific configuration is as detailed below:
 - **If **Notification Image** is enabled:**
    Android:
> ?
> - Thumbnail:
>   The URL must be in HTTPS format.
>   The thumbnail can be displayed for pushes delivered through the TPNS and Huawei channels.
>   Format requirements: image in `PNG`, `JPG`, or `JPEG` format at dimensions of 120×120 px and below 200 KB in size.
> - Big image:
>   The URL must be in HTTPS format.
>   The big image can be displayed for pushes delivered through the TPNS and Mi channels.
>   Format requirements: image in `PNG`, `JPG`, or `JPEG` format at fixed dimensions of 876x324 px and below 1 MB in size.

 ![](https://main.qcloudimg.com/raw/5314797a28893a0ced7d2bc0a32811bd.png)
 iOS:

 >? After the image URL is entered, the image will be displayed in the notification. Format requirements:
>
> - The file size cannot exceed 10 MB.
> - The file must be in `PNG`, `JPG`, `JPEG`, or `GIF` format.
> - The URL must be in HTTPS format.

 ![](https://main.qcloudimg.com/raw/ea40f906c6fc5d322f92510b30883c49.png)
 - **If **Notification Audio** or **Notification Audio/Video** is enabled:**
    Android:
> ?After the audio URL is entered, notifications delivered through the TPNS channel can contain audio.
> - The audio file size cannot exceed 5 MB.
> - The URL must be in HTTPS format.

  ![](https://main.qcloudimg.com/raw/8433c6eae3503c9c58878f05089c5ea5.png)
  iOS:

> ?After the audio/video URL is entered, notifications can contain audio or video and be played back through Apple's native component.
> - The audio/video file size cannot exceed 5 MB.
> - The file must be in `MPEG`, `MPEG-2 Video`, `MPEG-4`, or `AVI` format.
> - The URL must be in HTTPS format.

  ![](https://main.qcloudimg.com/raw/81bcf3c89c21ba42c279e060af081c07.png)



### RESTful API

If you want to deliver rich media messages when calling the API for push, you can set the following parameters in the Android or iOS message body in the `Push` API:


<table>
<thead>
<tr>
<th>Platform</th>
<th>Parameter</th>
<th>Remarks</th>
</tr>
</thead>
<tbody><tr>
<td>Android</td>
<td nowrap="nowrap"><li>Thumbnail: <code>icon_res</code>, <code>icon_type</code> </li><li>Big image: <code>xg_media_resources</code> </li><li>Audio: <code>xg_media_audio_resources</code></li></td>
<td><li> Thumbnail is supported only for the TPNS and Huawei channels </li><li>Big image is supported only for the TPNS and Mi channels </li><li>Audio is supported only for the TPNS channel</li></td>
</tr>
<tr>
<td>iOS</td>
<td nowrap="nowrap"><li>Image and audio/video: <code>xg_media_resources</code></li></td>
<td>Notification image and notification audio/video cannot be enabled at the same time</td>
</tr>
</tbody></table>


For more information, please see the description of [required parameters for the Push API](https://intl.cloud.tencent.com/document/product/1024/33764).


#### Sample push on Android

```
{
    "audience_type": "token",
    "token_list": [
        "05da87c0ae******2dfa9e08d884aada5bb2"
    ],
    "message_type": "notify",
    "multi_pkg":true,
    "message": {
        "title": "Push title",
        "content": "Push content",
        "xg_media_resources": "xxx1" , // Enter the rich media element address, such as `https://www.xx.com/img/bd_logo1.png?qua=high`
        "xg_media_audio_resources":"xxx", // Enter the audio rich media element address, such as `https://sc1.111ttt.cn/2018/1/03/13/396131227447.mp3` 
        "android": {
       "icon_type": 1,
        "icon_res": "xxx", // Enter the image thumbnail element address
             "custom_content":"{\"key\":\"value\"}"
        }                        
    }
}
```

## FAQs

#### The Meizu, OPPO, and Vivo channels do not support rich media. How do I deliver a notification when pushing to all devices?

Notifications delivered through the TPNS, Huawei, Mi, and FCM channels can contain images, while those delivered through the Meizu, OPPO, and Vivo channels are in text format without images by default.

#### How can I include an image in a push message?

No matter whether you call an API or use the console to deliver a message, you should generate a URL for the image to include it in the message.

#### What is the delivery policy for audio rich media on Android?

Audio rich media pushes delivered through the TPNS channel can display the audio normally, while those delivered through other channels will be in text format without audio by default.

#### Can notification image and notification audio/video be enabled for rich media notification on iOS at the same time?

No. Only one of them can be enabled at a time.
