## Use case
Radio, TV, and OTT media services are based on the streaming media services provided by the TV in a user’s home. This use case generally involves the following core needs:
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
            High-resolution video
        </td>
				<td>
			As radio, TV, and OTT platform users generally play back the media on large-screen devices like smart TVs, subtle and vivid details of the video image are required first. Therefore, UHD video playback is the most basic need.
        </td>
	</tr>
	<tr>
        <td>
            Smart switch between multiple definitions
        </td>
				<td>
			 Radio, TV, and OTT platforms have a large user base with widely different network conditions. To adapt to different network environments, the platform generally needs to prepare multiple resolutions for a video resource, so that the device can automatically select and play back the media stream at the most appropriate bitrate based on the network conditions.
        </td>
	</tr>
	<tr>
        <td>
            Copyright Protection
        </td>
				<td>
			 Radio, TV, and OTT platforms have diverse media resource content, including movies, sports events, animations, and variety shows. As large-screen consumption continues increasing, such content also becomes more prone to piracy. Therefore, effective copyright protection measures are needed to minimize piracy.
        </td>
	</tr>
	<tr>
        <td>
            Smart media moderation
        </td>
				<td>
			As radio, TV, and OTT platforms have a wide audience. To prevent severe impact and huge losses due to the release of non-compliant content, efficient moderation capabilities are required. Generally, most of the videos on such platforms have a long duration, which makes the manual moderation process lengthy, inefficient, and error-prone. If machine-based smart moderation is used, a large number of compliant videos can be filtered out first, which greatly reduces the manual moderation costs.
        </td>
	</tr>
	<tr>
        <td>
            Media playback blocking 
        </td>
				<td>
				Media platforms need to be able to quickly block the playback of certain videos if non-compliant content is missed during moderation.
        </td>
	</tr>
		<tr>
        <td>
            Psuedo-live streaming
        </td>
				<td>
				Pseudo-live streaming (broadcasting a pre-recorded video to achieve a similar effect to live streaming) widely exists on radio, TV, and OTT platforms. TV shows, variety shows, and interview programs are recorded and edited in advance, and their URLs are placed on the preview page, so that the target audience can favorite the page and URLs in advance and watch them at the scheduled playback time.
        </td>
	</tr>
	<tr>
        <td>
            Efficient content cataloging
        </td>
				<td>
				The radio and TV industry has high numbers of videos, most of which are long videos. All of the content needs to be cataloged, but traditional manual cataloging is inefficient.
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
            High-resolution video
        </td>
				<td>
					<li><a href="https://intl.cloud.tencent.com/document/product/266/49254" title="Audio/Video transcoding" target="_blank">Audio/Video transcoding</a></br>VOD supports transcoding to high resolutions such as 2K, 4K, and 8K as well as HDR image quality, so as to meet the requirements of large-screen devices such as OTT TV for UHD and HD content.</li>
        </td>
	</tr>
	<tr>
        <td>
            Smart switch between multiple definitions
        </td>
				<td>
					<li><a href="https://intl.cloud.tencent.com/document/product/266/49263" title="Adaptive bitrate streaming" target="_blank">Adaptive bitrate streaming</a></br>Multiple bitstreams are output for one input file, so as to meet the playback needs of different devices in complex family network environments.</li>
        </td>
	</tr>
	 <tr>
        <td>
            Copyright Protection
        </td>
				<td>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49274" title="Hotlink protection" target="_blank">Hotlink protection</a></br>The hotlink protection feature of VOD can prevent hotlinking based on referer and key.
				</li>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49275" title="Encryption and DRM" target="_blank">Encryption and DRM</a></br>VOD supports both HLS private encryption and commercial-grade DRM to effectively prevent various cracking behaviors and safeguard copyrighted media.
				</li>
        </td>
	</tr>
	<tr>
        <td>
            Smart media moderation
        </td>
				<td>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49271" title="Smart moderation" target="_blank">Smart moderation</a></br>The smart moderation feature of VOD continuously performs training and modeling on massive amounts of non-compliant data to achieve industry-leading recognition accuracy and recall rate, guaranteeing the media content security of the radio, TV, and OTT platforms comprehensively and effectively.
				</li>
        </td>
	</tr>
	<tr>
        <td>
            Media playback blocking
        </td>
				<td>
					<li><a href="https://intl.cloud.tencent.com/document/product/266/49272" title="Media playback blocking" target="_blank">Media playback blocking</a></br>Through media playback blocking, platforms can immediately block non-compliant media content to prevent it from being further spread, so as to reduce the security risks to the platform and the damage to the brand image.</li>
        </td>
	</tr>
	<tr>
        <td>
            Psuedo-live streaming
        </td>
				<td>
					<li><a href="https://intl.cloud.tencent.com/document/product/266/49281" title="VOD-to-CSS" target="_blank">VOD-to-CSS</a></br>Based on the access control feature of VOD, VOD files can be played back as a pseudo-live stream. Radio, TV, and OTT platforms can quickly deliver VOD files as a pseudo-live stream at low costs, fully utilizing high-value recording content to attract more traffic to the platform.</li>
        </td>
	</tr>
	<tr>
        <td>
            Efficient media cataloging
        </td>
				<td>
					<li><a href="https://intl.cloud.tencent.com/document/product/266/49268" title="Labeling and categorization" target="_blank">Labeling and categorization</a></br>The labeling and categorization feature of VOD efficiently add labels and categories to massive amounts of video content, which solves the problem of low efficiency of manual cataloging. Based on the recognized label and category information, videos can be quickly archived, labeled, and searched for.</li>
        </td>
	</tr>
</table>
