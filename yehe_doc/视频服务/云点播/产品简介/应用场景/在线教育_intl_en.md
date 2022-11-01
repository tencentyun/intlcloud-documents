## Use case
Online education platforms allow students and teachers to attend classes and communicate over the network. These platforms generally have a large number of audio/video teaching resources, most of which are recorded and uploaded by registered teachers. Online education generally involves the following core needs:

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
            Playback on various platforms
        </td>
				<td>
				Students use different many different devices and platforms, including web and mobile clients, and need to be able to watch paid videos on their devices.
        </td>
	</tr>
	<tr>
        <td>
            Smart subtitling
        </td>
				<td>
				As teachers have different accents and speech rates, and students have different comprehension levels, subtitles need to be added to teaching videos to facilitate the study of all students. However, teaching videos are long, and manual subtitling is inefficient.
        </td>
	</tr>
 <tr>
        <td>
           Copyright protection
        </td>
				<td>
Educational content usually requires dedicated places, professional equipment, and expert teachers, all of which make production costly. As such, teaching videos become important digital assets of the platform, and their copyrights needs to be effectively protected to prevent them from being leaked. 
	</tr>
	<tr>
        <td>
            Time shifting
        </td>
				<td>
				Students entering the live classroom may not be able to understand the context of the current teaching content and need to watch the content from an earlier time point to get the context.
        </td>
	</tr>
	<tr>
        <td>
            Psuedo-live streaming
        </td>
				<td>
				The platform needs to be able to live stream pre-recorded courses at a specified time, so as to encourage students and parents to pay more attention to the courses while reducing the live streaming costs (costs of places, equipment, and teachers) and risks (the recorded video content can be moderated in advance).
        </td>
	</tr>
	<tr>
        <td>
            Smart moderation
        </td>
				<td>
				Improper words, behaviors, and images in teaching videos may cause a bad impact on students and bring legal risks and negative opinions to the platform. Therefore, the video content needs to be moderated. However, most teaching videos are long videos, for which traditional manual moderation tends to miss non-compliant content and involves a lengthy process with a low moderation quality and efficiency.
        </td>
	</tr>
	<tr>
        <td>
            Media playback blocking
        </td>
				<td>
				As teaching videos are mainly oriented to minors, non-compliant video content can be very sensitive. However, such content might fail to be detected due to insufficient performance of the moderation service, and platforms may only find out afterwards that non-compliant was released and needs to be quickly blocked.
        </td>
	</tr>
	<tr>
        <td>
            Reduced costs
        </td>
				<td>
				Students demand a high video playback smoothness and definition. However, large numbers of HD videos incur high storage costs.
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
           Playback on various platforms
        </td>
				<td>
				<li><a href="https://intl.cloud.tencent.com/document/product/266/49263" title="Adaptive bitrate streaming" target="_blank">Adaptive bitrate streaming</a></br>Multiple bitstreams are output for one input file, so as to meet the students' needs for playback under different network conditions.</li>
				<li><a href="https://intl.cloud.tencent.com/document/product/266/49265" title="Player SDK" target="_blank">Player SDK</a></br>The Player SDK is available for iOS, Android, web (Flash and HTML5), and Flutter, so as to meet students' needs for high-quality video playback on different devices. It also supports playback quality statistics collection.</li>
        </td>
	</tr>
	 <tr>
        <td>
           Smart subtitling
        </td>
				<td>
				<li><a href="https://intl.cloud.tencent.com/document/product/266/49267" title="Smart subtitling" target="_blank">Smart subtitling</a></br>VOD efficiently and accurately recognizes the audio content and automatically generates subtitle files in a standard format, helping students better study the courses.</li>
        </td>
	</tr>
	<tr>
        <td>
            Copyright protection
        </td>
				<td>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49274" target="_blank">Hotlink protection</a></br>The hotlink protection feature of VOD can prevent hotlinking based on referer and key.
				</li>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49275" title="Encryption and DRM" target="_blank">Encryption and DRM</a></br>VOD supports both HLS private encryption and commercial-grade DRM to effectively prevent various cracking behaviors and safeguard copyrighted media.
				</li>
        </td>
	</tr>
	<tr>
        <td>
            Time shifting
        </td>
				<td>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49279" title="Time shifting" target="_blank">Time shifting</a></br>VOD allows students to watch the content from an earlier time point during live streaming to better understand the context and to switch back to the latest live content at any time.
				</li>
        </td>
	</tr>
	<tr>
        <td>
            Psuedo-live streaming
        </td>
				<td>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49281" title="VOD-to-CSS" target="_blank">VOD-to-CSS</a></br>VOD-to-CSS can reduce the live streaming costs and improve the student focus and the learning effect.
				</li>
        </td>
	</tr>
	<tr>
        <td>
            Smart moderation
        </td>
				<td>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49271" title="Smart moderation" target="_blank">Smart moderation</a></br>VOD intelligently detects non-compliant content in teaching videos, so as to guarantee a healthy study experience and avoid the security risks of the platform content.
				</li>
        </td>
	</tr>
	<tr>
        <td>
            Media playback blocking
        </td>
				<td>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49272" title="Media playback blocking" target="_blank">Media playback blocking</a></br>The platform can quickly prohibit the playback of non-compliant videos to prevent them from being further spread.
				</li>
        </td>
	</tr>
	<tr>
        <td>
            Reduced costs
        </td>
				<td>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49251" title="Media deletion" target="_blank">Media deletion</a></br>Media resources can be partly deleted. Only LD videos will be retained for old videos, and HD videos will be deleted to reduce the storage costs. Media resources can be deleted automatically upon expiration.
				</li>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49252" title="Smart cold storage" target="_blank">Smart cold storage</a></br>You can configure smart cold storage policies in various dimensions, such as creation time, file category, and views, so as to automatically transition media resources meeting the conditions to a storage class at lower costs.
				</li>
        </td>
	</tr>
</table>
