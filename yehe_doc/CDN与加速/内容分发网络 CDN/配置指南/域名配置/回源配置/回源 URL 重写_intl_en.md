## Overview

If you need to modify the origin-pull request URL to the URL that matches the origin server, you can use the origin URL rewrite configuration in Tencent Cloud CDN.

>! This feature is not available for ECDN domain name.


## Directions

### Viewing the configuration

Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, click **Manage** on the right of a domain name to enter its configuration page, and switch to the **Origin-pull Configuration** tab to find the **Origin URL Rewrite Configuration** section.
![](https://main.qcloudimg.com/raw/e6721b8c8d3ebcb9b5a27fb36e6c6782.png)



### Adding rules

You can click **Add Rule** to add rewrite rules as needed.
<img src="https://main.qcloudimg.com/raw/5f7d6907976fb0696f633af29321c99c.jpg" style="height:300px"/>


**Configuration limitations**

- Each domain name can have up to 100 rewrite rules.
- You can adjust the priority for multiple rules. Rules at the bottom of the list have higher priority.
- Current Origin URL: starting with “/”; prefix matching is used by default; supporting full-path matching (e.g., /test/a.jpg) and wildcard (*) matching (e.g., /test/*/*.jpg). If you want to specify a file directory, you cannot end the path with “/” (e.g., /test).
- Target Origin Domain: the current domain name is used by default (excluding “http://” and “https://”). You can modify it as needed.
- Target Origin Path: starting with “/” (e.g., /newtest/b.jpg); the wildcard “*” can be captured with “$n” (e.g., if n=1,2,3… then /newtest/$1/$2.jpg). If you want to specify a file directory, you cannot end the path with “/” (e.g., /test).
- Up to 5 “*” and 10 “$n” are supported.
- The target origin domain can contain up to 250 characters. Other content can contain up to 1,024 characters. 



## Configuration Samples:

Suppose the **Origin URL Rewrite Configuration** of the acceleration domain name www.test.com is as follows:


The origin-pull will be rewritten as follows:
- In case www.test.com/images/1.jpg is requested, the request hits the first, second and third rule. As rules are executed from the bottom to top, the URL will be re-written to www.test.com/index.html.
- In case www.test.com/images is requested and the request hits the second rule, the URL will be rewritten to www.test.com/goodboy.html.
