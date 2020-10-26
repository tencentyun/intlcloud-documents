

## Configuration

HTTP Strict Transport Security (HSTS) is a web security protocol promoted by the Institution of Electronics and Telecommunication Engineers (IETE). It forces the client (such as the browser) to use HTTPS to create a link with the server to help encrypt the website globally.

## Configuration Limitations

- `expireTime` can range from 0 to 365 days and is configured in seconds.
- The `includeSubDomain` parameter can be controlled by selecting whether or not to include sub-domain names.
- To enable HSTS configuration, HTTPS acceleration configuration must be completed first.

## Configuration Guide

Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** to the right of the target domain name to access its configuration page. Then, click the **Advanced Configuration** tab. In the **HTTPS Configuration** section, you can see the HSTS configuration item, which is disabled by default:
![](https://main.qcloudimg.com/raw/4e44076b3485c9de15776134af7d5e96.png)
Toggle the switch to enable this feature and configure it accordingly:
![](https://main.qcloudimg.com/raw/5a98a2ede54d4eceb8b5f4f0a8bbaa3b.png)
After you click **OK**, the response header value will be determined according to the configured content. You can click **Edit** to modify it:
![](https://main.qcloudimg.com/raw/e22e2cf4ad493379db7f1bcf49cfa03a.png)

## Configuration Sample

Suppose the HSTS configuration of the domain name `cloud.tencent.com` is as follows:
![](https://main.qcloudimg.com/raw/58e49b2b5a0b94f21fa3547dda08daed.png)
When accessed, its response header is:
![](https://main.qcloudimg.com/raw/910e57e5abdedba4a33b4e4748a81318.png)

