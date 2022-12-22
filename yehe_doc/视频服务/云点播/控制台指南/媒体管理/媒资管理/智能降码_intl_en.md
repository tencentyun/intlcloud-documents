## Overview
You can configure smart bitrate reduction policies in the VOD console to automatically reduce the bitrate of media files that meet the specified conditions.
>! 
>- Smart bitrate reduction works on a file ID level. If a media file meets the conditions of a bitrate reduction policy, the policy will be applied to all its transcoding and adaptive bitrate outputs in HLS format (which have the same file ID).
>- Smart bitrate reduction (TSC transcoding) does not work on files whose bitrates have already been reduced.
>- Bitrate reduction policies are not applied to transcoding and adaptive bitrate outputs generated before September 19, 2022.

## Configuring a smart bitrate reduction policy
Log in to the [VOD console](https://console.cloud.tencent.com/vod/overview) and select **Media Assets > Smart Bitrate Reduction** on the left sidebar.

![](https://qcloudimg.tencent-cloud.cn/raw/1da0dfdc7cbc585ac5649065b961639f.jpg)

Click **Create policy**.

Enter a **policy name** and **specify the conditions**:

* **Playback count**: Specify the playback count threshold (how many times a file is played within a certain time period).
* **Video label**: Specify the video labels. The policy will only be applied to videos that have the specified labels.


![](https://qcloudimg.tencent-cloud.cn/raw/3aee1a4981e5d6e7ed24204c88b10807.jpg)

Return to the **Smart Bitrate Reduction** page and enable the policy.

![](https://qcloudimg.tencent-cloud.cn/raw/32c4262abd02280c9ce998717dc4dd3c.jpg)

After the policy is enabled, VOD will execute bitrate reduction tasks automatically on files that meet the conditions of the policy.
The [Task Flow Status Change](https://www.tencentcloud.com/document/product/266/33953) callback notifies you about the progress of bitrate reduction tasks.
