## Configuration Overview

If you need to modify the origin URL to the URL that matches the origin server, you can use the origin URL rewrite configuration in Tencent Cloud CDN.



## Configuration Guide

### Viewing configuration

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, click **Manage** on the right of a domain name to enter its configuration page, and switch to the **Origin-pull Configuration** tab to find the **Origin URL Rewrite Configuration** section.
![](https://main.qcloudimg.com/raw/e6721b8c8d3ebcb9b5a27fb36e6c6782.png)



### Adding rules

You can click **Add Rule** to add rewrite rules as needed.

![](https://main.qcloudimg.com/raw/5f7d6907976fb0696f633af29321c99c.jpg)


**Configuration limitations**

- Each domain name can have up to 10 rewrite rules.
- You can adjust the priority for multiple rules. Rules at the bottom of the list have higher priority.
- Current Origin URL: starting with `/`; supporting full-path matching (e.g., /test/a.jpg) and wildcard (*) matching (e.g., /test/*/*.jpg).
- Target Origin Domain: it is the current domain name by default and can be modified. It excludes `http://` and `https://`.
- Target Origin Path: starting with `/` (e.g., /newtest/b.jpg); the wildcard `*` can be captured with `$n` (e.g., if n=1,2,3… then /newtest/$1/$2.jpg).
- The target origin domain can contain up to 250 characters. Other content can contain up to 1,024 characters. Chinese characters are not supported.



## Configuration Samples:

If the **Origin URL Rewrite Configuration** of the acceleration domain name `www.test.com` is as follows:
![](https://main.qcloudimg.com/raw/4797e184e62c1abd5ed3cf1d1091f3fb.png)

Then the actual origin-pull will be as follows:

- Pull the origin server to request `www.test.com/test/`, `www.test.com/newtest/` will be actually requested.
- Pull the origin server to request `www.test.com/test/a.jpg`, `www.newtest.com/newtest/a.jpg` will be actually requested.
