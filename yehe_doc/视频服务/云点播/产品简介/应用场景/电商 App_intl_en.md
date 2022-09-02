## Use case
Ecommerce apps are online transaction platforms where enterprises and individuals can market and sell their products. Sellers typically produce and upload product images and videos to better showcase their products. Buyers can also upload images and videos to share feedback about their shopping experience or write product reviews. Ecommerce apps generally involve the following core needs:
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
            Smart switch between multiple definitions
        </td>
				<td>
			 When playing a video, the optimal video definition needs to be selected intelligently based on changes in the user's network environment to ensure a smooth playback experience.
        </td>
	</tr>
		<tr>
        <td>
            Screencapturing features
        </td>
				<td>
				The platform needs to provide diverse ways to showcase products so as to attract more sellers. For example, the platform needs to allow sellers to generate static thumbnails to use on the homepage and generate animated thumbnails for video previews, so as to display the product content more quickly and directly.
        </td>
	</tr>
	<tr>
        <td>
            High image quality at a low bitrate
        </td>
				<td>
				Sellers want their videos to be available in HD and loaded quickly so their product videos can attract more consumers to browse and purchase the products.
        </td>
	</tr>
 <tr>
        <td>
           High-quality upload from client
        </td>
				<td>
Consumers may use various mobile device models and want a fast and stable video upload even under poor network conditions. A poor upload experience may cause consumers to give up uploading and form negative opinions about the platform, which damages the platform’s image.
        </td>
	</tr>
	<tr>
        <td>
            Time shifting
        </td>
				<td>
				Consumers who enter a live shopping room during live streaming and miss previous information about a product may want to watch from an earlier time point to get more product information.
        </td>
	</tr>
	<tr>
        <td>
            Smart product recommendations
        </td>
				<td>
				The platform needs to intelligently analyze click counts for product videos and make recommendations to users based on the categories and tags of the products that interest them, so as to increase the purchase rates.
        </td>
	</tr>
	<tr>
        <td>
            Reduced costs
        </td>
				<td>
				Many live shopping video recordings need to be retained only for audit by applicable authorities, some of which will never or seldom be played back but will incur a large proportion of the storage costs.
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
           Smart switch between multiple definitions
        </td>
				<td>
				<li><a href="https://intl.cloud.tencent.com/document/product/266/49263" title="Adaptive bitrate streaming" target="_blank">Adaptive bitrate streaming</a></br>Multiple bitstreams are output for one input file, which allows for smooth playback under various changing network conditions.</li>
        </td>
	</tr>
 <tr>
        <td>
           Screencapturing features
        </td>
				<td>
				<li><a href="https://intl.cloud.tencent.com/document/product/266/49257" title="Video screencapturing" target="_blank">Video screencapturing</a></br>Sellers can perform various screencapturing operations, including generating point-in-time screenshots, sampled screenshots, thumbnails, image sprites, and animated images, so they can showcase products in diverse ways.</li>
        </td>
	</tr>
	<tr>
        <td>
            High image quality at a low bitrate
        </td>
				<td>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49255" title="TSC transcoding" target="_blank">TSC transcoding</a></br>VOD’s  TSC transcoding feature ensures that consumers can enjoy a smooth and clear video playback experience.
				</li>
        </td>
	</tr>
	<tr>
        <td>
            High-quality upload from client
        </td>
				<td>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49247" title="Multi-end upload" target="_blank">Multi-end upload</a></br>VOD supports upload from clients for different platforms such as Android, iOS, and web.
				</li>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49149" title="Upload acceleration" target="_blank">Upload acceleration</a></br>VOD uses a series of technical methods such as scheduling optimization to deliver an industry-leading upload quality (with an upload success rate of over 99.5%). The excellent upload experience encourages consumers to share their purchase experiences and improves the platform’s reputation.
				</li>
        </td>
	</tr>
	<tr>
        <td>
            Time shifting
        </td>
				<td>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49279" title="Time shifting" target="_blank">Time shifting</a></br>When an ecommerce live stream is ongoing, consumers entering the live room can manually drag the progress bar to watch the content at an earlier time point, so as to get more information about the products.
				</li>
        </td>
	</tr>
	<tr>
        <td>
            Smart product recommendations
        </td>
				<td>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49268" title="Labeling and categorization" target="_blank">Labeling and categorization</a></br>The labeling and categorization feature of VOD can automatically label and categorize videos, so that the platform can recommend relevant products to consumers based on their product video clicks and playback completion rates.
				</li>
        </td>
	</tr>
	<tr>
        <td>
            Reduced costs
        </td>
				<td>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49252" title="Smart cold storage" target="_blank">Smart cold storage</a></br>VOD allows you to configure smart cold storage policies for live video recordings that are seldom played back and retained mainly for auditing purposes, which effectively helps you reduce the cost of storing those required videos.
				</li>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49251" title="Media deletion" target="_blank">Media deletion</a></br>You can configure an expiration time for recording files that are stored only for auditing purposes. Such media files will be automatically deleted upon expiration, which effectively helps you reduce storage costs.
				</li>
        </td>
	</tr>
</table>
