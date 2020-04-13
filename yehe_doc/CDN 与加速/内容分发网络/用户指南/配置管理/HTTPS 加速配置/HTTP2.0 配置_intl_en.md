## Configuration Scenario
If a domain name has been configured with a certificate for HTTPS acceleration, you can enable HTTP2.0 support.
>Currently, only HTTP2.0 access is supported. HTTP2.0 origin-pull is not supported.

## Configuration Guide
### Viewing configuration
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of the domain name to enter its configuration page. Under the **Advanced Configuration** tab, find **HTTP2.0 Configurations**, which is enabled by default:
![](https://main.qcloudimg.com/raw/b4e746132ced3995845c0af895408324.png)

### Modifying configuration
Switch to enable or disable HTTP2.0. After the certificate configuration is deleted, HTTP2.0 configuration will be automatically invalidated:
![](https://main.qcloudimg.com/raw/78075916f06b8cc5b03a75ac86786fe3.png)

>If your domain name is configured for global acceleration, HTTP2.0 configuration will take effect globally. This configuration does not distinguish between requests from and outside of Mainland China.

