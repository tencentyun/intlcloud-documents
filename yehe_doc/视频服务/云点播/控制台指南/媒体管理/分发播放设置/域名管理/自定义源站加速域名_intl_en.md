## Overview

VOD allows you to distribute media stored in a self-owned origin server or third-party storage service via VOD’s CDN. To use this feature, you need to add a custom domain in VOD and configure origin server information such as the origin server type, protocol, and origin server address (you can only configure origin servers for custom domains).

## Directions
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod) and select **Application Management** on the left sidebar.
2. Select the target application.
3. By default, you will be directed to **Media Assets > Video/Audio Management > Uploaded**.
4. Select **Distribution and Playback** > [Domain Name](https://console.cloud.tencent.com/vod/distribute-play/domain) on the left sidebar.
5. Select the **Custom origin server domains** tab at the top.
![img](https://qcloudimg.tencent-cloud.cn/raw/f0536b39ee6156173e7cd27b3642f791.png)
6. Click **Add Domain** and complete the domain and origin server settings:
 - Domain settings
Enter your domain name and select the acceleration region. For detailed directions, see [Customizing Domain Names](https://intl.cloud.tencent.com/document/product/266/35572).
![](https://qcloudimg.tencent-cloud.cn/raw/ceb83e97ffdd3118c4890c13a68c6971.png)
 - Origin server settings
![](https://qcloudimg.tencent-cloud.cn/raw/43279ccef236c0211c4b996f8ff92fd6.png)

**Origin server type**
VOD supports two types of origin servers: self-owned servers and third-party storage services.
<table>
   <tr>
      <td >Self-owned server</td>
      <td >An existing server with stable performance. You can enter multiple IP addresses or one domain name.</td>
   </tr>
   <tr>
      <td>Third-party storage</td>
      <td>A non-Tencent Cloud third-party storage service. Currently, Alibaba Cloud OSS and AWS S3 are supported.</td>
   </tr>
</table>

**Protocol**
The protocol used when a CDN cache node pulls data from your origin server. HTTP and HTTPS are supported.
<table>
   <tr>
      <td>HTTP</td>
      <td>HTTP is used for both HTTP and HTTPS requests.</td>
   </tr>
   <tr>
      <td>HTTPS</td>
      <td>HTTPS is used for both HTTP and HTTPS requests.</td>
   </tr>
	    <tr>
      <td>Same as request/td>
      <td>HTTP will be used for HTTP requests, and HTTPS will be used for HTTPS requests.</td>
   </tr>
</table>

>? If you select HTTPS, make sure your origin server supports HTTPS. Otherwise VOD will fail to pull data from it.

**Origin server address**

<table>
   <tr>
      <td>Self-owned server</td>
      <td>You can enter multiple IP addresses (separate with commas) or one domain.</td>
   </tr>
   <tr>
      <td>Third-party storage</td>
      <td><li>If your content is stored in the bucket of a third-party storage service, enter a valid address of the bucket (cannot contain `http://` or http:// headers). Currently, Alibaba Cloud OSS and AWS S3 are supported.</li><br><li>If you use a private bucket, you need to enter a valid access key and ID to authorize VOD to access the bucket, see <a href="https://www.tencentcloud.com/document/product/266/53277">Access Key Obtaining Guidelines</a>。</li> </td>
   </tr>
</table>

>? For self-owned origin servers, you can specify the host of a domain or IP address that VOD pulls from. If you do not specify it, VOD will pull from the current domain.
4. After adding a custom domain in VOD, for end users to access your content via the domain, you need to add a CNAME record for it at your DNS provider. For detailed directions, see [Customizing Domain Names](https://intl.cloud.tencent.com/document/product/266/35572#.E8.A7.A3.E6.9E.90.E5.9F.9F.E5.90.8D).


## Modifying Origin Server Information
You can modify the origin server information of a custom domain.
1. Go to [Domain Name](https://console.cloud.tencent.com/vod/distribute-play/domain) and select the **Custom origin server domains** tab, find the target domain, and click **Set**.
2. Click **Modify** to modify the origin server information. It takes about five minutes for modifications to take effect.
![](https://qcloudimg.tencent-cloud.cn/raw/5df5f46ec7dc7fdc55f9bc3b780f8ac7.png)

>?
>- To change a custom origin server domain to a VOD domain, you need to disable the domain, remove it as a custom origin server domain, and add it again under the **VOD acceleration domains** tab.
>- If you want to configure an origin server for a VOD domain, you need to disable the domain, remove it as a VOD acceleration domain, and add it again under the **Custom origin server domains** tab.
