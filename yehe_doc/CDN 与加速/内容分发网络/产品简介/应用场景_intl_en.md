## Use Cases
The table below lists the use cases of CDN. You can click to view the details.

<table  style="width:890">
<thead>
	<tr>
		<th scope="col" style="width: 100px;">Use Case</th>
		<th scope="col">Description</th>
	</tr>
</thead>
<tbody>
	<tr>
	<td><a href = "#m1">Website acceleration</a></td>
		<td >CDN provides accelerated delivery capabilities for static contents such as webpages, images, and small files in business scenarios like web portals, ecommerce, and UGC communities, significantly improving user experience. </td>
	</tr>
	<tr>
		<td><a href = "#m2">Download acceleration</a></td>
		<td >CDN provides stable and high-quality download acceleration for game, app, or ROM installation packages.</td>
	</tr>
	<tr>
		<td><a href = "#m3">Audio/Video acceleration</a></td>
		<td>Supported by Tencent's profound experience in online video operation, CDN can sustain massive volumes of concurrent requests for online audio and video playback during peak hours, effectively ensuring high service availability and media transfer speed while providing a stable, smooth and enriched viewing experience. </td>
	</tr>
	<tr>
		<td><a href = "#m4">ECDN</a></td>
		<td >Enterprise Content Delivery Network (ECDN) is a standalone product of Tencent Cloud for one-stop acceleration of dynamic or dynamic-static resources. It can automatically identify dynamic and static resources while implementing simultaneous acceleration for all types of resources on one single platform. </td>
	</tr>
	<tr>
		<td><a href = "#m5">SCDN</a></td>
		<td >Tencent Cloud SCDN provides powerful security protection capabilities in addition to all acceleration strengths of CDN. It can defend against high-traffic DDoS attacks and large-scale CC attacks and provide WAF against website intrusions. You can quickly connect to and enable SCDN in CDN.</td>
	</tr>
</tbody>
</table>
## Use Cases Description
<span ID = "m1"></span>
### Website acceleration
Website acceleration suitable for all types of websites, such as web portals, ecommerce platforms, and UGC communities. CDN can cache and accelerate the delivery of static contents on your websites. To accelerate dynamic contents, use [ECDN](https://intl.cloud.tencent.com/product/ecdn).

<blockquote class="d-mod-explain">
<div class="d-mod-title d-explain-title">
<i class="d-icon-explain"></i>What are static and dynamic contents?
</div>
<p></p>	
<ul>	
<li>Static content refers to content that stays the same when requested. <br>Examples: .html, .css, and .js files, images, videos, software installation packages, APK files, and compressed files.</li>
<li>Dynamic content refers to content that varies when requested. <br>Examples: APIs and .jsp, .asp, .php, .perl, and .cgi files.</li>
</ul>	
</blockquote>
CDN provides powerful static content delivery capabilities, significantly speeding up page loading and offering a smooth and fast browsing experience for geographically dispersed end users. During service peaks when there are a large number of concurrent users, it can alleviate the pressure on origin servers to ensure stable and smooth access to services and webpages.
![](https://main.qcloudimg.com/raw/c2291b131ce33d1eb39ec35167453437.png)


<span ID = "m2"></span>
### Download acceleration
Download acceleration is suitable for speeding up the download of various files such as game, app, and ROM installation packages

Backed by a massive amount of reserved elastic bandwidth, CDN can sustain traffic surges and speed up the download of large files, ensuring service stability and providing an efficient download experience for all end users.
![](https://main.qcloudimg.com/raw/ada400d5a04d58fb73662e6bc028232c.png)


<span ID = "m3"></span>
### Audio/Video acceleration
Audio/video acceleration is suitable for different types of audio/video on-demand websites and applications such as audio/video apps, online audio/video platforms, and IPTV. With enhanced content delivery capabilities and supported by Tencent's profound experience in online video operation, Tencent Cloud CDN can effectively ensure smooth audio/video playback for all end users during peak hours with massive volumes of concurrent requests.
![](https://main.qcloudimg.com/raw/0e852cfff1cd2f131f3ab1256a5b3a51.png)


<span ID = "m4"></span>
### ECDN
[ECDN](https://intl.cloud.tencent.com/product/ecdn) is suitable for websites and applications with dynamic/static hybrid resources or a large number of dynamic resources, such as .asp, .jsp, .php, .cgi., and .perl files, APIs, and database interaction requests.

By integrating static edge caching with dynamic origin-pull route optimization, intelligently scheduling requests to the optimal service nodes, automatically identifying static and dynamic resources, and utilizing Tencent's proprietary optimal route calculation algorithm and TCP optimization technology, ECDN, currently a standalone product, can provide end users with a high-performance and one-stop acceleration experience.
![](https://main.qcloudimg.com/raw/a6f7d54e98720a3d4a18d673fc1f9b4c.png)

<span ID = "m5"></span>

### SCDN
SCDN By integrating static edge caching with dynamic origin-pull route optimization, intelligently scheduling requests to the optimal service nodes, automatically identifying static and dynamic resources, and utilizing Tencent's proprietary optimal route calculation algorithm and TCP optimization technology, ECDN, currently a standalone product, can provide end users with a high-performance and one-stop acceleration experience.
SCDN is built upon CDN and you do not need to re-do DNS configuration. Network security protection can be quickly enabled for domain names accelerated by CDN. 
![](https://main.qcloudimg.com/raw/164d28b237eb5dbe05a57b631d98616e.png)



​	