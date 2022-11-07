One of the main pain points of subscription-based video streaming platforms is that people may download their videos and share or sell them elsewhere without authorization. This can result in great losses for the copyright holders. To deter piracy, an effective way is to track down the sources and hold them liable or demand compensation. VOD’s digital watermarks, which feature high security, low costs, and high robustness, help you achieve this without compromising viewing experience.

## Shortcomings of Traditional Watermarks

Traditional measures against unauthorized video recording work by adding viewers’ user IDs to videos. A user ID is **either encoded into the video as a common text/image watermark or placed as an image layer over the source video by the player**.

<table>
   <tr>
      <th width="0px" style="text-align:center">Common text/image watermark</td>
      <th width="0px" style="text-align:center">Player-based floating watermark</td>
   </tr>
   <tr>
      <td><img src="https://qcloudimg.tencent-cloud.cn/raw/82766338aee9f4f9715427e337babd25.png" width=500>The image or text watermark showing the viewer’s user ID is encoded into the video.

</td>
      <td><img src="https://qcloudimg.tencent-cloud.cn/raw/69dbaf292d144094854efca31e51d922.png" width=500>
			The player places a watermark image layer over the source video during playback. The watermark usually moves randomly across the screen.</td>
   </tr>
</table>
The table below compares the two types of watermarks:

|  | Common Text/Image Watermark | Player-Based Floating Watermark |
| -- | -- | -- |
| Security | High: The watermark is encoded into the video and is difficult to remove. | Relatively low: The watermark is added as an image layer and is not encoded into the video. |
| Costs | High: Watermarking is required for each viewer, which means transcoding and storage fees are incurred each time a video is played. | Low: The watermark is a built-in feature of the VOD player. |
| Robustness | Low: The watermark appears at a fixed position, which makes it easy to crop it out or cover it. | Relatively low: The watermark is visible and may be easily covered. |
| Viewing experience | Affected: The watermark is visible and affects viewing experience. | Affected: The watermark is visible and affects viewing experience. |


As you can see, traditional watermarking solutions have their limits.

## VOD Digital Watermarks

VOD’s digital watermarking solution features low costs, high security, and high robustness, and does not compromise viewing experience.

* Low costs: Each watermarked video is charged only once for transcoding and storage, regardless of the number of viewers.
* High security: The watermark is encoded into the video and cannot be removed from recorded or downloaded copies.
* High robustness: The watermark works under different conditions (resampling, compression, dithering, cropping, scaling, rotation, wave filtering, and so on.)
* Viewing experience: The watermark does not affect the video quality and is invisible to the human eye.

>! VOD’s digital watermarking feature is currently in beta testing and has certain limits:
>1. It only works for videos **longer than 30 minutes**.
>2. Currently, it delivers better tracking results for **movies, TV dramas, and variety shows**.
>3. We are still working on digital watermarks for **online course videos**. If you are from the education sector, please check back soon for the official launch of the digital watermarking feature.

## Directions

### Adding a digital watermark

Call the [ProcessMeida](https://intl.cloud.tencent.com/document/product/266/34125) API to start a transcoding or adaptive bitrate task to add a watermark.

#### Transcoding
* Select an HLS transcoding template such as the preset template 100230 (MediaProcessTask.TranscodeTaskSet.Definition=100230)
* Enable digital watermarks (MediaProcessTask.TranscodeTaskSet.TraceWatermark.Switch=ON)

#### Adaptive bitrate
* Select an HLS adaptive bitrate template, such as the preset template 10 (MediaProcessTask.AdaptiveDynamicStreamingTaskSet.Definition=10).
* Enable digital watermarks (MediaProcessTask.AdaptiveDynamicStreamingTaskSet.TraceWatermark.Switch=ON).

### Playing back the video

You need to assign each paid user a six-digit hexadecimal integer as the viewer ID (`uv`), which will be used for ID extraction.

* If you use VOD’s [Player SDK](https://intl.cloud.tencent.com/document/product/266/33977) or [player adapter](https://intl.cloud.tencent.com/document/product/266/42095), you need to assign a [player signature](https://intl.cloud.tencent.com/document/product/266/38099) for each playback request (set the [signature parameter](https://intl.cloud.tencent.com/document/product/266/38099#.E7.AD.BE.E5.90.8D.E5.8F.82.E6.95.B0) `uv` to the viewer’s viewer ID).
* If you don't use VOD’s Player SDK, you need to add the `uv` parameter (the value of which is the viewer’s viewer ID) to the query string of the request URL according to the splicing rules of [hotlink protection URLs](https://intl.cloud.tencent.com/document/product/266/33986).

### Extracting the watermark

In case of unauthorized video distribution, call [ExtractTraceWatermark](https://www.tencentcloud.com/document/product/266/50423) to extract the distributor’s viewer ID (`uv`).

## Directions
Follow the steps below to add a digital watermark and extract the viewer's ID.

[](id:step1)
### Step 1. Upload a video

1. In the VOD console, select **Media Assets > Video/Audio Management** on the left sidebar, and click **Upload** to upload a video.
2. Note the file ID.

[](id:step2)
### Step 2. Add a digital watermark

1. Refer to the [document](https://intl.cloud.tencent.com/document/product/266/34125) about the `ProcessMedia` API and use [API Explorer](https://console.cloud.tencent.com/api/explorer) to initiate an adaptive bitrate streaming task.
 * For **FileId**, enter the file ID noted in [step 1](#step1).
 * Set `MediaProcessTask.AdaptiveDynamicStreamingTaskSet.0.Definition` to `10`, which indicates to use the adaptive bitrate template 10.
 * Set `MediaProcessTask.AdaptiveDynamicStreamingTaskSet.0.TraceWatermark.Switch` to `ON`.
2. After the task is completed, in the VOD console, select **Media Assets** > **Video/Audio Management** on the left sidebar, find the watermarked video, and click **Manage**. In **Adaptive Bitrate Streaming Template List**, find template 10, and click **Copy URL**.

[](id:step3)
### Step 3. Play the watermarked video

1. In the playback URL obtained in [step 2](#step2), add a query string parameter `uv` and pass in a six-digit hexadecimal integer. For example, if you pass in `12abcd`, the URL of the watermarked video would be `http://xxx.vod2.myqcloud.com/xxx/xxx/xxx.m3u8?uv=12abcd`. Open this URL with a browser to play the watermarked video.

[](id:step4)
### Step 4. Get the watermarked video

1. In the VOD console, select **Media Assets > Video/Audio Management** on the left sidebar. Click **Upload**, select **Pull**, enter the URL spliced in step 3, and click **Pull**.
2. Return to the **Video/Audio Management** page, find the video pulled and click **Manage**. In the **Basic Info** area, find **Operation**, and click **Copy address**.

[](id:step5)
### Step 5. Extract the viewer ID

1. Refer to the [document](https://www.tencentcloud.com/document/product/266/50423) about the `ExtractTraceWatermark` API and use [API Explorer](https://console.cloud.tencent.com/api/explorer) to start a digital watermark extraction task. Set the request parameter `Url` to the URL you copied in [step 4](#step4).
2. After the extraction task is completed, refer to the [document](https://cloud.tencent.com/document/api/266/33431) about the `DescribeTaskDetail` API and use [API Explorer](https://console.cloud.tencent.com/api/explorer) to query the extraction task. In the response, you will find the viewer ID assigned in [step 3](#step3). This concludes the ID extraction process.

## Billing

Using the digital watermark feature involves the following fees:

* Transcoding fees: Because transcoding or adaptive bitrate streaming needs to be performed when you add a digital watermark to a video, transcoding fees will be incurred.
* Watermarking fees: Watermarking fees will be incurred for adding digital watermarks.
* Storage fees: Because the output video of transcoding or adaptive bitrate streaming will use storage space, storage fees will be incurred.
* Extraction fees: Extracting the ID of the viewer responsible for unauthorized distribution will incur extraction fees.

For the pricing details, see [Daily Pay-As-You-Go](https://intl.cloud.tencent.com/document/product/266/14666).
