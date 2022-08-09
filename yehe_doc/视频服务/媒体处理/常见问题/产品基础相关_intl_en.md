## Concepts

[](id:b1)
### What is MPS?
Media Processing Service (MPS) is a cloud-based multimedia transcoding and processing service capable of handling vast amounts of data. You can use it to transcode your videos stored in the cloud to make them suitable for OTT services or playback on PC and mobile devices. You can also transcode videos to different bitrates and resolutions for different platforms. Other services MPS offers include watermarking, video screenshot, smart thumbnail generation, smart editing, etc.

[](id:b2)
### What is video bitrate?
Video bitrate is the number of data bits transferred per unit time. It is often measured in Kbps, or kilobits per second.
Bitrate (Kbps) = File size (KB) × 8 ÷ Transfer time (s)

[](id:b3)
### What is TESHD in MPS?
TESHD is a process where videos are processed to reduce bandwidth usage while retaining or improving video quality. It allows you to deliver higher-definition videos to your users with less bandwidth usage.

[](id:b4)
### Does MPS use hardware or software for decoding?
MPS offers video processing services such as on-cloud transcoding, watermarking, thumbnail generation, and smart editing. It does not offer decoding services.

[](id:b5)
### What is the basic process involved in using MPS?
The process includes configuring workflows, triggering transcoding tasks, executing transcoding tasks, and sending event notifications. The figure below shows how a [workflow](https://intl.cloud.tencent.com/document/product/1041/33475) works.

<img src="https://qcloudimg.tencent-cloud.cn/raw/f2d33c2685ad9855b10bd1d808e5105b.png" width=600px>


## Features
[](id:f1)
### Does MPS provide test accounts?
No, it doesn’t.

[](id:f2)
### What screenshot taking modes does MPS support?
MPS supports time point screenshot (single screenshots), sampled screenshot (multiple screenshots), and image sprite screenshot. For details, see “Screenshot Template” in [Template Settings](https://intl.cloud.tencent.com/document/product/1041/33486).

[](id:f3)
### Does MPS support regular expressions?
No, it doesn’t.

[](id:f4)
### Does MPS support multi-task processing?
Yes, it does.

[](id:f5)

### Will multi-task processing slow down the overall progress?
No, it won’t.

[](id:f6)
### Does MPS support video splicing?
Yes, it does. You cannot splice videos via the console but can call an API to splice videos. For detailed directions, see [EditMedia](https://intl.cloud.tencent.com/document/product/1041/37460).

[](id:f7)
### Does MPS support video compression?
No, it doesn’t.

[](id:f8)
### Does MPS support video rotation?
No, it doesn’t.
MPS allows you to transcode your videos stored in the cloud to make them suitable for OTT services or playback on PC or mobile devices. It also supports watermarking and screenshot taking.

[](id:f9)
### Can MPS convert images to videos?
No, it can’t.

[](id:f10)
### Can I increase the number of tags for AI analysis?
The top 5 tags are displayed and cannot be adjusted currently. If you want to display more, try frame tags.

[](id:f11)
### Can MPS convert the audio in video files to text?
MPS can perform content recognition on videos and the results include text converted from audio.

[](id:f12)

### Does smart thumbnail generation support animated images?
No, it doesn’t.
Smart thumbnail generation is selecting one or several screenshots from a video as the thumbnail based on content analysis results. It does not support animated thumbnails. Currently, you can only generate animated thumbnails by configuring templates. For detailed directions, see [Animated Image Generating](https://intl.cloud.tencent.com/document/product/266/33941).

[](id:f13)
### Can a workflow output to multiple directories?
MPS does not support outputting to multiple directories, but you can output to multiple buckets. You can also configure multiple workflows to output to different directories.
![](https://qcloudimg.tencent-cloud.cn/raw/684c56181bcd670c616ab1b1f252281a.png)

[](id:f14)
### Does MPS support video segmentation?
No, it doesn’t.

[](id:f15)
### Does MPS support HDR transcoding?
It supports converting H.264 HLG videos into HDR format. If you have other needs, please contact us by [submitting a ticket](https://console.cloud.tencent.com/workorder/category).
