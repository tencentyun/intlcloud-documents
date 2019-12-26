### What container formats and audio/video codecs are supported by the transcoding service?
Supported video input formats include:

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

Supported video output formats include:

| Container Format     | Video Codec | Audio Codec  |
|:---------:|:---:|:----:|
| MP4 | H.264 and H.265 |  AAC |
| HLS | H.264 and H.265 |  AAC |
| TS | H.264 and H.265 |  AAC |
| FLV | H.264 and H.265 | AAC  |
| DASH | H.264 and H.265 | AAC  |

Supported audio input formats include:

| Container Format   | Audio Codec  |
|:-----:|:---:|
| SILK | SILK |
| AMR | AMR |

Supported audio output formats include:

| Container Format   | Audio Codec  |
|:-----:|:---:|
| M4A | AAC |
| MP3 | LAME |


### What if no transcoding is initiated?

Possible reasons and troubleshooting methods include:

- **Upload failed**: File upload through a Tencent Cloud COS SDK or in the COS Console failed, and an HTTP error code is returned (e.g., `4XX` or `5XX`). In this case, no COS event notification will be triggered, and MPS will not initiate a transcoding task. **Please check whether the file is successfully uploaded.**
- **Upload succeeded but did not trigger transcoding**: Possible reasons include: No workflow is set up, or the workflow is incorrectly configured. **Please check and make sure that the workflow is correctly configured.**

### What if transcoding fails to be initiated?

Possible reasons and troubleshooting methods include:

- **Incorrect request parameters**: If the API returns an error, please check the API parameters and make sure that success is returned for the API call.
- **No authorization**: If the API returns a permission-related error, please check whether you have grant MPS the permission to COS and CMQ resources.

### What if transcoding fails?

Transcoding failure refers to a failure that occurs during any subtask in MPS, such as transcoding, screencapturing, watermarking, and intelligent audit, recognition, analysis, and release.
You can determine the error type based on the returned error code and message, as shown below:
- Incorrect source file metadata or unsupported format.
- Failed screencapturing (due to lack of video stream), unknown errors, etc.

If the error is relevant to the source file, please check file metadata and encoding parameters. For errors of other types, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
