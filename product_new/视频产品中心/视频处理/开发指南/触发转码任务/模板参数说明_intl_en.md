When creating a parameter template, you need to customize parameters in it such as the bitrate, video width and height, remuxing format, and codec. The meanings and value ranges of key parameters in each type of parameter templates are as shown below:

## Audio/Video Transcoding Template

<table>
    <tr>
        <th style="width:18%">  Category </th>
        <th style="width:22%">  Parameter </th>
        <th> Description  </th>
    </tr>
    <tr>  <td rowspan=4>  Muxing </td>
    </tr>
    <tr>
        <td> Container format  </td>
        <td> The following video and audio container formats are supported:
            <li>Video: MP4, TS, HLS, and FLV</li>
            <li>Audio: MP3, M4A, FLAC, and OGG</li>
        </td>
    </tr>
    <tr>
        <td> Video stream deletion  </td>
        <td> If this parameter is enabled, the output video after transcoding will contain only the audio stream with the video stream discarded</td>
    </tr>
    <tr>
        <td>  Audio stream deletion </td>
        <td> If this parameter is enabled, the output video after transcoding will contain only the video stream with the audio stream discarded</td>
    </tr>
    <tr>
        <td rowspan=7>   Video encoding   </td>
        <td>     Codec </td>
        <td> H.264 and H.265 are supported  </td>
    </tr>
    <tr>
        <td>  Bitrate </td>
        <td>  Supported bitrate range: 10–35 Mbps   </td>
    </tr>
    <tr>
        <td> Frame rate </td>
        <td> Supported frame rate range: 1–60 fps; common values: 24, 25, and 30 fps  </td>
    </tr>
    <tr>
        <td> Resolution </td>
        <td> 
            <li>Supported width range: 128–4,096 px</li>
            <li>Supported height range: 128–4,096 px</li>
        </td>
    </tr>
    <tr>
        <td> GOP length </td>
        <td> Supported GOP length range: 1–10s </td>
    </tr>
    <tr>
        <td> Profile </td>
        <td>
            <li>When the video codec is H.264, the `Baseline`, `Main`, and `High` profiles are supported</li>
            <li>When the video codec is H.265, only the `Main` profile is supported</li>
        </td>
    </tr>
    <tr>
        <td> Color space </td>
        <td> YUV420P is supported </td>
    </tr>
    <tr>
        <td rowspan=4> Audio encoding parameters </td>
        <td> Codec </td>
        <td> MP3, AAC, AC3, and FLAC are supported </td>
    </tr>
    <tr>
        <td> Sample rate </td>
        <td>
            The following audio sample rates are supported:
            <li>34,000 Hz</li>
            <li>44,100 Hz</li>
            <li>48,000 Hz</li>
        </td>
    </tr>
    <tr>
        <td> Bitrate </td>
        <td>
            Supported bitrate range: 26–256 Kbps, including the following values:
            <li>48 Kbps</li>
            <li>64 Kbps</li>
            <li>128 Kbps</li>
        </td>
    </tr>
    <tr>
        <td> Channel </td>
        <td>
        	<li>Mono</li>
		    <li>Dual</li>
			<li>Stereo</li>
        </td>
    </tr>
</table>

## Watermarking Template

| Parameter      | Description     |
| ------------- | ------ |
| Type  | Image and text watermarks are supported: <li>Image watermark: Static or animated images are supported</li><li>Text watermark: Texts in various languages are supported</li> |
| Position | Relative position of a watermark in the video    |
| ImageSize | Size of an image watermark in the video     |
| ImageContent | Binary content of an image watermark |
| FontSize     | Font size of a text watermark |
| FontType     | Font of a text watermark, e.g., Times New Roman |
| FontColor    | Color of a text watermark, e.g., 0xRRGGBB   |
| FontAlpha  | Transparency of text watermark. Value range: 0–100% |

## Screencapturing Template

### Time point screencapturing template

A time point screencapturing template is used to take a screenshot at a specified time point or take a screenshot as a cover.

| Parameter       | Description            |
| ----------- | --------- |
| Format   | Output format of a screenshot file. Currently, only JPG is supported   |
| Width        | Screenshot width. Value range: 128–4,096 px  |
| Height     | Screenshot height. Value range: 128–4,096 px   |
| FillType | Filling refers to the way of processing a screenshot when its aspect ratio is different from that of the source video. Generally, the following filling types are supported: <li>Stretch: The screenshot is stretched to match the aspect ratio of the source video, which may make the screenshot "shorter" or "longer" </li><li>Fill with black: This option retains the aspect ratio of the source video for the screenshot and fill the unmatched area with black color blocks </li><li>Fill with white: This option retains the aspect ratio of the source video for the screenshot and fill the unmatched area with white color blocks </li><li>Gaussian blur: This option retains the aspect ratio of the source video for the screenshot and fills the unmatched area with Gaussian blur </li> |

### Sampled screencapturing template

A sampled screencapturing template is used to take sampled screenshots.

| Parameter  | Description  |
| ----------- | -- |
| Format  | Output format of a screenshot file. Currently, only JPG is supported    |
| Width   | Screenshot width. Value range: 128–4,096 px         |
| Height  | Screenshot height. Value range: 128–4,096 px         |
| SampleType | The following two types are supported: <li>Sample by percent: If this type is selected and `Interval` is set to `5%` for example, 20 screenshots will be generated </li><li>Sample by time: If this type is selected and `Interval` is set to `10s` for example, the number of generated screenshots will depend on the video length </li> |
| Interval   | Sampling interval. <li>If the sampling type is by percent, this parameter will be a percent value </li><li>If the sampling type is by time, this parameter will be a second value </li> |
| FillType | Filling refers to the way of processing a screenshot when its aspect ratio is different from that of the source video. Generally, the following filling types are supported: <li>Stretch: The screenshot is stretched to match the aspect ratio of the source video, which may make the screenshot "shorter" or "longer" </li><li>Fill with black: This option retains the aspect ratio of the source video for the screenshot and fill the unmatched area with black color blocks </li><li>Fill with white: This option retains the aspect ratio of the source video for the screenshot and fill the unmatched area with white color blocks </li><li>Gaussian blur: This option retains the aspect ratio of the source video for the screenshot and fills the unmatched area with Gaussian blur </li> |

### Image sprite generating template

An image sprite screencapturing template is used to take screenshots and combine them to generate an image sprite.

| Parameter         | Description              |
| ------------ | ------------------ |
| Format       | Output format of an image sprite file. Currently, only JPG is supported                         |
| Width      | Subimage width of an image sprite                     |
| Height   | Subimage height of an image sprite                       |
| Rows       | Number of rows of subimages in an image sprite                  |
| Columns    | Number of columns of subimages in an image sprite                   |
| SampleType | Sampling type of subimages. Currently, only sampling by time is supported |
| Interval   | Time interval for capturing a screenshot as a subimage     |

>
>- The value of `Width` * `Columns` should be between 128 and 4,096 px (i.e., the range of the image sprite width).
>- The value of `Height` * `Rows` should be between 128 and 4,096 px (i.e., the range of the image sprite height).


## Animated Image Generating Template

The target specification of an animated image is subject to parameters such as animated image format, width, height, and frame rate.

| Parameter             | Description       |
| ---------------- | ---------- |
| Format   | Output format of an animated image file. Currently, only GIF and WEBP are supported |
| Width    | Animated image width. Value range: 128–4,096 px          |
| Height | Animated image height. Value range: 128–4,096 px           |
| FPS      | Supported frame rate range: 1–60 fps                  |
