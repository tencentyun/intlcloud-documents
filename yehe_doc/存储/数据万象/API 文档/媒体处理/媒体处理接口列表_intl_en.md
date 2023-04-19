## Job APIs

Job is an abstract concept. Media processing includes many types of jobs, such as transcoding, screenshot, and media information query.
A job contains three key pieces of information: input, output, and parameters. Input and output control the input file when the job is executed and the target file after the job is executed, and parameters control the detailed configurations for executing specific features.
A job can be either sync or async:
- Sync job: Jobs can be submitted synchronously for execution.
- Async job: Jobs are queued in the media processing queue in order of submission and priority.

<table>
<thead>
<tr>
<th colspan=2>Feature</th>
<th>Job API</th>
</tr>
</thead>
<tbody><tr>
<td rowspan=7>Basic processing</td>
<td>Audio/Video transcoding</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1045/48941">Submitting Audio/Video Transcoding Job</a></td>
</tr>
<tr>
<td>Top speed codec transcoding</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1045/49782">Submitting Top Speed Codec Transcoding Job</a></td>
</tr>
<tr>
<td>Video-to-animated image conversion</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1045/49569">Submitting Video-to-Animated Image Conversion Job</a></td>
</tr>
<tr>
<td>Video frame capturing</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1045/48938">Submitting Video Frame Capturing Job</a></td>
</tr>
<tr>
<td>Audio/Video remuxing</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1045/48936">Submitting Remuxing Job</a></td>
</tr>
<tr>
<td>Audio/Video splicing</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1045/48929">Submitting Video Splicing Job</a></td>
</tr>
<tr>
<td>Media information query</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1045/48932">Submitting Media Information Query Job</a></td>
</tr>
<tr>
<td rowspan=3>Image quality enhancement</td>
<tr>
<td>Image quality enhancement (including functions such as hyper-differentiation rate, interpolation, color enhancement, etc.)</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1045/48944">Submitting Image quality enhancement Job</a></td>
</tr>
<tr>
<td>Video quality scoring</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1045/48934">Submitting Video Quality Scoring Job</a></td>
</tr>
<tr>
<td>Copyright protection</td>
<td>Digital watermark</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1045/48930">Submitting Digital Watermark Adding Job</a></td>
</tr>
<tr>
<td rowspan=3>Smart editing</td>
<td>Video tagging</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1045/48945">Submitting Video Tagging Job</a></td>
</tr>
<tr>
<td>Video montage</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1045/48943">Submitting Video Montage Job</a></td>
</tr>
<tr>
<td>Intelligent thumbnail</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1045/48937">Submitting Intelligent Thumbnail Job</a></td>
</tr>
<tr>
<td rowspan=4>Smart voice</td>
<td>Audio noise cancellation</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1045/48933">Submitting Audio Noise Cancellation Job</a></td>
</tr>
<tr>
<td>Voice/Sound separation</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1045/48946">Submitting Voice/Sound Separation Job</a></td>
</tr>
<tr>
<td>Text to speech</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1045/48942">Submitting Text-to-Speech Job</a></td>
</tr>
<tr>
<td>Speech recognition</td>
<td><a href="https://www.tencentcloud.com/document/product/1045/49789">Submitting Speech Recognition Job</a></td>
</tr>
<tr>
<td rowspan=3>Sync jobs</td>
<td>Video frame capturing</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1045/49539">Getting Media File Screenshot</a></td>
</tr>
<tr>
<td>Media information query</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1045/49541">Getting Media File Information</a></td>
</tr>
<tr>
<td>Private M3U8</td>
<td><a href="https://www.tencentcloud.com/document/product/1045/49542">GetPrivateM3U8</a></td>
</tr>
</tbody></table>


## Template APIs
For media processing features such as audio/video transcoding, audio/video splicing, video frame capturing, and video-to-animated image conversion, you need to specify a template when creating a **job** or **workflow** in CI. The template page provides preset templates, and you can also customize templates based on your business needs. For more information on media processing templates, see [Media Processing](https://www.tencentcloud.com/document/product/1045/49899).

## Workflow APIs

A workflow in media processing refers to the process of automatically processing the specified uploaded file by configuring multiple job operations. For more information on calls, see [Workflow APIs](https://www.tencentcloud.com/document/product/1045/43618).

## Batch Operation APIs

A batch operation is to execute a single job or automatically perform operations configured in a workflow on the specified existing file. For more information on calls, see [Batch Job APIs](https://www.tencentcloud.com/document/product/1045/47027).
