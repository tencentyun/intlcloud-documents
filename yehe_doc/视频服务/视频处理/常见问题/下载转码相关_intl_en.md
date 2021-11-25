[](id:q1)
### What container formats and audio/video codecs are supported for transcoding?
<table>
   <tr>
      <th width="15%" style="text-align:center">Category</td>
      <th width="17%" style="text-align:center">Parameter</td>
      <th  style="text-align:center">Description</td>
   </tr>
   <tr>
      <td rowspan='3' style="text-align:center">Input formats</td>
      <td style="text-align:center">Container format</td>
      <td>3GP, AVI, FLV, MP4, M3U8, MPG, ASF, WMV, MKV, MOV, TS, WebM, MXF</td>
   </tr>
   <tr>
      <td style="text-align:center">Video codec</td>
      <td>AV1, AVS2, H.264/AVC, H.263, H.263+, H.265, MPEG-1, MPEG-2, MPEG-4, MJPEG, VP8, VP9, RealVideo, Windows Media Video, QuickTime</td>
   </tr><tr>
      <td style="text-align:center">Delete audio streams</td>
      <td>AAC, ADPCM, AMR, DSD, MP1, MP2, MP3, PCM, RealAudio, Windows Media Audio, Vorbis, AC-3</td>
   </tr>
   <tr>
      <td rowspan='5' style="text-align:center">Output formats</td>
      <td rowspan='3' style="text-align:center">Container format</td>
      <td>Video: FLV, MP4, HLS (M3U8 + TS), MXF</td>
   </tr><tr>
      <td>Audio: MP3, MP4, Ogg, FLAC, M4A</td>.
   </tr><tr>
      <td>Image: GIF, WebP</td>
   </tr>
   <tr>
      <td style="text-align:center">Video codec</td>
      <td>H.264/AVC, H.265/HEVC, AV1</td>
   </tr><tr>
      <td style="text-align: center; ">Audio codec</td>
      <td>MP3, AAC, FLAC, MP2, Vorbis</td>
   </tr><tr>
			 <td rowspan='2'  style="text-align:center">Packaging</td>
      <td style="text-align:center">Delete video streams</td>
      <td> If this is enabled, the transcoding result will contain only audio streams.</td>
   </tr>
	 	 	   <tr>
      <td style="text-align:center">Delete audio streams</td>
      <td> If this is enabled, the transcoding result will contain only video streams.</td>
</table>

[](id:q2)
### Why isn’t transcoding initiated?
See below for the possible cases and troubleshooting methods:

- **Upload failed**: If file upload through the COS SDK or via the console fails, and an HTTP error code (`4XX` or `5XX`) is returned, no COS event callback will be triggered, and MPS will not initiate the transcoding task. **Please check whether your file has been uploaded successfully.**
- **Upload successful**: If upload is successful but transcoding is not initiated, it may be because no workflow has been configured or the workflow is configured incorrectly. **Make sure you have configured a workflow correctly**.

[](id:q3)
### Why do I fail to initiate transcoding?

See below for the possible cases and troubleshooting methods:

- **Incorrect request parameters**: If the API returns an error, check your request parameters to ensure successful API call.
- **No authorization**: If the API returns a permission-related error, please check whether you have granted MPS permissions to COS and CMQ resources.

[](id:q4)

### What should I do if transcoding fails?

Transcoding failure is failure to finish any of the tasks MPS supports, including transcoding, screenshot, watermarking, intelligent video recognition, and intelligent video analysis.
Based on the error code and message returned, you can determine which of the following two categories an error belongs to:

- Incorrect source file metadata or unsupported format.
- Failed to take a screenshot (due to lack of video stream), unknown errors, etc.

If the error is relevant to the source file, please check the file metadata and encoding parameters. For other error types, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

[](id:q5)

### How do I download videos in batches?
MPS does not support batch download currently.

[](id:q6)
### Can I download files in PS format?
No, you can’t. See the table below for supported formats:

| Format | Video Codec            | Audio Codec        |
| -------- | ----------------------- | ------------------- |
| MP4      | H.264, H.265            | AAC                 |
| FLV      | H.264, H.265            | AAC                 |
| MOV      | H.264, H.265, MPEG4     | AAC                 |
| WMV      | WMV1, WMV2              | WMA1, WMA2          |
| MKV      | H264, VP8, MPEG4        | AAC                 |
| AVI | H264, WMV1, WMV2, MPEG4 |  AAC, WMA1, WMA2 |
| RMVB     | RealVideo                 | RAAC, RACP          |
| TS | H.264, MP1V, MP4V | MP1, MP2, MP3, MP4A  |
| MPG      | MPEG1, MPEG2            | MP2                 |
| 3GP      | H263, MPEG4             | AMR, AAC            |

[](id:q7)
### Why aren’t my videos output at the specified bitrate?
Without compromising visual experience, MPS reduces the quality of unimportant frames to lower the output bitrate.
If you want your videos to be output at the specified bitrate, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) and provide us the ID of your transcoding template so that we can make adjustment accordingly.

[](id:q8)
### Can I convert a video to higher resolution using MPS? Will this improve video quality?
We don’t recommend transcoding a video of low resolution into one of high resolution. MPS has to stretch the original video to achieve this. As most low-resolution videos have low bitrate, the results are not satisfactory even if you increase the bitrate. All transcoding operations of MPS are performed on original videos. We recommend you retain the quality of original videos.

[](id:q9)
### How do I set the resolutions of legacy transcoding templates?
If the vertical resolution in your legacy template is 720p and horizontal resolution proportionally scaled, choose **Set by width and height** and set height to 720 px and width to 0, as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/8f506fb7b469cc022ae910fce6ee3606.png)

[](id:q10)
### If the trigger directory is the same as the output directory, will MPS trigger transcoding for output videos again?
No, it won’t. For details, see [Triggering Transcoding Task](https://intl.cloud.tencent.com/document/product/1041/33492).

[](id:q11)
### How do I view my transcoding usage?
Log in to the [MPS console](https://console.cloud.tencent.com/mps) and click **Usage Statistics** to view detailed transcoding statistics.
The page displays transcoding statistics for today, yesterday, the last 7 days, the last 30 days. You can also customize a time period within the last 30 days.
Transcoding usage is classified into **General Transcoding** and **TESHD**.

- General Transcoding Duration: Indicates the total transcoding duration under this transcoding category within the specified time period.
- General Transcoding Tasks: Indicates the total number of transcoding tasks under this transcoding category within the specified time period.
- Transcoding Trend: Displays the duration curves for different output resolutions.
- Transcoding Details: Displays transcoding details including transcoding resolution, transcoding duration, and number of transcoding tasks under the chosen transcoding category within the specified time period.
- Transcoding Ratio: Displays the ratios of transcoding durations for different output resolutions under the chosen transcoding category.
  ![image.png](https://qcloudimg.tencent-cloud.cn/raw/6df46aa04cdf2518580a166e06a4427b.png)

