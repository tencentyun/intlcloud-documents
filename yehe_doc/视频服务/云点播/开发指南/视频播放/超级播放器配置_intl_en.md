When you use the superplayer to play back a video, the video **image content** is the [adaptive bitrate streaming](https://intl.cloud.tencent.com/document/product/266/33942) output, and the **thumbnail preview** is the [image sprite](https://intl.cloud.tencent.com/document/product/266/33940) output.
If your video has multiple adaptive bitrate streaming and image sprite outputs, you need to specify:

* Which adaptive bitstream is to be played back.
* Which image sprite is to be used as thumbnails.

An adaptive bitstream contains multiple substreams, which correspond to different resolution names during resolution switch. When specifying the resolution name of each substream displayed in the player, you need to specify the naming rule for the substream resolutions.

## Player Configuration Item

VOD supports **superplayer configuration**, where you can specify the **adaptive bitrate streaming template ID** and **image sprite template ID**. In addition, it allows you to customize the **resolution naming rule** (such as LD, SD, and HD) of each substream.

| Configuration Item | Configuration Method | Feature |
| -- | -- | -- |
| Adaptive bitstream for playback | Adaptive bitrate streaming template ID | It controls the content played back by the player |
| Image sprite template for thumbnail preview | Image sprite template ID | It controls the thumbnails displayed on the progress bar. |
| Substream resolution name displayed by player | Naming of the length of substream short side | It controls the names of resolutions for resolution switch |

## Preset Configuration
VOD provides the following three preset configurations for your convenience:

<table class="table auto-table"><tbody><tr ><th rowspan="2">Configuration Name</td><th colspan="3">Configuration Item</td></th>
<tr><th>Adaptive bitstream to be played back (template ID)</td><th>Image sprite to be used (template ID)</td><th>Resolution naming rule (based on length of substream short side)</td></tr>
<tr><td>default</td><td>10</td><td>10</td><td rowspan="3"><ul style="margin:0;"><li >240p: LD</li><li>480p: SD</li><li>720p: HD</li><li>1080p: FHD</li><li>1440p: 2K</li><li>2160p: 4K</li><li>Others: <code>xx</code>p (<code>xx</code> indicates the length of the video short side)</li></td></tr>
<tr><td>basicDrmPreset</td><td>12</td><td>10</td>
<tr><td>advanceDrmPreset</td><td><li>when client supports FairPlay, play 11</li><li>when client supports Widevine, play 13</li></td><td>10</td>
</tbody></table>

* If the video content does not require encryption, you can use the `LongVideoPreset` preset task flow for adaptive bitrate streaming and the `default` preset superplayer configuration for playback. For specific samples, please see [Integration Guide](https://intl.cloud.tencent.com/document/product/266/38098).
* If you need to play back VOD priavte protocal encrypted content, you can use the `SimpleAesEncryptPreset` preset task flow for adaptive bitrate streaming and the `basicDrmPreset` preset superplayer configuration for playback. For specific samples, please see [Integration Guide](https://intl.cloud.tencent.com/document/product/266/38294).
* If you need to play back DRM protected content, you can use the `WidevineFairPlayPreset` preset task flow for adaptive bitrate streaming and the `advanceDrmPreset` preset superplayer configuration for playback.



## Custom Configuration
In addition to using preset superplayer configurations, you can also customize the configuration in the [console](https://intl.cloud.tencent.com/document/product/266/38261) or through [API](https://intl.cloud.tencent.com/document/product/266/37567).
You can use a custom superplayer configuration for playback as instructed in [Integration Guide](https://intl.cloud.tencent.com/document/product/266/38098).

## Using Configuration
If you use a configuration rather than the `default` preset configuration, you need to use the [superplayer signature](https://intl.cloud.tencent.com/document/product/266/38099) and specify the configuration name to be used in the `pcfg` signature parameter.
You can use the superplayer signature for playback as instructed in [Integration Guide](https://intl.cloud.tencent.com/document/product/266/38098).