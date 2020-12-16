## Feature Overview

Custom error page configuration supports redirecting a request to which the specified status code could have been returned to the specified destination URL.

Currently supported status codes are as follows:
- 4XX: 400, 403, 404, 405, 414, 416
- 5XX: 500, 501, 502, 503, 504



## Configuration Guide

### Viewing configuration

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, click **Manage** on the right of a domain name to enter its configuration page, and switch to the **Advanced Configuration** tab to find the **Custom Error Page Configuration** section.

The custom error page configuration is disabled by default.
![](https://main.qcloudimg.com/raw/ad8f4340f2f7c67247e9730a12e6d27b.png)



### Adding rules

You can click **Add Rule** to add custom error page rules as needed.



**Configuration limitations**

- Each status code can only have one unique rule.
- Redirect: 301 or 302.
- Destination URL: it must contain `http://` or `https://`, and the host should be the same as the current domain name.
- The content can contain up to 1,024 characters and Chinese characters are not supported.
