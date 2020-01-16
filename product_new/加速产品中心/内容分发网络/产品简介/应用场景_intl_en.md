This document describes the features and use cases of CDN.

## Scenario Overview
The table below lists the use cases of CDN. You can click to view the details.


<table  style="width:890">
<thead>
	<tr>
		<th scope="col" style="width: 100px;"> Use Case</th>
		<th scope="col">Description</th>
	</tr>
</thead>
<tbody>
	<tr>
	<td><a href = "#m1">Website Acceleration</a></td>
		<td >CDN provides accelerated delivery capabilities for static contents such as webpages, images, and small files in business scenarios like web portals, ecommerce, and UGC communities, significantly improving end users’ website experience. </td>
	</tr>
	<tr>
		<td><a href = "#m2">Download Acceleration</a></td>
		<td >CDN can stably and reliably accelerate downloads of game, app, or ROM installation packages. </td>
	</tr>
	<tr>
		<td><a href = "#m3">Audio/Video Acceleration</a></td>
		<td>Supported by Tencent's profound experience in online video operation, CDN can sustain massive volumes of concurrent requests for online audio and video playback during peak hours, effectively ensuring high service availability and media transfer speed while providing a stable, smooth and enriched viewing experience. </td>
	</tr>
	<tr>
		<td><a href = "#m4">ECDN</a></td>
		<td >Enterprise Content Delivery Network (ECDN) is a standalone product of Tencent Cloud for one-stop acceleration of dynamic or dynamic-static resources. It can automatically identify dynamic and static resources while implementing simultaneous acceleration for all types of internal resources on one single platform. </td>
	</tr>
	<tr>
		<td><a href = "#m5">SCDN</a></td>
		<td >In addition to all the acceleration benefits of CDN, Secure Content Delivery Network (SCDN) also features enhanced network security protection against high-traffic DDoS and CC attacks while supporting integration with Web Application Firewall (WAF). Security protection can be quickly enabled in CDN. </td>
	</tr>
</tbody>
</table>

## Scenario Description
<span ID = "m1"></span>
### Website Acceleration
Website acceleration is suitable for all types of websites such as web portals, ecommerce platforms, and UGC communities. CDN can cache and accelerate the delivery of static contents on your website such as images, HTML, CSS, and JavaScript files. To accelerate access to dynamic contents such as .asp, .jsp, .php, .cgi, and .perl files as well as API and database requests, use [ECDN](https://intl.cloud.tencent.com/product/dsa).

CDN provides powerful static content delivery capabilities, significantly speeding up page loading and offering a smooth and fast browsing experience for geographically dispersed end users. During service peaks with a large number of concurrent users, it can alleviate the pressure on origin servers to ensure stable and smooth access to services and webpages.
![](https://main.qcloudimg.com/raw/c9d1c4da99eabde91c5c63a10bf83d46.jpg)


<span ID = "m2"></span>
### Download Acceleration
Download acceleration is suitable for speeding up the download of various files such as game, app, and ROM installation packages

Supported by the massive amounts of elastic bandwidth resources of Tencent Cloud, CDN can endure large-scale traffic and speed up the download of large files, ensuring service stability and providing an efficient download experience for all end users.
![](https://main.qcloudimg.com/raw/d87bc25ccad9a04e936b6ee6ecca653f.jpg)


<span ID = "m3"></span>
### Audio/Video acceleration
Audio/video acceleration is suitable for different types of audio/video on-demand websites and applications such as audio/video apps, online audio/video platforms, and IPTV. With enhanced content delivery capabilities and supported by Tencent's profound experience in online video operation, Tencent Cloud CDN can effectively ensure smooth audio/video playback for all end users during peak hours with massive volumes of concurrent requests.
![](https://main.qcloudimg.com/raw/b492585e2b1c6840834c32f7303b7b53.jpg)


<span ID = "m4"></span>
### ECDN
[Enterprise Content Delivery Network (ECDN)](https://intl.cloud.tencent.com/product/dsa) is suitable for websites and applications with a mix of dynamic and static resources, or with many requests for dynamic resources such as .asp, .jsp, .php, .cgi, and .perl files as well as API and database requests.

By integrating static edge caching with dynamic origin-pull route optimization, intelligently scheduling requests to the optimal service nodes, automatically identifying static and dynamic resources, and utilizing Tencent's proprietary optimal route calculation algorithm and TCP optimization technology, ECDN, currently a standalone product, can provide end users with a high-performance and one-stop acceleration experience.
![](https://main.qcloudimg.com/raw/7546f16ca821a265837bbfb080de255e.jpg)


<span ID = "m5"></span>
### SCDN
**Secure Content Delivery Network (SCDN)** is suitable for scenarios that integrate high-speed delivery of static and dynamic contents with security protection. It is ideal for industries that require fast content delivery and high network security, such as gaming, internet finance, ecommerce, and government portals. In addition to all the acceleration benefits of CDN, SCDN also features enhanced network security protection against high-traffic DDoS and CC attacks while supporting integration with Web Application Firewall (WAF). Security protection can be quickly enabled in CDN.

SCDN is built upon CDN and you do not need to re-do DNS configuration. Network security protection can be quickly enabled for domain names accelerated by CDN.
![](https://main.qcloudimg.com/raw/d2a1b1f002aefc746fa5ff54efdbd9a8.jpg)



