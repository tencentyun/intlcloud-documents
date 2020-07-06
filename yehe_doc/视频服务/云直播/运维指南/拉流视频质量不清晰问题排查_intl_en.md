The video of the host is captured by the local camera, encoded and pushed by the SDK for client, and then distributed to the viewers by Tencent Cloud CDN. If you provide a multi-bitrate address, the video stream will also be re-encoded in Tencent Cloud. The quality of output video mainly depends on the quality of input video captured by camera, and the frame rate, keyframe interval, resolution, and bitrate configured for encoding. Considering the influence on video delay and bitrate, we recommend setting the keyframe interval to 2-3 seconds.

This document describes how to troubleshoot the problem that the video pulled to the following **two** playback addresses is pixelated and how to optimize the video quality.

## Playback Address of Input Video Stream
If the video pulled to the **playback address of the input video stream** (neither watermarked nor mixed) is pixelated, we recommend locating the problem at the push end:
1. Troubleshoot problems of the camera. For example, check whether there is dust, or whether the camera has focused or captured properly.
2. Check whether the frame rate and bitrate of the pushed stream are as expected.
<table>
<thead><tr><th>Resolution</th><th>Frame Rate</th><th>Expected Bitrate</th></tr></thead>
<tbody><tr>
<td>640 × 368</td>
<td>15 fps</td>
<td>800 Kbps</td>
</tr><tr>
<td>960 × 544</td>
<td>15 fps</td>
<td>1,000 Kbps</td>
</tr><tr>
<td>1280 × 720</td>
<td>15 fps</td>
<td>1,500 Kbps</td>
</tr><tr>
<td>1920 × 1080</td>
<td>15 fps</td>
<td>2,500 Kbps</td>
</tr>
</tbody></table>

#### Optimization
- If you use a third-party SDK, please refer to the above recommended bitrates to adjust and control the video quality, or contact the third-party SDK manufacturer to solve the problem.
- If the video in the preview window has a good quality but the pulled video is pixelated, this may be because the quality of the video in the preview window is inconsistent with that of the encoded and pushed one. Please refer to the above recommended settings to adjust the quality of the encoded and pushed video.

 

## Playback Address of Video Stream at Low Bitrate and Resolution
If the video pulled to the **playback address of a low-bitrate and low-resolution video stream** is pixelated, you need check the video quality of the playback address of the input video stream. If the input video has a good quality, so does the video pushed by the client. In this case, we recommend that you modify the transcoding parameters in Tencent Cloud. For example, you can increase the output bitrate to a recommended value in the transcoding template.
<table>
<thead><tr><th>Resolution</th><th>Frame Rate</th><th>Expected Bitrate</th></tr></thead>
<tbody><tr>
<td>640 × 368</td>
<td>15 fps</td>
<td>800 Kbps</td>
</tr><tr>
<td>960 × 544</td>
<td>15 fps</td>
<td>1,000 Kbps</td>
</tr><tr>
<td>1280 × 720</td>
<td>15 fps</td>
<td>1,500 Kbps</td>
</tr><tr>
<td>1920 × 1080</td>
<td>15 fps</td>
<td>2,500 Kbps</td>
</tr>
</tbody></table>

For example, if the video resolution is 640 × 368 and the template frame rate is 30 fps, we recommend increasing the output bitrate to 1.5 times of its original value, so the recommended bitrate is calculated by 800 Kbps × 1.5=1,200 Kbps.


>! If the problem persists after all the above steps are completed, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=39&source=0&data_title=%E4%BA%91%E7%9B%B4%E6%92%AD%20%20CSS&step=1).



