## Use case
Live streaming apps allow hosts to broadcast, deliver commentary, or perform for viewers over the network in real time. Since 2016, the live streaming industry has grown enormously, and more new forms have developed from entertainment (such as live shows and game live streaming) to live classes, live shopping, and live Q&A. Live streaming apps generally have the following core needs:
<table>
    <tr>
        <th>
            Core Need              
        </th>
				<th>
           Description
        </th>
    </tr>
		<tr>
        <td>
            Live recording
        </td>
				<td>
			 Regulatory authorities require that the live videos be retained for a certain period of time for audit. Operators also need to record high-value live content to be viewed later, such as live concerts and live teaching courses.
        </td>
	</tr>
	<tr>
        <td>
            Time shifting
        </td>
				<td>
			 During game or sports event live streaming, new viewers entering the live stream want to be able to go back to an earlier part of the stream to better understand the context.
        </td>
	</tr>
	<tr>
        <td>
            Live stream editing
        </td>
				<td>
			 During live streaming, the host or the live streaming operator needs to be able to create video clips in real time so they can be quickly release to social media platforms, so as to attract more viewers.
        </td>
	</tr>
	<tr>
        <td>
            Psuedo-live streaming
        </td>
				<td>
			For high-value live content, the operator generally considers recording it for secondary editing and streaming it again at a later specified time, so as to attract more viewers. This is much cheaper than organizing a new live streaming event.
        </td>
	</tr>
	<tr>
        <td>
            High image quality at a low bitrate
        </td>
				<td>
				For content in which video images change quickly, such as game and sports event live streaming, the recorded video has a high bitrate and incurs high storage costs. In addition, users need a high network bandwidth for smooth playback. Therefore, to guarantee a high image quality at a low bitrate is good for both the platform and users.
        </td>
	</tr>
		<tr>
        <td>
            Screencapturing features
        </td>
				<td>
				After a live stream is recorded as a VOD video, the platform can perform various screencapturing operations on the VOD video. For example, it can take sampled screenshots for content moderation or generate an image sprite for video timestamping to help viewers quickly locate different time points in the video.
        </td>
	</tr>
	<tr>
        <td>
            Splicing and clipping
        </td>
				<td>
				When a live stream is interrupted multiple times, it generates multiple video files that need to be spliced together to get a complete live recording file. Editors also want to splice multiple live stream segments or recording file segments together to generate highlight videos.
        </td>
	</tr>
</table>

## Solutions
<table>
    <tr>
        <th>
            Core Need              
        </th>
				<th>
           Recommended VOD Feature
        </th>
    </tr>
		<tr>
        <td>
           Live recording
        </td>
				<td>
				<li><a href="78309" title="CSS recording" target="_blank">CSS recording</a></br>VOD records and stores the live content for regulatory audit. Valuable video recordings can be edited for secondary delivery.</li>
        </td>
	</tr>
	 <tr>
        <td>
           Time shifting
        </td>
				<td>
				<li><a href="https://intl.cloud.tencent.com/document/product/266/49279" title="Time shifting" target="_blank">Time shifting</a></br>VOD allows viewers to drag the progress bar to watch the content from an earlier time point during live streaming and to switch back to the latest live content at any time.</li>
        </td>
	</tr>
	<tr>
        <td>
           Live stream editing
        </td>
				<td>
				<li><a href="https://intl.cloud.tencent.com/document/product/266/49280" title="Live clipping" target="_blank">Live clipping</a></br>During live streaming, the host or the operator can clip out historical highlights to generate a video in real time and share it immediately or store it persistently.</li>
        </td>
	</tr>
 <tr>
        <td>
           Psuedo-live streaming
        </td>
				<td>
				<li><a href="https://intl.cloud.tencent.com/document/product/266/49281" title="VOD-to-CSS" target="_blank">VOD-to-CSS</a></br>After recording a high-value live stream, the operator edits it and delivers it as a pseudo-live stream to make viewers feel more engaged and attract more attention and clicks. In addition, this is much cheaper than organizing a real live streaming event.</li>
        </td>
	</tr>
	<tr>
        <td>
            High image quality at a low bitrate
        </td>
				<td>
					<li><a href="https://intl.cloud.tencent.com/document/product/266/49255" title="TCS transcoding" target="_blank">TCS transcoding</a></br>In scenarios where the bitrate is high and the image is complex, such as recording of game and sports event live streaming, VOD uses the smart dynamic encoding technology and the precise bitrate control model to maintain a high definition at a low bitrate, reducing the bandwidth costs by nearly 50% while guaranteeing the same subjective image quality.</li>
        </td>
	</tr>
	<tr>
        <td>
            Screencapturing features
        </td>
				<td>
					<li><a href="https://intl.cloud.tencent.com/document/product/266/49257" title="Video screencapturing" target="_blank">Video screencapturing</a></br>VOD allows you to generate point-in-time screenshots, sampled screenshots, thumbnails, image sprites, and animated images. The host or the operator can display the video content in various forms to improve the viewing experience.</li>
        </td>
	</tr>
	<tr>
        <td>
            Splicing and clipping
        </td>
				<td>
					<li><a href="https://intl.cloud.tencent.com/document/product/266/49259" title="Splicing and clipping" target="_blank">Splicing and clipping</a></br>When a live stream is interrupted, multiple video files may be generated when the stream is recorded to VOD. In this case, you can splice the video stream segments together to generate a complete VOD video. You can also splice multiple live stream segments or recording file segments to generate highlight videos.</li>
        </td>
	</tr>
</table>
