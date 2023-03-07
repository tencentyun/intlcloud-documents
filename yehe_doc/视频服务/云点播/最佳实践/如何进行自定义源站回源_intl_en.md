## Overview

You can configure a third-party origin server for your domain in VOD to pull media files from the origin server and distribute the media via VOD. This multi-cloud media distribution solution is enabled by VOD’s CDN capability. This document shows you how to configure and use an origin server with VOD.

## Use cases

- Your media assets are stored with a third-party cloud vendor, and **the cost of migrating them is high**. You can use VOD’s custom origin server feature to deliver your content without migrating your media assets.
- You have **high requirements on latency and stuttering** and your existing service provider is unable to meet them. You can use VOD’s custom origin server feature to deliver smoother playback and improve your user experience.
- You need **more than one channel** to distribute your content to ensure the reliability and improve the disaster recovery capability of your business.


## Prerequisites

1. You have [signed up](https://intl.cloud.tencent.com/register?&s_url=https%3A%2F%2Fcloud.tencent.com%2F) for a Tencent Cloud account, completed identity verification, and [logged in](https://intl.cloud.tencent.com/login?s_url=https%3A%2F%2Fcloud.tencent.com%2F).
2. You have [activated](https://console.cloud.tencent.com/vod/overview) VOD.



## Supported Origin Server Types

- **Self-owned origin servers**
- **Third-party storage services**

## Directions

### Step 1. Add a domain and configure origin server information

1. Log in to the VOD console and select **Distribution and Playback** > [Domain Name](https://console.cloud.tencent.com/vod/distribute-play/domain) on the left sidebar.
2. Select the **Custom origin server domains** tab at the top.
![](https://qcloudimg.tencent-cloud.cn/raw/e68e04641c3ad616450a70c72d5d3dcd.png)
3. Click **Add Domain** and enter a domain. For more information, see [Customizing Domain Names](https://intl.cloud.tencent.com/document/product/266/35572).
![](https://qcloudimg.tencent-cloud.cn/raw/0fbcc49821fd7eebffd9ad17a81072b1.png)
4. Enter your origin server information. Currently, **self-owned servers** and **third-party storage** are supported.     
![](https://qcloudimg.tencent-cloud.cn/raw/9ac80033d6fb055e299a2f355d0d1825.png) 

**Self-owned servers**
If you want to use your existing server as the origin server to distribute media files stored in it via VOD, configure as follows:
<table>
   <tr>
      <th width="0px" style="text-align:center">Item</td>
      <th width="0px" style="text-align:center">Description</td>
   </tr>
   <tr>
      <td>Origin server type</td>
      <td>Select <b>Self-owned server</b></td>
   </tr>
   <tr>
      <td>Protocol</td>
      <td>Select the protocol, which can be HTTP, HTTPS, or “Same as request”.</td>
   </tr>
	   <tr>
      <td>Origin server address</td>
      <td>You can enter multiple IP addresses (separate with commas) or one domain.</td>
   </tr>
	 <tr>
      <td>Host</td>
      <td>For self-owned origin servers, you can specify the host of a domain or IP address that VOD pulls from.<br> If you do not specify it, VOD will pull from the current domain.</td>
   </tr>
</table>

<dx-alert infotype="explain" title="">
- You cannot use your VOD default domain as the origin server address.
- If you select **Same as request**, HTTP will be used for HTTP requests, and HTTPS will be used for HTTPS requests (your origin server must support HTTPS).
- You can use a domain as the origin server address, but this domain cannot be the same as the domain you use for acceleration.
</dx-alert>
<b>Third-party storage</b><br>
If you want to distribute the media files you store in a third-party storage service via VOD’s CDN, configure as follows:              
<table>
   <tr>
      <th width="0px" style="text-align:center">Item</td>
      <th width="0px" style="text-align:center">Description</td>
   </tr>
   <tr>
      <td>Origin server type</td>
      <td>Select <b>Third-party storage</b></td>
   </tr>
   <tr>
      <td>Third-party storage</td>
      <td>Currently, Alibaba Cloud OSS and AWS S3 are supported.</td>
   </tr>
	   <tr>
	<td>Protocol</td>
	  <td>HTTP or HTTPS</td>
   </tr>
	 <tr>
      <td>Origin server address</td>
      <td>Enter a valid bucket address (cannot contain “http://” or http:// headers).</td>
   </tr>
</table>
<img src="https://qcloudimg.tencent-cloud.cn/raw/f5ca4759794c94ffba9f6a960b9a8641.png" /><br>
If you use a private bucket as the origin server, you need to enter a valid access ID and key to authorize VOD to access the bucket.
<img src="https://qcloudimg.tencent-cloud.cn/raw/66864ace26867520f76172f2901ad138.png" />

## Step 2. Configure CNAME for your domain

After you add a custom domain in VOD, you need to add a CNAME record for it at your DNS provider before users can access your media files via the domain. For detailed directions, see [Configuring CNAME](https://intl.cloud.tencent.com/document/product/266/42076).

### Step 3. View and modify origin server information
1. Go to **Domain Name**, select the **Custom origin server domains** tab, find the domain you added, and click **Set**.
![](https://qcloudimg.tencent-cloud.cn/raw/3522690fd01bd3c0f90eb1065dc87965.png)
2. Click **Basic Configuration** to view or modify the origin server settings of the domain.
![](https://qcloudimg.tencent-cloud.cn/raw/bb04aa08590e9f88680c29eb19a502b9.png)

After completing the above steps, you will be able to distribute media files to end users from a self-owned server or third-party storage service via VOD’s CDN. The process is as follows:

1. After you complete the above settings for a custom domain (for example `test.com`), when an end user opens the address of a media file under the domain (for example `http://www.test.com/test.mp4`) in a browser, a request will be sent to the local DNS resolver.
2. Because a CNAME record (`www.test.com.cdn.dnsv1.com`) has been added for the domain, the request will be referred to Tencent’s proprietary load balancing system Global Server Load Balance (GSLB).
3. GSLB will return a list of IP addresses to the local DNS resolver.
4. The user gets the IP address of the optimal node to access the media file.
5. The end user sends a request to the IP address to visit the media file `http://www.test.com/test.mp4`.
6. If the `test.mp4` file has been cached in the CDN node, the file will be returned to the user. If not, the node will request the file from the **origin server you configured**, cache the file, and return it to the user.

>? Using VOD’s origin server feature to distribute media files will incur **playback traffic costs** and **origin server traffic costs**. Playback traffic costs are charged by VOD. For details, see [Daily Pay-As-You-Go](https://intl.cloud.tencent.com/document/product/266/14666) and [Prepaid Packages](https://www.tencentcloud.com/document/product/266/52806#2.-.E6.B5.81.E9.87.8F.E8.B5.84.E6.BA.90.E5.8C.85). Origin server traffic costs are charged by your origin server.