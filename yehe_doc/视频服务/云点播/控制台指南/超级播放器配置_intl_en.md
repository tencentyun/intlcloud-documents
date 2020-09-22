
Superplayer is the player feature provided by VOD, which allows you to specify the adaptive bitrate streaming output, image sprites as thumbnails, and definition through relevant configuration items. It also supports preview in the console. For more information, please see [Superplayer Preview](https://intl.cloud.tencent.com/document/product/266/33896).
>!For the sake of security, only the `default` template in VOD currently does not require to enable key hotlink protection for the domain name, while other templates can take effect only after key hotlink protection is enabled. If you have not set key hotlink protection, click [Domain Management](https://console.cloud.tencent.com/vod/distribute-play/domain) to enable it.


## Preset Configuration
VOD provides the following two preset configurations for your convenience:

<table class="table auto-table"><tbody><tr><th rowspan="2">Configuration Name</td><th colspan="3">Configuration Item</td></tr>
<tr><th>Adaptive bitstream to be played back (template ID)</td><th>Image sprite to be used (template ID)</td><th>Substream naming rule (based on length of substream short side)</td></tr>
<tr><td>default</td><td>10</td><td>10</td><td rowspan="2"><ul style="margin:0;"><li >240p: LD</li><li>480p: SD</li><li>720p: HD</li><li>1080p: FHD</li><li>1440p: 2K</li><li>2160p: 4K</li><li>Other: <code>xx</code>p (<code>xx</code> indicates the length of the video short side)</li></td></tr>
<tr><td>basicDrmPreset</td><td>12</td><td>10</td>
</tbody></table>


## Custom Configuration

Log in to the console, select **Distribution and Playback Settings** > **[Superplayer Settings](https://console.cloud.tencent.com/vod/distribute-play/super-player)**, and click **Create**:
1. Enter the playback configuration name (only **digits** and **letters** are supported).
2. Enter the playback configuration description (up to 15 characters).
3. Select a preset or previously created custom template in **Adaptive bitrate streaming template for playback**.
>?This configuration item specifies the adaptive bitrate streaming template through which video files that can be played back by your player are transcoded. For example, if the adaptive bitrate streaming template `10` is selected in the playback configuration, then the player can play back only videos transcoded through this template.
4. Select a preset or previously created custom image sprite template in **Image sprite template for thumbnail preview**.
>?This configuration item specifies the image sprite file for thumbnail preview in the player. For example, if the `SpriteScreenShot10` template is selected in the playback configuration, only image sprites captured through the `SpriteScreenShot10` template can be used for preview in the player.
5. Name the substreams for different resolutions for the player in **Definition used for the player to play substreams**. If this configuration item is left empty, the default value will be used. You can customize the video short side length and definition.
6. Click **OK** to complete the creation.

After the configuration is successfully created, it will be displayed in the superplayer configuration list. You can also preview the corresponding configuration as instructed in [Superplayer Preview](https://intl.cloud.tencent.com/document/product/266/33896).


