## Feature Overview

You can configure the browser cache validity policies to reduce origin-pull rate.

> ?When resources are requested, if they are cached on a browser, the browser will return the resources, otherwise requests will be forwarded to CDN nodes. If the resources are cached on CDN nodes, CDN nodes will return the resources, otherwise the origin server will be pulled.

## Configuration Guide

### Viewing the configuration

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, click **Manage** on the right of a domain name to enter its configuration page, and open the **Cache Configuration** tab to find the **Browser Cache Validity Configuration** section.

For new domain names, the default rule is "Follow Origin Server" for "All Files", which cannot be deleted.
![](https://main.qcloudimg.com/raw/d74acc06100e385c87176d62459f12a6.png)

>?For existing domain names, this configuration may be empty. When you add a rule for the first time, the default rule ("Follow Origin Server" for "All Files") will be automatically added at the same time.

### Adding rules

Click **Add Rule** to add browser cache validity rules for specified file type, file directory, file path, and homepage.
<img src="https://main.qcloudimg.com/raw/d98a14185f9e9d41d682fb356601e9e5.jpg" style="height:220px"/>

- Follow Origin Server: follow the `Cache-Control` header of the origin server.
- Cache: set the cache validity of resources in a browser.
- No cache: the browser does not cache resources.



**Configuration limitations**

- Each domain name can have up to 20 rules. Only one "All Files" and "Homepage" rule can be added.
- The "All Files" rule cannot be deleted, but its cache option can be modified.
- Rule priority can be adjusted: rules at the bottom of the list have higher priority.
- In each rule of specified file type, file directory, and file path, up to 50 groups of content can be entered. Please use ";" to separate different content, e.g., Specified File Type: jpg;png.
- Chinese characters are not supported.
