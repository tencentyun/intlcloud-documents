The greatest challenge faced by paid video platforms is that some users may download videos in various ways and share or sell them to other platforms without authorization. This severely damages the interests of copyright holders. Unauthorized video recording is the main form of video piracy. Pirates often use screen recording software to record the video, and may even use a camera to directly record their screen, which is hard to prevent.

One of the most effective ways to suppress unauthorized video recording is to track down pirates and combine other means to protect copyrighted content, deter piracy, and demand compensation. VOD's digital watermark feature guarantees a high security level at low costs and helps you easily trace unauthorized video recording.

## Shortcomings of Traditional Watermarks

Traditional countermeasures against unauthorized video recording are to add the viewer's user ID to the video image. There are mainly two methods: adding a **common image and text watermark** or adding a **player floating watermark**.

<table>
   <tr>
      <th width="0px" style="text-align:center">Common Image and Text Watermark</td>
      <th width="0px" style="text-align:center">Player Floating Watermark</td>
   </tr>
   <tr>
      <td><img src="https://qcloudimg.tencent-cloud.cn/raw/82766338aee9f4f9715427e337babd25.png" width=500><br>
         The image or text watermark is encoded into the video, and the content is the viewer's user ID.      
</td>
      <td><img src="https://qcloudimg.tencent-cloud.cn/raw/69dbaf292d144094854efca31e51d922.png" width=500><br>
			A watermark covering the video layer during playback in the player. It usually moves like a news ticker on the video image.</td>
   </tr>
</table>
These two types of watermarks have the following characteristics:

| Watermarking Method | Common Image and Text Watermark | Player Floating Watermark |
| -- | -- | -- |
| Security | High: The watermark is encoded to the video and cannot be removed. | Low: The watermark appears in the video player but is not encoded to the video. |
| Costs | High: Each unique user ID watermark needs to be transcoded and stored once. | Low: It is embedded in the player. |
| Robustness | Low: The watermark is in a fixed position and is easily clipped or obscured. | Low: The watermark is visible and can be obscured. |
| Visibility | Watermark is visible and can be a distration. | Watermark is visible and can be a distration. |


As shown above, these two types of traditional watermarks have several disadvantages.

## VOD Digital Watermark

VOD digital watermark can deliver a high security at low costs.

* Low costs: Only streams A and B need to be transcoded for a video. This means that it takes only the costs of transcoding and storing two streams to mark and track billions of viewers.
* High security: The watermark is encoded to the video image, so it cannot be removed even if the video data is obtained.
* High robustness: Resistant to various attacks, such as resampling, compression, dithering, cropping, scaling, rotation, filtering, etc.
* Invisibility: The watermark is invisible to human eyes, having no affect on video quality.

>!
>VOD digital watermark is currently in the public beta stage, and there are following suggestions for use:
>- Add a digital watermark to a video **longer than 30 minutes**.
>- The extraction of watermark in **movies, TV shows and variety shows** has a relatively better performance.
>- The extraction of watermark in **online education** videos is being optimized. It is recommended to test and integrate this feature after offical release.

## Directions

### Adding a digital watermark

Call the [ProcessMeida](https://intl.cloud.tencent.com/document/product/266/34125) API to initiate a task to add a digital watermark to a video. Select Transcoding or Adaptive Bitrate Streaming as the processing type:


#### Transcoding
* Select a transcoding template with the container format as HLS, such as `STD-H264-HLS-720P` (template ID 100230). Pass in the template ID to `MediaProcessTask.TranscodeTaskSet.TraceWatermark.Definition`.
* Pass in `ON` for `MediaProcessTask.TranscodeTaskSet.TraceWatermark.Switch` to enable digital watermark.

#### Adaptive Bitrate Streaming
* Select an adaptive bitrate streaming template with the container format as HLS, such as `Adaptive-HLS` (template ID 10). Pass in the template ID to `MediaProcessTask.AdaptiveDynamicStreamingTaskSet.TraceWatermark.Definition`.
* Pass in `ON` for `MediaProcessTask.AdaptiveDynamicStreamingTaskSet.TraceWatermark.Switch` to enable digital watermark.


#### Playing back the video

You need to associate a `uv`, which is a 6-digit hexadecimal integer, with all your paid users. The `uv` will be used as the proof for viewer traceability.

* If you use the [Player SDK](https://intl.cloud.tencent.com/document/product/266/33977) or [Player Adapter](https://intl.cloud.tencent.com/document/product/266/42095) of VOD, your business server needs to distribute a [player signature](https://intl.cloud.tencent.com/document/product/266/38099) for each playback request. You need to enter the viewer `uv` as the `uv` in [signature parameters](https://intl.cloud.tencent.com/document/product/266/38099#.E7.AD.BE.E5.90.8D.E5.8F.82.E6.95.B0).
* If you don't use the VOD Player SDK, you need to add the viewer `uv` to `QueryString` in the URL according to the rules of [key hotlink protection](https://intl.cloud.tencent.com/document/product/266/33986).

### Extracting the watermark

If you find out that your video has been pirated, you can call the [ExtractTraceWatermark](https://intl.cloud.tencent.com/document/product/266/50423) API to extract the `uv` of the viewer who pirated the video.

## Directions
Use the following steps to add a digital watermark and extract the viewer's ID:

[](id:step1)
### Step 1. Upload a video

1. In the VOD console, select **Video Management** > **Audio/Video Management** on the left sidebar, click **Upload Audio/Video**, and upload a video.
2. After uploading the video, note down the video ID.


[](id:step2)
### Step 2. Add a digital watermark

1. Refer to [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125) and use [API Explorer](https://console.cloud.tencent.com/api/explorer) to initiate an adaptive bitrate streaming task:
 * Enter the ID of the video uploaded in **[step 1](#step1)** for `FileId`.
 * Enter `10` for `MediaProcessTask.AdaptiveDynamicStreamingTaskSet.Definition`, which indicates to transcode with adaptive bitrate streaming template 10.
 * Enter `ON` for `MediaProcessTask.AdaptiveDynamicStreamingTaskSet.TraceWatermark.Switch`, which enables digital watermark.
2. After the task is completed, select **Video Management** > **Audio/Video Management** on the left sidebar in the console, find the target video, and click **Manage**. Find the adaptive bitstream of template 10 in the **Adaptive Bitrate Streaming Template** list, click **Copy URL**, and note down the playback URL.

### Step 3. Play the video

1. Add the `uv` (an 6-digit hexadecimal integer, such as `12abcd`) as `QueryString` to the playback URL obtained in **[step 2](#step2)** to get a new URL similar to `http://xxx.vod2.myqcloud.com/xxx/xxx/xxx.m3u8?uv=12abcd`. Copy the URL and paste it in a browser to play the video.


### Step 4. Mock video piracy

1. In the VOD console, select **Video Management** > **Audio/Video Management** on the left sidebar, click **Upload Audio/Video**, select **Pull** as the upload method, click **Add a Row**, and  enter the URL of the video obtained in **[step 3](#step3)**.
2. After the task is completed,  select **Video Management** > **Audio/Video Management** in the VOD console, find the uploaded video, and click **Manage**. Find the playback URL , click **Copy URL**, and note down the playback URL.

### Step 5. Extract the watermark

1. Refer to [ExtractTraceWatermark](https://intl.cloud.tencent.com/document/product/266/50423) and use [API Explorer](https://console.cloud.tencent.com/api/explorer) to initiate a watermark extraction task:
 * Enter the playback URL of the video uploaded in **[step 4](#step4)** for `URL`.
2.  After the task is completed,  refer to [DescribeTaskDetail](https://www.tencentcloud.com/document/product/266/34129) and use [API Explorer](https://console.cloud.tencent.com/api/explorer) to view the task details. The `uv` obtained in **[step 3](#step3)** will be found in the task output.



## Billing

Using the digital watermark feature involves the following fees:

* Transcoding fees: Because transcoding or adaptive bitrate streaming needs to be performed when you add a digital watermark to a video, transcoding fees will be incurred.
* Watermarking fees: When you add a digital watermark to a video, watermarking fees will be incurred.
* Storage fees: Because the output video of transcoding or adaptive bitrate streaming will use storage space, storage fees will be incurred.
* Extraction fees: When you extract the pirate's user ID after piracy is found, extraction fees will be incurred.

For the specific unit prices of the above billable items, see [Daily Pay-As-You-Go](https://intl.cloud.tencent.com/document/product/266/14666).
