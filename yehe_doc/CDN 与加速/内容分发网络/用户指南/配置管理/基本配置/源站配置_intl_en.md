## Configuration

You can modify the domain name’s basic information such as the origin-pull protocol, and origin domain in the origin server configuration module.

## Configuration Guide

### Viewing the configuration
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of the domain name to access its configuration page. You can find the origin server configuration module in the **Basic Configuration** tab.
![](https://main.qcloudimg.com/raw/524f3c9aa2f9f2017d53409ee610bb5b.png)
**Origin Server Type**
External Origin: select this option if you already have your own business server (i.e., origin server). Enter the corresponding IP address list or domain name as the origin server address.
[COS Origin](https://intl.cloud.tencent.com/product/cos): if resources are stored in COS, the bucket can be selected as the origin server.
**Origin Server Address**
Enter an origin server address corresponding to the origin server type.
**Origin-pull Protocol**
The protocol used when a CDN cache node forwards requests to the origin server for origin-pull. You can select HTTP or HTTPS.
**Origin Domain**
The site domain name accessed on the origin server by a CDN node during origin-pull. For more information, please see [Origin-Pull Domain Name Configuration](#exp).

### Modifying the configuration
#### 1. Modify the primary origin server configuration
Click **Edit** on the top-right corner to modify the configuration of the primary origin server:

**Modify the origin server address**
If external origin server is selected, you can enter up to 511 characters for the origin server address. The following configuration modes are supported:
- **Multi-IP round-robin origin-pull**: if multiple IPs are entered for the origin server, round-robin origin-pull will be used. The origin server detection feature of CDN is enabled by default. When the number of failed origin-pulls of an IP exceeds the threshold, requests will no longer be forwarded to this address, which will be blocked for a period of time and then automatically resumed.
- **IPv6 origin server**: if you have IPv6 beta eligibility and selected "IPv4 + IPv6" as the request protocol of the domain name, you can enter an IPv6 address as the origin server.
- **Origin-pull to custom port**: "origin server:port" format is supported. HTTP protocol supports the custom port between 1 and 65535. HTTPS protocol currently only supports port 443.
- **Weighted origin-pull**: configure weight between 1 to 100 in the format of "origin server:port:weight". The port can be omitted: “origin server::weight”.
- **Domain name origin-pull**: You can configure a domain name as the origin server, which should be different from the business acceleration domain name. (Currently, origin-pull to IPv6 domain name is not supported).

**Modify the origin-pull protocol**
You can configure origin-pull protocol for the domain name to HTTP, HTTPS, or follow protocol in the origin server configuration section:
+ **HTTP**: HTTP origin-pull is used for access requests over both HTTP and HTTPS.
+ **HTTPS**: HTTPS origin-pull is used for access requests over both HTTP and HTTPS.
+ **Follow protocol**: HTTP requests use HTTP origin-pull, while HTTPS requests use HTTPS origin-pull.

> !
> + If you select HTTPS origin-pull or follow protocol, make sure the origin server supports HTTPS access. Otherwise, origin-pull will fail.
> + Currently, you can still modify this configuration item on the certificate management page. However, it will be migrated in the future.

**Modify the origin domain**
When a domain name is connected, the default origin domain will be the acceleration domain name. If a wildcard domain name is connected, it will be the default origin domain, while the actual origin domain will be the access domain name. You can modify it here as needed.

> ! If COS is used as the origin server, the origin domain cannot be modified.

#### 2. Configure the hot backup origin server
If your primary origin server is an external one, you can add a hot backup origin server. All origin-pull requests will be forwarded to the primary origin server first. If a 4XX or 5XX error code is returned or an exception such as connection timeout or protocol incompatibility occurs, requests will be forwarded to the hot backup origin server to pull resources and ensure the high availability of origin-pull.

You can configure origin-pull protocol and origin domain for the hot backup origin server differently from those for the primary origin server.
![](https://main.qcloudimg.com/raw/4d2ba172412182eb87ba40149775689f.png)

>! If your primary origin server is a IPv6 address, the hot backup origin servers cannot be added.

#### 3. Add the region-specific configuration
If your acceleration domain name is configured for global acceleration and you want to avoid cross-border traffic, you can click **Add Special Configuration** at the bottom to configure different origin servers for different service regions of the domain name:
![](https://main.qcloudimg.com/raw/d4a7a61ed28daa2c3eb0febf02ca931c.png)
Select regions that need different origin-pull policies and enter the corresponding origin server information:
![](https://main.qcloudimg.com/raw/d8f02e0ae1e44972cedd07160bb9f5cb.png)

> !
> + After the region-specific configuration is added, it currently cannot be directly deleted.
> + If the region-specific configuration is the same as the basic configuration, they will automatically merge. You can configure them to be the same to delete the region-specific configuration.

## Configuration Samples
<a ID="exp"></a>
### Origin-pull domain name configuration
Suppose the CDN origin server and the acceleration domain name `www.test.com` are configured as follows:
![](https://main.qcloudimg.com/raw/ec2e007bb32723f7dd12aac17524c8af.png)
The access route for the user will be:
When a user accesses the resource `http://www.test.com/test.txt` that has not been cached on the CDN node, the node will resolve the domain name `www.abc.com` to get the origin server address `1.1.1.1`. Then, the CDN node will access the server `1.1.1.1`, find the `test.txt` file in the website path `www.def.com`, and return the file to the user.

### Region-specific configuration
Suppose the CDN origin server and the acceleration domain name `www.test.com` are configured as follows:
![](https://main.qcloudimg.com/raw/e9104ca2b0e38c62bdffb022a933b2b9.png)
The actual origin-pull will then be:

1. When a user in mainland China accesses the file `http://www.test.com/test.txt` and the node in mainland China has not cached this resource, it will forward the request to the server `1.1.1.1` and try to find the `test.txt` file in the website path `1.test.com`. If the resource exists, the node will directly return the file to the user. If not, it will go to step 2.
2. As the CDN node in mainland China fails to forward the request to the primary origin server and cannot find the resource, it will forward the request to the server `2.2.2.2`, find the `test.txt` file in the website path `1.test.com`, and then cache and return it to the user.
3. At this time, a user outside of mainland China accesses the file `http://www.test.com/test.txt`. As the node outside of mainland China has not cached this resource, it will forward the request to the server `3.3.3.3` and try to find the `test.txt` file in the website path `3.test.com`. If the resource exists, the node will directly return the file to the user. If not, it will go to step 4.
4. As the CDN node outside of mainland China fails to forward the request to the primary origin server outside of mainland China and cannot find the resource, it will forward the request to the server `4.4.4.4`, find the `test.txt` file in the website path `4.test.com`, and then cache and return it to the user outside of mainland China.
