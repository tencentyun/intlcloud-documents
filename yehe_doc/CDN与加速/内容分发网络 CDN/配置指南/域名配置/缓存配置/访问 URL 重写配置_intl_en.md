## Configuration Overview

If you need to modify the actual access URL to the URL that matches the origin server, you can use the access URL rewrite configuration in Tencent Cloud CDN.

You can customize the access URL rewrite configuration to redirect 302 URLs to the specified URL.

## Configuration Guide

### Viewing configuration

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, click **Manage** on the right of a domain name to enter its configuration page, and open the **Cache Configuration** tab to find the **Access URL Rewrite Configuration** section.

**Access URL Rewrite Configuration** is disabled by default.
![](https://main.qcloudimg.com/raw/01f93aaa70c523ae0bb1ab5debae8558.png)


### Adding rules

You can click **Add Rewrite Rule** to add rules as needed.
<img src="https://main.qcloudimg.com/raw/97ea8713395f3af8654c39be97f124d3.png"  style="height:300px"></img>

**Configuration limitations**
+ Each domain name can have up to 100 rewrite rules.
+ You can adjust the priority for multiple rules. Rules at the bottom of the list have higher priority.
+ Current URL: starting with `/`; supporting full-path matching (e.g., /test/a.jpg) and wildcard (*) matching (e.g., /test/*/*.jpg). If you want to specify a file directory, you cannot end the path with `/` (e.g., /test).
+ Target Host: it is the current domain name (starting with `http://`) by default. It can be modified to other domain names starting with `http://` or `https://`.
+ Target Path: starting with `/` (e.g., /newtest/b.jpg); the wildcard `*` can be captured with `$n` (e.g., if n=1,2,3… then /newtest/$1/$2.jpg). If you want to specify a file directory, you cannot end the path with `/` (e.g., /test).
+ Up to 5 `*` and 10 `$n` are supported.
+ The content can contain up to 1,024 characters and Chinese characters are not supported.




## Configuration Samples

If the **Access URL Rewrite Configuration** of the acceleration domain name `www.test.com` is as follows:
![](https://main.qcloudimg.com/raw/214b034e578d5eaac0a63cacd49f1e2d.png)

Then the actual access will be as follows:

+ A client requests `www.test.com/test/a.jpg` and the CDN node returns `www.test.com/newtest/b.jpg`.
+ A client requests `www.test.com/test/a.png` and the CDN node returns `www.newtest.com/newtest/a.png`.



