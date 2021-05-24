
Superplayer is the player feature provided by VOD, which allows you to specify the adaptive bitrate streaming output, image sprites as thumbnails, and definition through relevant configuration items. It also supports preview in the console. For more information, please see [Superplayer Preview](https://intl.cloud.tencent.com/document/product/266/33896).
>!For the sake of security, only the `default` template in VOD does not require to enable key hotlink protection for the domain name, while other templates can take effect only after key hotlink protection is enabled. If you have not set key hotlink protection, click [Domain Management](https://console.cloud.tencent.com/vod/distribute-play/domain) to enable it.


## Preset Configuration
VOD provides the following two preset configurations for your convenience:

<table class="table auto-table"><tbody><tr><th rowspan="2">Configuration Name</td><th colspan="3">Configuration Item</td></tr>
<tr><th>Adaptive bitstream to be played back (template ID)</td><th>Image sprite to be used (template ID)</td><th>Substream naming rule (based on length of substream short side)</td></tr>
<tr><td>default</td><td>10</td><td>10</td><td rowspan="2"><ul style="margin:0;"><li >240p: LD</li><li>480p: SD</li><li>720p: HD</li><li>1080p: FHD</li><li>1440p: 2K</li><li>2160p: 4K</li><li>Other: <code>xx</code>p (<code>xx</code> indicates the length of the video short side)</li></td></tr>
<tr><td>basicDrmPreset</td><td>12</td><td>10</td>
</tbody></table>


## Custom Configuration

Log in to the console, select **System Settings** > **[Superplayer Configuration](https://console.cloud.tencent.com/vod/distribute-play/super-player)**, and click **Create**:
1. Enter the playback configuration name (only **digits** and **letters** are supported).
2. Enter the playback configuration description (up to 15 characters).
3. Select a preset or previously created custom template in **Adaptive bitrate streaming template for playback**.
>?Your player can play back only the videos transcoded through the selected adaptive bitrate streaming template. For example, if the adaptive bitrate streaming template `10` is selected in the playback configuration, then your player can play back only videos transcoded through this template.
4. Select a preset or previously created custom image sprite template in **Image sprite template for thumbnail preview**.
>?Only the image sprites captured through the selected template can be used for thumbnail preview in your player. For example, if the `SpriteScreenShot10` template is selected in the playback configuration, only image sprites captured through the `SpriteScreenShot10` template can be used for preview in your player.
5. **Substream Names** displays the definitions as the names of substreams for playback. The default values will be used if you don't change them. You can also customize the video short side lengths and corresponding definitions.
6. Click **Confirm** to complete the creation.

After the configuration is successfully created, it will be displayed in the superplayer configuration list. You can also preview the corresponding configuration as instructed in [Superplayer Preview](https://intl.cloud.tencent.com/document/product/266/33896).


