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
      <td><img src="https://qcloudimg.tencent-cloud.cn/raw/82766338aee9f4f9715427e337babd25.png" width=500>

</td>
      <td><img src="https://qcloudimg.tencent-cloud.cn/raw/69dbaf292d144094854efca31e51d922.png" width=500>
			A watermark covering the video layer during playback in the player. It usually moves like a news ticker on the video image.</td>
   </tr>
</table>
These two types of watermarks have the following characteristics in terms of security and costs:

| Watermarking Method | Security | Costs |
| -- | -- | -- |
| Common image and text watermark | High: The watermark is encoded to the video and cannot be removed. | High: Each unique user ID watermark needs to be transcoded and stored once. |
| Player floating watermark | Low: The watermark appears in the video player but is not encoded to the video. | Low: It is embedded in the player. |

As shown above, neither of these two types of traditional watermarks can deliver both a high security and a low cost at the same time.

## VOD Digital Watermark

### How it works
<img src="https://qcloudimg.tencent-cloud.cn/raw/ccfa5b05ef291a3a115ca336e8a9cbab.jpg" width=999>

VOD's digital watermark uses an AB stream-based technology.

* Streams A and B are transcoded from the source video and segmented (the difference between streams A and B is the watermark position).
* CDN outputs a unique AB combined stream for each end user.
* The AB watermark sequence is extracted from the pirated video, and then the user ID is extracted from the watermark.

### Pros

The AB stream-based digital watermark can deliver a high security at low costs.

* Low costs: Only streams A and B need to be transcoded for a video. This means that it takes only the costs of transcoding and storing two streams to mark and track billions of viewers.
* High security: The watermark is encoded to the video image, so it cannot be removed even if the video data is obtained.

## Directions

### Adding a digital watermark

Create an image watermark template in the console or via APIs.
Call the [ProcessMeida](https://intl.cloud.tencent.com/document/product/266/34125) API to initiate a task to add a digital watermark to a video longer than 320 seconds.
* To add a digital watermark to the output video of transcoding, pass in the watermark template ID to `MediaProcessTask.TranscodeTaskSet.TraceWatermark.Definition`.
* To add a digital watermark to the output video of adaptive bitrate streaming, pass in the watermark template ID to `MediaProcessTask.AdaptiveDynamicStreamingTaskSet.TraceWatermark.Definition`.

### Playing back the video

You need to associate a `uid`, which is an 8-digit hexadecimal integer, with all your paid users. The `uid` will be used as the proof for viewer traceability.

* If you use the [Player SDK](https://intl.cloud.tencent.com/document/product/266/33977) or [Player Adapter](https://intl.cloud.tencent.com/document/product/266/42095) of VOD, your business server needs to distribute a [player signature](https://intl.cloud.tencent.com/document/product/266/38099) for each playback request. You need to enter the viewer `uid` as the `uid` in [signature parameters](https://intl.cloud.tencent.com/document/product/266/38099#.E7.AD.BE.E5.90.8D.E5.8F.82.E6.95.B0).
* If you don't use the VOD Player SDK, you need to add the viewer `uid` to `QueryString` in the URL according to the rules of [key hotlink protection](https://intl.cloud.tencent.com/document/product/266/33986).

### Extracting the watermark

If you find out that your video has been pirated, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to provide the pirated video file and watermark template ID. VOD will extract the `uid` of the viewer who pirated the video.

## Directions
Use the following steps to add a digital watermark and extract the viewer's ID:
[](id:step1)
### Step 1. Create a watermark template
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod), select **Video Processing Settings** > **Template Settings** on the left sidebar, select the **Watermark Template** tab, and click **Create Watermark Template**.
2. Select image watermark for **Watermark Type**. After uploading a watermark image, click **Create**.
3. Note down the watermark template ID of the newly created watermark template.

[](id:step2)
### Step 2. Upload a video

1. In the VOD console, select **Video Management** > **Audio/Video Management** on the left sidebar, click **Upload Audio/Video**, and upload a video (preferably longer than six minutes).
2. After uploading the video, note down the video ID.

[](id:step3)
### Step 3. Add a digital watermark

1. Refer to [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125) and use [API Explorer](https://console.cloud.tencent.com/api/explorer) to initiate an adaptive bitrate streaming task:
 * Enter the ID of the video uploaded in **[step 2](#step2)** for `FileId`.
 * Enter `10` for `MediaProcessTask.AdaptiveDynamicStreamingTaskSet.Definition`, which indicates to transcode with adaptive bitrate streaming template 10.
 * Enter the ID of the watermark template created in **[step 1](#step1)** for `MediaProcessTask.AdaptiveDynamicStreamingTaskSet.TraceWatermark.Definition`.
2. After the task is completed, select **Video Management** > **Audio/Video Management** on the left sidebar in the console, find the target video, and click **Manage**. Find the adaptive bitstream of template 10 in the **Adaptive Bitrate Streaming Template** list, click **Copy URL**, and note down the playback URL.

### Step 4. Play back and shoot the video

1. Add the `uid` (an 8-digit hexadecimal integer, such as `1234abcd`) as `QueryString` to the playback URL obtained in **[step 3](#step3)** to get a new URL similar to `http://xxx.vod2.myqcloud.com/xxx/xxx/xxx.m3u8?uid=1234abcd`. Copy the URL and paste it in a browser to play the video.
2. To simulate unauthorized video recording, use a mobile phone to record the video while it plays in the browser, and then save the recorded video as a video file.

### Step 5. Extract the watermark

[Submit a ticket](https://console.cloud.tencent.com/workorder/category) to VOD to provide the video obtained in **step 4** and the ID of the watermark template created in **[step 1](#step1)**. The VOD team will extract the `uid` of the user who is playing back (pirating) the video in the recorded video file.

## Billing

Using he digital watermark feature involves the following fees:

* Transcoding fees: Because transcoding or adaptive bitrate streaming needs to be performed when you add a digital watermark to a video, transcoding fees will be incurred.
* Storage fees: Because the output video of transcoding or adaptive bitrate streaming will use storage space, storage fees will be incurred.
* Extraction fees: When you [submit a ticket](https://console.cloud.tencent.com/workorder/category) to VOD to extract the pirate's user ID after piracy is found, extraction fees will be incurred.

For the specific unit prices of the above billable items, see [Daily Pay-As-You-Go](https://intl.cloud.tencent.com/document/product/266/14666).
