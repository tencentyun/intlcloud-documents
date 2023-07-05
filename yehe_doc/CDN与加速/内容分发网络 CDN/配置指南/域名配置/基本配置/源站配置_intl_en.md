## Overview

You can modify the domain name's origin server basic information, origin-pull protocol, origin domain, and other information in the origin server configuration module.

>! We recommend that you configure your origin server in the same region as the acceleration region. For example, if the acceleration region resides in the Chinese mainland, configure your origin server in the Chinese mainland. If you configure the origin server in Hong Kong (China) or outside the Chinese mainland, cross-board access is required during origin-pull. In this case, the origin-pull effect may not be ensured.
If your acceleration domain name is configured for global acceleration, you can configure independent origin servers respectively for different regions in the origin server configuration module of the domain name. This way, origin-pull requests that are initiated in and outside the Chinese mainland are sent to different origin servers. This ensures the origin-pull effect.

## Directions

### Primary origin server configuration

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of a domain name to enter its configuration page. Open the **Basic Configuration** tab to see the **Origin Server Information** section.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/9IJQ709_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230224110508.png)

**Origin server type**

<table>
<thead>
<tr>
<td style="width:150px">Customer origin</td>
<td>You can use a stable business server that is running as the origin server. Enter the corresponding IP list or a domain name as the origin server address.</td></ul>
</tr>
</thead>
<tbody><tr>
<td><a href="https://www.tencentcloud.com/products/cos">Tencent Cloud COS Origin</a></td>
<td>You can select a COS bucket as the origin server. Private bucket access can be enabled.</td>
</tr>
<tr>
<td>Third-Party Object Storage Origin	
</td>
<td>You can use a bucket of a third-party object storage service other than Tencent Cloud COS as the origin server. Currently, the supported third-party object storage services include Amazon S3, Alibaba Cloud OSS, Huawei Cloud OBS, and Qiniu Cloud KODO.<br/>
<strong>Note:</strong> Currently, ECDN does not support origin servers that are based on third-party object storage services.</td>
</tr>
</tbody></table>


**Origin-pull protocol**
The protocol used when a CDN cache node forwards requests to the origin server for origin-pull. You can select HTTP or HTTPS.

<table>
<thead>
<tr>
<td style="width:150px">HTTP Origin-pull</td>
<td>CDN pulls HTTP or HTTPS content from the origin server over HTTPS.</td></ul>
</tr>
</thead>
<tbody><tr>
<td>HTTPS Origin-pull</td>
<td>CDN pulls HTTP or HTTPS content from the origin server over HTTPS to prevent theft and tampering of origin-pull data with low CPU usage. Make sure that the origin server is accessible over HTTPS.</td>
</tr>
<tr>
<td>Follow Protocol</td>
<td>HTTP is used for an origin-pull of HTTP content. HTTPS is used for an origin-pull of HTTPS content. HTTPS is also used when you transfer key sensitive content. We recommend that you select this option. Make sure that the origin server is accessible over HTTPS.
</td>
</tr>
</tbody></table>

> !If you select HTTPS origin-pull, make sure that the origin server is accessible over HTTPS. Otherwise, origin-pull may fail.



**Origin server address**
<table>
<thead>
<tr>
<td style="width:80px">External origin</td>
<td style="padding-bottom:0px;padding-top:15px"><ul><li>You can enter multiple origin IPs or origin domain names with one entry per line.
  <br><strong>Origin-pull from multiple origin IPs in round robin mode:</strong> You can enter multiple origin IPs with one entry per line to pull content from these IPs in round robin mode. CDN checks the availability of each origin IP by default. If content fails to be pulled from an IP or if more than five origin-pull requests that are sent to the origin IP time out within one minute, no more origin-pull requests are sent to the origin IP. The origin IP is blocked for 600 seconds and automatically resumed later.<br><strong>Origin-pull from a domain name:</strong> You can configure a domain name as the origin server address. The domain name must be different from the acceleration domain name. You cannot use IPv6 domain names.<br><strong>Note:</strong> You cannot enter a domain name that is connected to CDN and points to the acceleration domain name. Otherwise, resolution loop occurs, which leads to origin-pull failures.<li> When you enter an origin IP or domain name, you can add a port that ranges from 0 to 65535 and a weight that ranges from 1 to 100 in the format of Origin server address:Port:Weight or Origin server address::Weight. By default, the port is omitted.<br><strong>Note:</strong> The weights are sorted based on the size of the number. The larger the number, the higher the weight, and the higher the priority of the origin IP or domain name.<li>The origin server address can contain up to 511 characters.</td></ul>
</tr>
</thead>
<tbody><tr>
<td><a href="https://www.tencentcloud.com/products/cos">Tencent Cloud COS Origin</a></td>
<td><li>Select a COS bucket as the origin server.<li>Select the default domain name, static website domain name, or global acceleration domain name as the bucket address based on the bucket configuration and your actual business needs. For example, if the static website configuration is enabled for the selected bucket, select the static website domain name.<li>If the access permission of the bucket is set to private read, authorize CDN to access the bucket, and enable origin-pull authentication to allow private bucket access.</td>
</tr>
<tr>
<td>Third-Party Object Storage Origin</td>
<td style="padding-bottom:0px;padding-top:15px"><ul><li>If your resources are stored in a bucket of a third-party object storage service, enter a valid bucket address as the origin server address. Currently, the supported third-party object storage services include Amazon S3, Alibaba Cloud OSS, Huawei Cloud OBS, and Qiniu Cloud KODO.</br><strong>Example:<code> my-bucket.s3.ap-east-1.amazonaws.com</code> or <code>my-bucket.oss-cn-beijing.aliyuncs.com</code>. </strong>The bucket address cannot contain the <code>http://</code> or <code>http://</code> protocol header.<li>If you use a private bucket of a third-party object storage service as the origin server, enter a valid key and enable origin-pull authentication to allow private bucket access.</td>
</tr></ul>
</tbody></table>




**Origin domain**
It refers to the domain name that is accessed on the origin server by a CDN node during origin-pull. For more information about how to configure an origin domain, see [Origin domain configuration](#exp).

> ?The differences between an origin server address and an origin domain are as follows:
> - Origin server address specifies the IP address to which an origin-pull request is sent.
> - Origin domain specifies the website corresponding to the IP address to which an origin-pull request is sent.

<table>
<thead>
<tr>
<td style="width:80px">External origin</td>
<td >The acceleration domain name is used as the origin domain by default. If a wildcard domain name is connected, the origin domain is the actual access domain name by default and can be customized.</td></tr>
</thead>
<tbody><tr>
<td><a href="https://www.tencentcloud.com/products/cos">Tencent Cloud COS Origin</a></td>
<td>The bucket access address is used as the origin domain by default, which is the same as the origin server address and cannot be modified.</td>
</tr>
<tr>
<td>Third-Party Object Storage Origin</td>
<td>The bucket access address is used as the origin domain by default, which is the same as the origin server address and cannot be modified.</td>
</tr>
</tbody></table>



### Hot backup origin server configuration

You can add a hot backup origin server for your primary origin server. All origin-pull requests will be forwarded to the primary origin server first. If a 4XX or 5XX error code is returned or an exception such as connection timeout or protocol incompatibility occurs, requests will be forwarded to the hot backup origin server to pull resources, ensuring the high availability of origin-pull.

The hot backup origin server can be configured with its own origin server address and origin domain.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/fBH6442_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230224110649.png)

>!
>- You cannot use a COS bucket or a bucket of a third-party object storage service as a hot backup origin server.
>- If an IPv6 origin server is used as the primary origin server, it cannot be configured with a hot backup origin server.
>- You cannot configure the weight of a hot backup origin server.

### Region-specific configuration

If your acceleration domain name is configured for global acceleration and you want to avoid cross-border traffic, click **+ Region-specific configuration** to configure different origin servers for different service regions of the acceleration domain name.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/XXa9147_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230224112431.png)
Select regions that need different origin-pull policies and enter the corresponding origin server information. For more information, see [Region-specific configuration](#special).

>!
>
>- You cannot add a region-specific configuration if you use a bucket of a third-party object storage service as the origin server.


## Configuration Samples

### Origin domain configuration[](id:exp)

If the CDN origin server and the acceleration domain name `www.test.com` are configured as follows:
![](https://main.qcloudimg.com/raw/ec2e007bb32723f7dd12aac17524c8af.png)
The access route for the user will be:
When a user accesses the resource `http://www.test.com/test.txt` that has not been cached on the CDN node, the node will resolve the domain name `www.abc.com` to get the origin server address `1.1.1.1`. Then, the CDN node will access the server `1.1.1.1`, find the `test.txt` file in the website path `www.def.com`, and return the file to the user.


[](id:special)
### Region-specific configuration

If the CDN origin server and the acceleration domain name `www.test.com` are configured as follows:
![](https://main.qcloudimg.com/raw/e9104ca2b0e38c62bdffb022a933b2b9.png)
The actual origin-pull will then be:

1. When a user in the Chinese mainland accesses the file `http://www.test.com/test.txt` and the node in the Chinese mainland has not cached this resource, it will forward the request to the server `1.1.1.1` and try to find the `test.txt` file in the website path `1.test.com`. If the resource exists, the node will directly return the file to the user. If not, it will go to step 2.
2. As the CDN node in Mainland China fails to forward the request to the primary origin server and cannot find the resource, it will forward the request to the server `2.2.2.2`, find the `test.txt` file in the website path `2.test.com`, cache and return it to the user.
3. At this time, a user outside the Chinese mainland accesses the file `http://www.test.com/test.txt`. As the node outside the Chinese mainland has not cached this resource, it will forward the request to the server `3.3.3.3` and try to find the `test.txt` file in the website path `3.test.com`. If the resource exists, the node will directly return the file to the user. If not, it will go to step 4.
4. As the CDN node outside the Chinese mainland fails to forward the request to the primary origin server outside the Chinese mainland and cannot find the resource, it will forward the request to the server `4.4.4.4`, find the `test.txt` file in the website path `4.test.com`, and then cache and return it to the user outside the Chinese mainland.
