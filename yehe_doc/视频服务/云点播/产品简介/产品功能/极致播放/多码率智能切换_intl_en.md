## Overview
Adaptive bitrate streaming allows the video player to automatically switch to the audio/video stream at the most appropriate bitrate based on the user's current network conditions. Under poor network conditions, the video stream at a low resolution will be played back to guarantee the playback smoothness. Under good network conditions, a video stream at a higher resolution will be switched to automatically to fully utilize the bandwidth and deliver an optimal image quality. To implement this feature, you need to output the source audio/video stream as audio/video streams with various specifications (including bitrate and video resolution) and package them to generate an adaptive bitstream file, so that the player can automatically select and play back the bitstream best suiting the current bandwidth.
The adaptive bitrate streaming feature of VOD is industry-leading in terms of feature comprehensiveness and ease of use.

<table>
    <tr>
        <th style="width:160px">
            Strength               
        </th>
				<th>
           Description
        </th>
    </tr>
		 <tr>
        <td>
            Comprehensive features
        </td>
				<td>
				<li>Adaptive bitrate streaming supports HLS and MPEG-DASH formats.</li>
				<li>Adaptive bitrate streaming supports advanced features such as encryption and digital rights management (DRM).</li>
        </td>
 </tr>
	 <tr>
        <td>
            Ease of use
        </td>
				<td>
				<li>All parameters of an adaptive bitrate streaming task of VOD can be set in a template. Rather than configuring complex parameters, you only need to enter a template ID. It provides common preset system templates for you to use directly, and you can also manage your own custom templates.</li>
				<li>Adaptive bitrate streaming supports automatic task triggering upon upload completion. You can specify the task flow parameters during upload, and the adaptive bitrate streaming task will be triggered automatically upon the completion of audio/video upload, eliminating the need to initiate a task manually.</li>
				<li>Adaptive bitrate streaming can be initiated manually for existing audios/videos. You only need to specify the template ID when initiating a task.</li>
				<li>The VOD Player SDK can play back adaptive bitstreams quickly and conveniently after simple and quick integration.</li>
        </td>
 </tr>
</table>

## Use cases
<table>
    <tr>
        <th style="width:160px">
            Scenario               
        </th>
				<th>
           Description
        </th>
    </tr>
		<tr>
        <td>
            Ecommerce platforms
        </td>
				<td>
				Audios/videos are available in multiple definitions. When a viewer plays a product video, playback smoothness is guaranteed first, and the stream with the optimal video definition is switched to automatically based on the viewer’s network conditions.
        </td>
    </tr>
	<tr>
        <td>
            Video website
        </td>
				<td>
				The same video is available in multiple definitions. The player automatically switches to the optimal definition based on the current network conditions, guaranteeing a smooth playback.
        </td>
 </tr>
 <tr>
        <td>
            UGSV platforms
        </td>
				<td>
				The bitrate is automatically switched based on the network conditions of the user's playback device to guarantee the playback smoothness first.
        </td>
 </tr>
  <tr>
        <td>
            Online education platforms
        </td>
				<td>
				The communication quality is improved based on network conditions, and multiple definitions are provided for a recorded video, so that the most appropriate definition can be automatically switched to based on the user's network conditions during playback. For important content, users can manually switch the definition. If the bitrate is too high, playback can be paused to let the video buffer.
        </td>
 </tr>
</table>

## Directions
For more information, see [Transcoding to Adaptive Bitrate Streaming](https://intl.cloud.tencent.com/document/product/266/33942).
