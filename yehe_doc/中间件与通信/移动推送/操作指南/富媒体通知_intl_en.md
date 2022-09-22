## Overview

Rich media push allows you to push rich media contents such as image, audio, and video in addition to text, which can effectively increase the notification click rate. You can use this feature to push a wider variety of contents such as news, coupons, and event information, satisfying your personalized push needs.

## Application Scope

Currently, TPNS rich media push supports the following types of rich media contents:

- Android: image and audio
- iOS: image, audio, and video
>?The TPNS channel for iOS supports rich media push by default. For the APNs channel, applications need to integrate with the [notification service extension plugin](https://intl.cloud.tencent.com/document/product/1024/30730).

The supported types of rich media and use requirements for each push channel are as follows:

| Push Channel | Supported Type | Use Requirements |
| -------- | ----------------- | ------------------------------------------------------------ |
| Huawei | Thumbnail | <ul  style="margin: 0;"><li>Only HTTPS URLs are supported.</li><li>Format requirements:<ul  style="margin: 0;"><li>`PNG`, `JPG`, and `JPEG`</li><li>120 x 120 px. The image will be automatically resized if its width or height exceeds 120 px.</li><li>Less than 200 KB</li></ul></li></ul>|
| Mi | Large image | <ul  style="margin: 0;"><li>Only HTTPS URLs are supported.</li><li>Format requirements:<ul  style="margin: 0;"><li>`PNG`, `JPG`, and `JPEG`</li><li>Fixed at 876 x 324 px</li><li>Less than 1 MB</li></ul></li></ul>Note: to use the large image notification feature in the Mi channel, you need to first call the image upload API of Mi to upload the image file, get the image address `pic_url` specified by Mi, and enter it in the corresponding TPNS push parameter `xg_media_resources`. For more information, see the large image upload API description in [here](https://dev.mi.com/console/doc/detail?pId=1163#_10_0).|
| TPNS     | Large image, thumbnail, and audio | <ul  style="margin: 0;"><li>Android platform:<ul  style="margin: 0;"><li>Only HTTPS URLs are supported.</li><li>Image format requirements:<ul  style="margin: 0;"><li>`JPEG`, `JPG`, and `PNG`</li><li>The height of a large image cannot exceed 324 px and the width is adaptive.</li><li>The size of a thumbnail should be 120 x 120 px. If its height or width exceeds 120 px, it will be cropped into a square.</li></ul></li><li>Audio file format requirements: an audio file cannot exceed 5 MB.</li></ul></li><li>iOS platform: the requirements are the same as that of the APNs channel.</li></ul> |
| APNs     | Thumbnail and audio/video | <ul  style="margin: 0;"><li>Only HTTPS URLs are supported.</li><li>Image format requirements:<ul  style="margin: 0;"><li>`JPEG`, `PNG`, and `GIF` formats</li><li>Less than 10 MB</li></ul></li><li>Audio/Video file format requirements:<ul  style="margin: 0;"><li>Video encoding formats: `MPEG`, `MPEG-2 Video`, `MPEG-4`, and `AVI`</li><li>Audio file extensions: `AIFF`, `WAV`, and `CAF`</li><li>Audio encoding formats: `Linear PCM`, `MA4 (IMA/ADPCM)`, `alaw`, and `μLaw`</li><li>An audio/video file should be less than 5 MB.</li><li>An audio file should be less than 30s long.</li></ul></li></ul>Note: image and audio/video cannot be enabled at the same time. |

## Operation Directions

### Console

1. Log in to the [TPNS console](https://console.cloud.tencent.com/tpns). Go to **Message Management** > **Task List**.
2. Click **Create Push** > **Advanced Settings**.
	 ![](https://main.qcloudimg.com/raw/cf75c4752a715bc241cee8a0273f10aa.png)
3. Enable **Notification Image** or **Notification Audio/Video**, and enter the rich media message URL. The detailed configuration instructions are as follows:
 - When you enable **Notification Image**:
    Android:
> ?
> - Thumbnail:
>   The URL must be in HTTPS format.
>   The thumbnail can be displayed in pushes delivered through the TPNS and Huawei channels.
>   Format requirements: `PNG`, `JPG`, or `JPEG`; 120 × 120 px; less than 200 KB
> - Large image:
>   The URL must be in HTTPS format.
>   The large image can be displayed in pushes delivered through the TPNS and Mi channels.
>   Format requirements: `PNG`, `JPG`, or `JPEG`; 876 x 324 px; less than 1 MB
>
 ![](https://main.qcloudimg.com/raw/5314797a28893a0ced7d2bc0a32811bd.png)
 iOS:
 >? After the image URL is entered, the image will be displayed in the notification. Format requirements:
>
> - The file size cannot exceed 10 MB.
> - The file must be in `PNG`, `JPG`, `JPEG`, or `GIF` format.
> - The URL must be in HTTPS format.
>
 ![](https://main.qcloudimg.com/raw/ea40f906c6fc5d322f92510b30883c49.png)
 - When you enable **Notification Audio** or **Notification Audio/Video**:
    Android:
> ?After the audio URL is entered, notifications delivered through the TPNS channel can contain audio.
> - The audio file size cannot exceed 5 MB.
> - The URL must be in HTTPS format.
>
  ![](https://main.qcloudimg.com/raw/8433c6eae3503c9c58878f05089c5ea5.png)
  iOS:
> ?After the audio/video URL is entered, notifications can contain audio or video and be played back through Apple's native component.
> - The audio/video file size cannot exceed 5 MB.
> - The file must be in `MPEG`, `MPEG-2 Video`, `MPEG-4`, or `AVI` format.
> - The URL must be in HTTPS format.
>
  ![](https://main.qcloudimg.com/raw/81bcf3c89c21ba42c279e060af081c07.png)



### RESTful API

To send a rich media message via an API call, you can set the following parameters in the Android or iOS message body in the `Push` API:


<table>
<thead>
<tr>
<th>Platform</th>
<th>Parameter</th>
<th>Notes</th>
</tr>
</thead>
<tbody><tr>
<td>Android</td>
<td nowrap="nowrap"><li>Thumbnail: <code>icon_res</code>, <code>icon_type</code> </li><li>Large image: <code>xg_media_resources</code> </li><li>Audio: <code>xg_media_audio_resources</code></li></td>
<td><li>Thumbnails are supported only for the TPNS and Huawei channels.</li><li>Large images are supported only for the TPNS and Mi channels.</li><li>Audios are supported only for the TPNS channel.</li></td>
</tr>
<tr>
<td>iOS</td>
<td nowrap="nowrap"><li>Image and audio/video: <code>xg_media_resources</code></li></td>
<td>Notification Image and Notification Audio/Video cannot be enabled at the same time.</td>
</tr>
</tbody></table>


For more information, see the **Required Parameters** section in [Push API](https://intl.cloud.tencent.com/document/product/1024/33764).


#### Below is a sample push on Android:

```
{
    "audience_type": "token",
    "token_list": [
        "05da87c0ae******2dfa9e08d884aada5bb2"
    ],
    "message_type": "notify",
    "multi_pkg":true,
    "message": {
        "Title": "Push title",
        "content": "Push content",
        "xg_media_resources": "xxx1" , // Enter the URL of the rich media element, such as `https://www.xx.com/img/bd_logo1.png?qua=high`.
        "xg_media_audio_resources":"xxx", // Enter the URL of the audio, such as `https://sc1.111ttt.cn/2018/1/03/13/396131227447.mp3`. 
        "android": {
       "icon_type": 1,
        "icon_res": "xxx", // Enter the URL of the thumbnail.
             "custom_content":"{\"key\":\"value\"}"
        }                        
    }
}
```

## FAQs

#### The Meizu, OPPO, and vivo channels do not support rich media. How do I deliver notifications to all devices?

Notifications delivered through the TPNS, Huawei, Mi, and FCM channels contain images, while those delivered through the Meizu, OPPO, and vivo channels are in plain text format without images by default.

#### How can I include an image in a push message?

Whether you call an API or use the console to deliver a message, you need to generate a URL for the image to include it in the message.

#### What is the policy for delivering audios on Android?

Audio pushes delivered through the TPNS channel can display the audios normally, while those delivered through other channels will be in plain text format without audios by default.

#### Can I enable both Notification Image and Notification Audio/Video for iOS?

No. You can only enable either of them.
