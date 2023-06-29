## Feature Overview

You can configure the custom error page, and redirect requests with the specified status code to the specified URL.

Currently supported status codes are as follows:
- 4XX: 400, 403, 404, 405, 414, 416, and 451
- 5XX: 500, 501, 502, 503, and 504

>! 
>- This feature may be unavailable on some platforms. We will complete the server upgrade as soon as possible.
>- This feature is only for redirecting requests encountered status codes during origin-pull, but not applicable to requests with status codes returned by any access control features such as the UA blocklist/allowlist configuration.

## Configuration Guide

### Viewing the configuration

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, click **Manage** on the right of a domain name to enter its configuration page, and switch to the **Advanced Configuration** tab to find the **Custom Error Page Configuration** section.

The custom error page configuration is disabled by default.
![](https://main.qcloudimg.com/raw/ad8f4340f2f7c67247e9730a12e6d27b.png)



### Adding rules

You can click **Add Rule** to add custom error page rules as needed.
<img src="https://main.qcloudimg.com/raw/7af17d161ec2f4e499a5740383d4658e.jpg" style="height:220px"/>



**Configuration limitations**

- Each status code can only have one unique rule.
- Redirect: 301 or 302.
- Destination URL: `http://` or `https://` is required.
- The content can contain up to 1,024 characters and Chinese characters are not supported.
