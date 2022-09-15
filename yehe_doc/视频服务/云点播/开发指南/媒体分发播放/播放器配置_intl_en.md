When using the Player SDK to play back a VOD video, you need to specify the image content and thumbnail.

The video **image content** is of one of the following types:

* The output video of [adaptive bitrate streaming](https://intl.cloud.tencent.com/document/product/266/33942)
* The output video of [transcoding](https://intl.cloud.tencent.com/document/product/266/33938)
* The [uploaded](https://intl.cloud.tencent.com/document/product/266/9760) source video

**Thumbnail** preview is the output image of an [image sprite](https://intl.cloud.tencent.com/document/product/266/33940).

An adaptive bitstream contains multiple substreams that correspond to different definition names during definition switching. When specifying the definition name of each substream displayed in the player, you need to specify the naming rule for the substream definitions.

## Player Configuration Item

VOD provides the **player configuration**. In the configuration, you can specify whether to play back the output video of adaptive bitrate streaming or transcoding or the uploaded source video.
When playing back an output video of adaptive bitrate streaming, you need to specify the **adaptive bitrate streaming template ID**. When playing back an output video of transcoding, you need to specify the **transcoding template ID**. When using the thumbnail preview, you need to specify the **image sprite template ID**.
The player configuration allows you to customize the **definition naming rule** (such as LD, SD, and HD) of each substream.

| Configuration Item | Configuration Method | Feature |
| -- | -- | -- |
| Image content to be displayed | Select one of the following options through the type field:<li>Play back the uploaded source video.</li><li>Play back the output video of transcoding: The transcoding template ID.</li><li>Play back the output video of adaptive bitrate streaming: The adaptive bitrate streaming template ID.</li> | Controls the content of the video image played back by the player. |
| Image sprite template for thumbnail preview | Specify image sprite template ID | Controls the thumbnails displayed on the progress bar. |
| Substream definition name displayed by the player | Specify the names corresponding to the length of the substream short side | Controls the names of the definitions that can be switched to during playback. |

## Preset Configuration
VOD provides the following two preset configurations for your convenience:

<table class="table auto-table"><tbody><tr ><th rowspan="2">Configuration Name</td><th colspan="3">Configuration Item</td></th>
<tr><th>The Image Content to Be Played Back</td><th>Thumbnail Preview</td><th>The Definition Naming Rule (Based on the Length of the Substream Short Side)</td></tr>
<tr><td>default</td><td>The adaptive bitstream generated with template 10</td><td>The image sprite generated with template 10</td><td rowspan="2"><ul style="margin:0;"><li >240p: LD.</li><li>480p: SD.</li><li>720p: HD.</li><li>1080p: FHD.</li><li>1440p: 2K.</li><li>2160p: 4K.</li><li>Others: <code>xx</code>p (<code>xx</code> indicates the length of the video short side).</li></td></tr>
<tr><td>basicDrmPreset</td><td>The adaptive bitstream generated with template 12</td><td>The image sprite generated with template 10</td>
</tbody></table>

* If the video content does not require encryption, you can use the `LongVideoPreset` preset task flow for adaptive bitrate streaming and the `default` preset player configuration for playback. For specific samples, see [Stage 1. Play back a video with superplayer](https://intl.cloud.tencent.com/document/product/266/38098).
* If you need to play back encrypted content, you can use the `SimpleAesEncryptPreset` preset task flow for adaptive bitrate streaming and the `basicDrmPreset` preset player configuration for playback. For specific samples, see [Stage 4. Play back an encrypted video](https://intl.cloud.tencent.com/document/product/266/38294).

## Custom Configuration
In addition to using preset player configurations, you can also customize the configuration in the [console](https://intl.cloud.tencent.com/document/product/266/38261) or through [API](https://intl.cloud.tencent.com/document/product/266/37567).
You can use a custom player configuration for playback as instructed in [Stage 1. Play back a video with superplayer](https://intl.cloud.tencent.com/document/product/266/38098).

## Using Configuration
If you use a configuration rather than the `default` preset configuration, you need to use the [player signature](https://intl.cloud.tencent.com/document/product/266/38099) and specify the configuration name to be used in the `pcfg` signature parameter.
You can use the player signature for playback as instructed in [Stage 1. Play back a video with superplayer](https://intl.cloud.tencent.com/document/product/266/38098).
