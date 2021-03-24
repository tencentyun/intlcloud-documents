## Configuration Overview

In the **Origin Server Configuration** section, you can modify the domain name's origin server basic information, origin-pull protocol, origin domain, and other information.


## Configuration Guide

### Primary origin server configuration

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of a domain name to enter its configuration page. Open the **Basic Configuration** tab to see the **Origin Server Information** section.
![img](https://main.qcloudimg.com/raw/524f3c9aa2f9f2017d53409ee610bb5b.png)
**Origin server type**
External origin: Select this option if you already have your own business server (i.e., origin server), and enter the corresponding IP address list or a domain name as the origin server address.
[COS origin](https://intl.cloud.tencent.com/product/cos): If your resources are stored in COS, the bucket can be selected as the origin server.

**Origin-pull protocol**
The protocol used when a CDN cache node forwards requests to the origin server for origin-pull. You can select HTTP or HTTPS.

You can configure origin-pull protocol for the domain name to HTTP, HTTPS, or follow protocol in origin server configuration:

- **HTTP**: HTTP origin-pull is used for access requests over both HTTP and HTTPS.
- **HTTPS**: HTTPS origin-pull is used for access requests over both HTTP and HTTPS.
- **Follow protocol**: HTTP requests use HTTP origin-pull, while HTTPS requests use HTTPS origin-pull.

> !
> - If you select HTTPS origin-pull, make sure the origin server supports HTTPS access, otherwise origin-pull will fail.
> - Currently, you can still modify this configuration item on the certificate management page. However, it will be migrated in the future.



**Origin server address**
<table>
<thead>
<tr>
<td style="width:80px">External origin</td>
<td style="padding-bottom:0px;padding-top:15px"><ul><li>You can enter a domain name or multiple IPs (one entry per line) as the origin server:
  <br><strong>Multi-IP polling origin-pull: </strong>Multiple IPs (one entry per line) can be set as the origin server and are polled during origin-pull. CDN checks the origin server by default. If an IP fails for certain times during origin-pull, it will be automatically blocked for a period of time and resumed later, during which no origin-pull request is sent there.<br>If you are accepted as an IPv6 origin server beta user and enable the IPv6 origin server when adding the domain name, you can enter an IPv6 origin server.<br><strong>Domain name origin-pull: </strong>A single domain name can be configured as the origin server, which must be different from the business acceleration domain name (IPv6 domain name cannot be used here).<br><li>Port and weight can be configured: port range: 0-65535; weight: 1-100; format: origin server:port:weight (the port can be omitted, format: origin server::weight)<br><strong>Note: </strong>If "HTTPS" or "Follow Protocol" is selected as the origin-pull protocol, the port should be 443 or left empty.<br><li>Up to 511 characters can be entered in the origin server input box.</td></ul>
</tr>
</thead>
<tbody><tr>
<td>COS origin</td>
<td>You can select a COS bucket as the origin server. Private bucket access can be enabled.</td>
</tr>
</tbody></table>




**Origin domain**
An origin domain refers to the website domain name accessed at the origin server IP address by a CDN node during origin-pull. It defaults to the current acceleration domain name or a wildcard domain name if a wildcard one is connected, and the actual origin domain is the access domain name. You can modify it as needed except for the case where a COS origin is used. For more information, please see [Origin Server Configuration](https://intl.cloud.tencent.com/document/product/228/6289).

> ?The differences between an origin server address and an origin domain are as follows:
> - Origin server address specifies the IP address to which an origin-pull request is sent.
> - Origin domain specifies the website corresponding to the IP address to which an origin-pull request is sent.

### Hot backup origin server configuration

You can add a hot backup origin server for your primary origin server. All origin-pull requests will be forwarded to the primary origin server first. If a 4XX or 5XX error code is returned or an exception such as connection timeout or protocol incompatibility occurs, requests will be forwarded to the hot backup origin server to pull resources, ensuring the high availability of origin-pull.

The hot backup origin server can be configured with its own origin server address and origin domain.
![img](https://main.qcloudimg.com/raw/4d2ba172412182eb87ba40149775689f.png)

>!If an IPv6 origin server is used as the primary origin server, it cannot be configured with a hot backup origin server.

### Region-specific configuration

If your acceleration domain name is configured for global acceleration and you want to avoid cross-border traffic, you can click **Add Special Configuration** to configure different origin servers for different service regions of the acceleration domain name:
![img](https://main.qcloudimg.com/raw/d4a7a61ed28daa2c3eb0febf02ca931c.png)
Select regions that need different origin-pull policies and enter the corresponding origin server information.

>!
> - After the region-specific configuration is added, it currently cannot be directly deleted.
> - If the region-specific configuration is exactly the same as the basic configuration, they will automatically merge. You can configure them to be the same to delete the region-specific configuration.

## Configuration Samples
[](id:exp)
### Origin domain configuration

If the CDN origin server and the acceleration domain name `www.test.com` are configured as follows:
![img](https://main.qcloudimg.com/raw/ec2e007bb32723f7dd12aac17524c8af.png)
The access route for the user will be:
When a user accesses the resource `http://www.test.com/test.txt`, which is not cached on the CDN node, the node will resolve the domain name `www.abc.com` to get the origin server address `1.1.1.1`. Then, the CDN node will access the server `1.1.1.1`, find the `test.txt` file in the website path `www.def.com`, and return the file to the user.

### Region-specific configuration

If the CDN origin server and the acceleration domain name `www.test.com` are configured as follows:
![img](https://main.qcloudimg.com/raw/e9104ca2b0e38c62bdffb022a933b2b9.png)
The actual origin-pull process will be:

1. When a user in the Chinese mainland accesses the file `http://www.test.com/test.txt` and the node in the Chinese mainland has not cached this resource, it will forward the request to the server `1.1.1.1` and try to find the `test.txt` file in the website path `1.test.com`. If the resource exists, the node will directly return the file to the user. If not, it will go to Step 2.
2. As the CDN node in the Chinese mainland fails to forward the request to the primary origin server and cannot find the resource, it will forward the request to the server `2.2.2.2`, find the `test.txt` file in the website path `1.test.com`, and then cache and return it to the user.
3. At this time, a user outside the Chinese mainland accesses the file `http://www.test.com/test.txt`. As the node outside the Chinese mainland has not cached this resource, it will forward the request to the server `3.3.3.3` and try to find the `test.txt` file in the website path `3.test.com`. If the resource exists, the node will directly return the file to the user. If not, it will go to step 4.
4. As the CDN node outside the Chinese mainland fails to forward the request to the primary origin server outside the Chinese mainland and cannot find the resource, it will forward the request to the server `4.4.4.4`, find the `test.txt` file in the website path `4.test.com`, and then cache and return it to the user outside the Chinese mainland.
