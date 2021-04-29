

## Configuration Overview
HTTP2.0 is the latest HTTP version which greatly enhances the web performance and further reduces the network delay. HTTP2.0 can be directly enabled for the domain names with certificates configured and HTTPS acceleration enabled.
> !Currently, only HTTP2.0 access is supported. HTTP2.0 origin-pull is not supported.


## Configuration Guide
### Viewing the configuration
Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of a domain name to enter its configuration page. Open the **HTTPS Configuration** tab to find the **HTTP2.0 Configuration**, which is enabled by default.
![](https://main.qcloudimg.com/raw/78075916f06b8cc5b03a75ac86786fe3.png)

### Modifying the configuration
Toggle the switch to enable or disable HTTP2.0. If the domain name certificate is deleted, HTTP2.0 will be automatically disabled.
![](https://main.qcloudimg.com/raw/b4e746132ced3995845c0af895408324.png)

> !If a domain name is configured for global acceleration, the HTTP2.0 configuration will be applied to global regions, regardless of whether they’re inside or outside the Chinese mainland.
> 