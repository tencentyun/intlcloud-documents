## Feature Overview

Browser cache validity configuration supports customizing client browser cache policies to reduce origin-pull rate.



## Configuration Guide

### Viewing configuration

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, click **Manage** on the right of a domain name to enter its configuration page, and switch to the **Cache Configuration** tab to find the **Browser Cache Validity Configuration** section.

After a new domain name is added, as the platform default policy is "Follow Origin Server", there will be a default rule which cannot be deleted: Type: All Files; Cache Behavior: Follow Origin Server.
![](https://main.qcloudimg.com/raw/d74acc06100e385c87176d62459f12a6.png)

>?In the configuration of existing domain names, there may be no rules. After a rule is added, the default rule will be automatically added: Type: All Files; Cache Behavior: Follow Origin Server.

### Adding rules

You can click **Add Rule** to add browser cache validity rules as needed. The supported cache types are specified file type, file directory, file path, and homepage.

![](https://main.qcloudimg.com/raw/d98a14185f9e9d41d682fb356601e9e5.jpg)

- Follow Origin Server: follow the `Cache-Control` header of the origin server.
- Cache: set the cache time of resources in a browser.
- No cache: obtain resources from the origin server.




**Configuration limitations**

- Each domain name can have up to 20 rules. Only one "All Files" and "Homepage" rule can be added.
- The "All Files" rule cannot be deleted, but its cache option can be modified.
- You can adjust the priority for multiple rules. Rules at the bottom of the list have higher priority.
- In each rule of specified file type, file directory, and file path, up to 50 groups of content can be entered. Please use ";" to separate different content, e.g., Specified File Type: jpg;png.
- Chinese characters are not supported.
