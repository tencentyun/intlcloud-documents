

## Configuration Overview

HTTP Strict Transport Security (HSTS) is a web security protocol promoted by the Institution of Electronics and Telecommunication Engineers (IETE). It forces the client (such as a browser) to use HTTPS to create a connection with the server so as to help encrypt the website globally.

## Configuration Limitations

- `expireTime` can range from 0 to 365 days and is configured in seconds.
- Check `includeSubDomain` if you need to include sub-domain names.
- To enable HSTS configuration, HTTPS acceleration configuration must be completed first.
- After the HSTS configuration is enabled, we recommend enable [Forced Redirection Configuration](https://intl.cloud.tencent.com/document/product/228/35214) to redirect HTTP requests to HTTPS requests. Otherwise the browser will not create HSTS cache for HTTP requests.

## Configuration Guide

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of a domain name to enter its configuration page. Open the **HTTPS Configuration** tab to find the **HSTS Configuration** section. It is disabled by default.
![](https://main.qcloudimg.com/raw/4e44076b3485c9de15776134af7d5e96.png)
Toggle it on and configure accordingly:
![](https://main.qcloudimg.com/raw/5a98a2ede54d4eceb8b5f4f0a8bbaa3b.png)
Click **Confirm** to apply the configuration to the response header. You can click **Edit** to modify it later.
![](https://main.qcloudimg.com/raw/e22e2cf4ad493379db7f1bcf49cfa03a.png)

## Configuration Sample

If the HSTS configuration of the domain name `cloud.tencent.com` is as follows:
![](https://main.qcloudimg.com/raw/58e49b2b5a0b94f21fa3547dda08daed.png)
The response header is:
![](https://main.qcloudimg.com/raw/910e57e5abdedba4a33b4e4748a81318.png)

