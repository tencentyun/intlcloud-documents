### What container formats and audio/video codecs do we support for transcoding?
We support the following video input formats:

| Container Format     | Video Codec | Audio Codec  |
|:---------:|:---:|:----:|
| MP4 | H.264 and H.265 |  AAC |
| FLV | H.264 and H.265 |  AAC |
| MOV | H.264, H.265, and MPEG4 |  AAC |
| WMV | WMV1 and WMV2 |  WMA1 and WMA2 |
| MKV | H264, VP8, and MPEG4 | AAC  |
| AVI | H264, WMV1, WMV2, and MPEG4 |  AAC, WMA1, and WMA2 |
| RMVB | RV series |  RAAC and RACP |
| TS | H.264, MP1V, and MP4V | MP1, MP2, MP3, and MP4A  |
| MPG | MPEG1 and MPEG2 |  MP2 |
| 3GP | H263 and MPEG4 |  AMR and AAC  |

We support the following video output formats:

| Container Format     | Video Codec | Audio Codec  |
|:---------:|:---:|:----:|
| MP4 | H.264 and H.265 |  AAC |
| HLS | H.264 and H.265 |  AAC |
| TS | H.264 and H.265 |  AAC |
| FLV | H.264 and H.265 | AAC  |
| DASH | H.264 and H.265 | AAC  |

We support the following audio input formats:

| Container Format   | Audio Codec  |
|:-----:|:---:|
| SILK | SILK |
| AMR | AMR |

We support the following audio output formats:

| Container Format   | Audio Codec  |
|:-----:|:---:|
| M4A | AAC |
| MP3 | LAME |


### Why wasn’t transcoding initiated?

Possible reasons and troubleshooting methods include:

- **Upload failed**: File upload through a Tencent Cloud COS SDK or in the COS Console failed, and an HTTP error code was returned (e.g., `4XX` or `5XX`). In this case, no COS event notification will be triggered, and MPS will not initiate a transcoding task. **Please check whether the file is successfully uploaded.**
- **Upload succeeded but did not trigger transcoding**: Possible reasons include: No workflow was set up, or the workflow was not set up correctly. **Please check and make sure that the workflow is set up properly.**

### Why did the transcoding initiation fail?

Possible reasons and troubleshooting methods include:

- **Incorrect request parameters**: If the API returns an error, please check the API parameters and make sure that the API call is successful.
- **No authorization**: If the API returns a permission-related error, please check whether you have granted MPS permissions to COS and CMQ resources.

### Why did transcoding fail?

Transcoding failure refers to a failure that occurs during any subtask. This includes transcoding, screencapturing, watermarking, video audit, content recognition and content analysis.
You can determine the error type based on the returned error code and message, as shown below:
- Incorrect source file metadata or unsupported format.
- Failed screencapturing (due to lack of video stream), unknown errors, etc.

If the error is relevant to the source file, please check the file metadata and encoding parameters. For other error types, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
