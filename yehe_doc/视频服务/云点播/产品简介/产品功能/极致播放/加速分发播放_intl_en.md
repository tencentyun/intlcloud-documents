## Overview
VOD has over 2,800 CDN cache nodes around the globe to enable global users to access nearby nodes to get the media content they want. This makes downloading media content faster and smoother by avoiding problems such as network instability and high access delay due to cross-ISP, cross-region, and cross-border communication. VOD provides a built-in default domain name. If you do not have a domain name, the default domain name can be used to deliver resources based on the nearby region. In addition, VOD also supports custom domain name management, purge and prefetch, and CDN usage statistics.

<table>
    <tr>
        <th style="width:150px">
            Feature               
        </th>
				<th>
           Description
        </th>
    </tr>
 <tr>
        <td>
            Domain name management
        </td>
				<td>
            <li>Supports the use of Tencent Cloud domain names or custom playback domain names.</li>
						<li>Configure different hotlink protection and release rules for different playback domain names.</li>
        </td>
 </tr>
  <tr>
        <td>
            Purge and prefetch
        </td>
				<td>
            <li>Supports CDN cache purge through a VOD media asset ID or URL. Once you perform a cache purge on a resource, the system will delete the existing cache of the resource from the CDN nodes across the entire network. When a user request arrives at a node, the node will pull the resource from the origin, return the request, and cache the resource, ensuring that the user gets the latest resource.</li>
						<li>Supports CDN cache prefetch through a VOD media asset ID or URL. When a resource is prefetched, it will be cached in advance to all the CDN nodes across the entire network. When a user request arrives at a node, the resource can be directly obtained from the node, which shortens the response time.</li>
        </td>
 </tr>
 <tr>
        <td>
            CDN usage statistics
        </td>
				<td>
				<li>Provides statistics for CDN, allowing you to keep track of traffic, bandwidth, and clicks by time, region, and ISP.</li>
				<li>View statistics for media files, including playback count and traffic for each video.</li>
				<li>Download the CDN logs of the access status of the connected domain name.</li>
        </td>
 </tr>
</table>

## Use cases
The accelerated delivery and playback feature of VOD is suitable for almost all online scenarios in which images or audio/video content need to be displayed, such as social media, ecommerce, video platforms, news websites, and forums. The globally deployed CDN cache nodes enable VOD to deliver a high-quality media content access service even in a complicated network environment.

<table>
    <tr>
        <th style="width:150px">
            Scenario               
        </th>
				<th>
           Description
        </th>
    </tr>
	 <tr>
        <td>
            Social media platforms
        </td>
				<td>
				Users may be located in different regions or countries and use different ISPs with different levels of network quality. CDN uses various optimization policies such as dynamic acceleration policies to automatically find and apply the optimal linkage for users during video playback, so as to deliver a smooth playback experience.
        </td>
 </tr>
 <tr>
        <td>
            Ecommerce platforms
        </td>
				<td>
            Merchants upload product images, audios, and videos for customers, and customers upload their own images, audios, and videos for product reviews. Resource delivery is accelerated through CDN to enable ultra fast loading of images, audios, and videos, effectively improving the user access and shopping experience.
        </td>
 </tr>
 <tr>
        <td>
            Video platforms
        </td>
				<td>
           Video platforms contain many long videos, which have a large file size and high requirements for the network stability. Video playback based on CDN allows users to enjoy a stable and smooth viewing experience even under poor network conditions.
        </td>
 </tr>
  <tr>
        <td>
            News website
        </td>
				<td>
            When trending news quickly reaches a high number of users, an instant traffic surge will occur. If users directly access the origin to view news images, audios, or videos, the origin may crash, losing the public attention. The media content can be hosted in VOD and pushed to global cache nodes through CDN, so that users can get the media content quickly and enjoy a smooth browsing experience.
        </td>
 </tr>
</table>

## Directions
For more information on domain name management, see the following:
- [Customizing Domain Names](https://intl.cloud.tencent.com/document/product/266/35572)
- [Managing Domain Names](https://intl.cloud.tencent.com/document/product/266/14057)
- [Configuring CNAME](https://intl.cloud.tencent.com/document/product/266/42076)
- [Default Distribution Configuration](https://intl.cloud.tencent.com/document/product/266/35768)

For more information on purge and prefetch, see:
- [Purge and Prefetch](https://intl.cloud.tencent.com/document/product/266/33899)

For more information on usage statistics analysis, see:
- [Usage Statistics](https://intl.cloud.tencent.com/document/product/266/30421)
- [Data Analysis](https://intl.cloud.tencent.com/document/product/266/30422)
- [Downloading Logs](https://intl.cloud.tencent.com/document/product/266/7983)
