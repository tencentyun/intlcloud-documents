## Use case
Short video platforms allow users to post and share their short videos with their friends and followers on social media. Short video services generally involve the following core needs:

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
            Quick video production and sharing
        </td>
				<td>
			Users record and share their lives in the form of a short video and involve themselves in video production, processing, upload, delivery, and playback. Therefore, allowing users to implement these operations quickly and easily will increase their involvement and facilitate the development of the social networking short video platform, which is one of the core needs of the platform.
        </td>
	</tr>
	<tr>
        <td>
            Smart media
        </td>
				<td>
			 On short video platforms, users want to be able to follow other interesting users and groups. The platform has to make personalized video recommendations based on the people, events, and objects that are followed by users. For videos that contain speech, the speakers may come from different regions and speak with different accents, which may be difficult to understand for viewers in other regions, so platforms must also need to support subtitles so content can be spread and enjoyed by everyone.
        </td>
	</tr>
	<tr>
        <td>
            Compliance control
        </td>
				<td>
			 Short video platforms are typically comprised of user-generated content (UGC), and often contain non-compliant content such as eroticism. As short videos are generated quickly and in large quantities, with diverse content scenarios, traditional manual moderation is inefficient and tends to leave omissions, making it hard to effectively moderate all videos. Smart moderation can quickly recognize harmful content, so as to guarantee the business interests and compliance of the platform and reduce the user operations costs. Therefore, effective compliance control is also one of the core needs of the social networking short video platform.
        </td>
	</tr>
	<tr>
        <td>
            Smart switch between multiple definitions
        </td>
				<td>
			Short videos are generally only several minutes long, and they are mostly played back on mobile clients, so smooth playback is one of the primary needs of viewers. The image quality needs to be improved as much as possible while guaranteeing the smoothness, so as to maximize the viewing experience.
        </td>
	</tr>
	<tr>
        <td>
            High image quality at a low bitrate
        </td>
				<td>
				High numbers of HD short videos incur high storage costs and playback traffic costs to the platform, and they also require a higher bandwidth and more traffic to be played back by users. Therefore, ensuring a high image quality at a low bitrate is another core need of short video platforms.
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
           Quick video production and sharing
        </td>
				<td>
					<li><a href="https://intl.cloud.tencent.com/document/product/266/6965" title="UGSV SDK" target="_blank">UGSV SDK</a></br>Based on Tencent Cloud's powerful VOD capabilities in upload, storage, transcoding, and delivery, VOD provides the client SDK that features capturing, editing, splicing, special effect creating, sharing, and playback of audio and video clips, allowing you to focus on your core business and implement your mobile short video application with speed and ease. Short video app users can quickly produce, process, and release their short videos.</li>
        </td>
	</tr>
	<tr>
        <td>
            Smart media
        </td>
				<td>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49268" target="_blank">Labeling and categorization</a></br>VOD intelligently labels and categorizes short video content uploaded by community users and collects the short video click rate to implement more accurate short video content recommendations.
				</li>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49269" target="_blank">Face recognition</a></br>VOD recognizes faces in the video content to recommend other short videos where the relevant persons appear.
				</li>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49267" target="_blank">Smart subtitling</a></br>VOD automatically generates a subtitles for the speech in a short video, so so viewers can clearly understand speakers with different accents and speech rates and can better remember the video content.
				</li>
        </td>
	</tr>
	<tr>
        <td>
            Compliance control
        </td>
				<td>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49271" target="_blank">Smart moderation</a></br>The smart moderation feature of VOD offers smart recognition capabilities with a high accuracy and recall rate. It recognizes non-compliant video segments quickly and effectively, which saves a lot of manpower for manual moderation, and is suitable for scenarios with a high number of short videos and diverse content, so as to protect the platform security and reduce the operational costs.
				</li>
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
            High image quality at a low bitrate
        </td>
				<td>
				<li><a href="https://intl.cloud.tencent.com/document/product/266/49255" title="TSC transcoding" target="_blank">TSC transcoding</a></br>For diverse and complex scenarios of short videos, VOD uses smart dynamic encoding technology and the precise bitrate control model to deliver a high definition at a low bitrate. In this way, users can enjoy a smooth and clear playback experience, and the platform can save a large proportion of the storage and traffic costs.</li>
        </td>
	</tr>
</table>
